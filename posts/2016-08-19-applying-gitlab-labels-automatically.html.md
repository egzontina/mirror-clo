---
title: "Applying GitLab Labels Automatically"
author: "Brian O'Connell"
author_twitter: boc_tothefuture
categories: GitLab
image_title: '/images/blogimages/applying-gitlab-labels-automatically-cover.jpg'
description: "Learn how to use GitLab Webhooks to apply labels automatically to MRs."
twitter_image: '/images/tweets/applying-gitlab-labels-automatically.png'
date: 2016-08-19 11:00
---

This is a customer story on how Brian uses [GitLab Webhooks][doc-webhooks]
to apply **labels** automatically to his projects' merge requests.

This article follows up his previous post, on how [using GitLab Labels][post-1]
helps him to direct focus and improve his workflow.

<!-- more -->

## Automatic application of GitLab Labels

In my previous post I described how to use [GitLab Labels][doc-labels]
to easily triage. [@shochdoerfer] asked me:

> _[@boc_tothefuture] how can [@GitLab] labels be applied automatically
for issues or merge requests?_

### A quick webhook server

We use [GitLab webhooks][doc-webhooks] to automatically apply labels
to incoming merge requests (MRs). To process the webhooks, we wrote a
simple [webrick] server whose process is supervised by [runit] and the
incredibly well written [runit cookbook][ru-cook].

### Adding labels automatically

Using the Webrick as a base it’s fairly easy to get labels added to your
MRs when they are opened. When the request comes in to your webrick server,
look at the GitLab `object_kind` to see if it's a MR.

```ruby
def merge_request?(request_body)
  body['object_kind'] == 'merge_request'
end
```

If the code is a merge request, the next step is calculate the labels that
should be applied to the MR. In our case that is a ‘Needs Review’ label
if the MR is just being opened. Then because we use [Semver] and
[thor-scmversion][thor] we just scan all the commit messages for `#patch`, `#minor`
and `#major` to apply the appropriate Semver tag to the MR.

You will need a valid [GitLab API][doc-api] key to modify and or request data about a MR.

```ruby
def update_labels(gitlab_server, api_key, request_body )
  project_id = request_body['object_attributes']['target_project_id']
  request_id = ['object_attributes']['id']
  labels = ['Needs Review'] if request_body['object_attributes']['action']
  semver_increment = semver_increment(gitlab_server, api_key,request_body )
  labels += semver_increment if semver_increment

  merge_data = {id: hook_id(hook), project_id: project_id(hook), labels: labels.to_a.sort.join(',')}
  url = "#{gitlab_server}/api/v3/projects/#{project_id}/merge_requests/#{request_id}?private_token=#{api_key}"
  RestClient::Request.execute(:method => :put, :payload => merge_data, :url => url)
end

def semver_increment(gitlab_server, api_key, request_body)
  from_branch = request_body['object_attributes']['target_branch']
  to_branch = request_body['object_attributes']['source_branch']
  project_id = request_body['object_attributes']['target_project_id']

  params = { private_token: api_key, from: from_branch, to: to_branch }
  url = "#{gitlab_server}/api/v3/projects/#{project_id}/repository/compare"
  changelog = JSON.parse(RestClient::Request.execute(:method => :get, :url => url, :headers => { params: params }))
  changelog = (changelog['commits'] || []).map { |commit| commit['message'] }
  return 'Major' if changelog.any? { |msg| msg.include? '#major' }
  return 'Minor' if changelog.any? { |msg| msg.include? '#minor' }
  return 'Patch' if changelog.any? { |msg| msg.include? '#patch' }
end
```

## Pro tips

You will need to do some extra work to make this work on updates.
For updates you will need pull the current labels and merge them
where appropriate. This is necessary to update the labels when a
subsequent commit to the MR takes it from a `#patch` to a `#minor`
or `#major`.

You should thread your webrick server so the processing of the updating
of incoming requests is in an different thread than the accepting of
webhooks from GitLab. If you don’t do multi-thread you may run into
issues where GitLab resends the webhooks because of a timeout. The
default timeout in GitLab is [10 seconds][timeout]. Simple threading with
[rubythread][ruby] and a [queue] should be sufficient.

Thanks to my colleague [Cameron McAvoy][cam] who added the label processing
to the original webhook server I wrote.

----

This post was [originally published][post] by Brian O'Connell himself.
{: .note}

<!-- 
original cover photo: http://www.freeimages.com/photo/pharmacy-sticker-box-1509293
license: http://www.freeimages.com/license
-->

<!-- identifiers -->

[@boc_tothefuture]: https://twitter.com/boc_tothefuture
[@GitLab]: https://twitter.com/gitlab
[@shochdoerfer]: https://twitter.com/shochdoerfer
[cam]: https://www.linkedin.com/in/cameron-mcavoy-7515a35b
[doc-api]: http://docs.gitlab.com/ce/api/
[doc-labels]: http://docs.gitlab.com/ee/user/project/labels.html
[doc-webhooks]: https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/web_hooks/web_hooks.md
[post-1]: /2016/08/17/using-gitlab-labels/
[post]: http://infrastructuredevops.com/08-04-2016/automated-gitlab-labels.html
[queue]: http://ruby-doc.org/core-2.2.0/Queue.html
[ru-cook]: https://github.com/chef-cookbooks/runit
[ruby]: http://ruby-doc.org/core-2.2.0/Thread.html
[runit]: http://smarden.org/runit/
[semver]: http://semver.org/
[thor]: https://github.com/RiotGamesMinions/thor-scmversion
[timeout]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/212/diffs#3e4fceb8f7271d481d5d56c4a5de142c30ca8301_78_78
[webrick]: https://en.wikipedia.org/wiki/WEBrick
