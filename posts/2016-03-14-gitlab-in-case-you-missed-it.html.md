---
title: "GitLab: In case you missed it"
date: 2016-03-14
author: Ivan Nemytchenko
author_twitter: inemation
image_title: '/images/unsplash/key-concepts.jpg'
---

I've recently joined GitLab as a Developer Advocate. 
Part of my role will be traveling to community events where I hope we'll meet in person. 
I'm also an experienced Ruby developer. 
As a rubyist, naturally, I've heard about GitLab and even used it couple of times.

The first two weeks working with GitLab have been full of pleasant surprises and dispelled delusions. 
If you haven't been following GitLab for the last two years, this post is for you.

<!--more-->

## GitLab.com

You don't have to download and install GitLab nowadays. 
You can simply [sign up for GitLab.com](https://gitlab.com/users/sign_in) and host your own repositories. 
Even the private ones. 
Yes, for free and without any restrictions. 
No, there is no catch.

It should be noted that repositories are actually called "projects". 

And that is not the only thing that catches your eye at first. 
As it turns out, the terminology is justified.

## The terminology 

These aren't just fancy terms to stand out from the crowd. 
I strongly recommend reading the article about [GitLab, GitHub and Bitbucket and terms comparison](https://about.gitlab.com/2016/01/27/comparing-terms-gitlab-github-bitbucket/), if you wish to sort out the details. 
I'd like to bring up the "Merge requests" topic, as it's the most controversial.

My initial reaction, naturally, was rejection. Most of us are accustomed to
"Pull requests", so what's the big idea?
But then I remembered that the title "Pull request" never did make perfect
sense to me because closing a pull request actually does branch merging.

As it turns out, there is a command [`git request-pull`](https://git-scm.com/docs/git-request-pull),
hence the feature title.

Pull requests have nothing in common with this git command. So, technically the correct name is "merge request". 
[Learn more](https://about.gitlab.com/2016/01/27/comparing-terms-gitlab-github-bitbucket/) on terminology differences, if you're interested.

The terminology was just a part of the deal. 
When reading the documentation, I discovered something called "omnibus" and
found some mysterious "runners" and "shared runners" in the settings. 
But first things first. 
Runners are connected to CI. 
Omnibus is related to GitLab installation on your own server.

## Continuous Integration (CI)

Continuous Integration is a best practice in software development.
For example, a CI server runs your tests every time you push changes to the repository.

A lot of companies have a separate CI service but in GitLab, [CI is embedded](http://docs.gitlab.com/ce/ci/).

If you had to manually connect two services before, it just works on its own in GitLab.
Though you can still use other continuous integration services such as [Jenkins](http://doc.gitlab.com/ee/integration/jenkins.html).

And it works through runners.

## Runners

A runner is a virtual machine that runs your tests, builds your builds or generates static files for your websites. 
GitLab.com users are able to make use of a special [Shared Runners](http://doc.gitlab.com/ce/ci/quick_start/README.html#shared-runners) pool to simply make everything work. 

Since the pool is shared across all projects on GitLab.com, sometimes it can
take a while to wait for your project's build to be processed.

If you are not satisfied with the Shared runners performance, you can
[setup a runner](https://about.gitlab.com/2016/03/01/gitlab-runner-with-docker/)
on your own server and connect it to one or more projects.

Don't forget that you can install GitLab on your own server as well. 

## GitLab installation with Omnibus


In the past, GitLab was installed manually. 
Now you can install and update the service from packages thanks to Omnibus.
[Omnibus](http://doc.gitlab.com/omnibus) is a tool developed by Chef
that helps to create installation packages for complex software with a lot of
components for various platforms.

Any installation using Omnibus lasts for 2-6 minutes tops, depending on your server performance. 
This is what GitLab installation looks like on Ubuntu 14.04 using a relatively slow VPS with 2Gb running memory:
<script type="text/javascript" src="https://asciinema.org/a/39151.js" id="asciicast-39151" async></script>

Hint: in case you'd prefer not to mess with console installation and updates at
all, you can simply rent a GitLab server on [Githost.io](https://githost.io/)

Both Omnibus and built-in CI are just a portion of what is being done to make developers' jobs easier.
Let us review a few features.

## Small features that make a difference

### Merge when build succeeds

With GitLab, you don't have to wait for your build to turn green to finally merge the branch. 
You can simply ask GitLab to do that for you.

![Merge when build succeeds](/images/automerge.jpg)

### Publishing with GitLab Pages

GitLab Pages runs on top of the built-in CI.
Thanks to the feature, you can host websites created by any static site generators on GitLab.

Fork a repo from [GitLab examples](https://gitlab.com/groups/gitlab-examples?utf8=%E2%9C%93&filter_projects=pages-)
or figure out GitLab CI settings to forget all about the manual static generation.
You simply push your changes to the repository and GitLab generates and deploys everything on its own.

Custom CNAME and TLS [are supported](http://doc.gitlab.com/ee/pages/README.html#add-a-custom-domain-to-your-pages-website).

These kinds of features have become possible due to the synergy between system components.
There's much more coming.

## GitLab Direction

Please don't be surprised once a crashed build creates a TODO automatically or GitLab introduces built-in chat.

If you want to know where GitLab is heading, keep an eye on the [Direction page](https://about.gitlab.com/direction/).
This includes not only the short term objectives for the next release, but also the long-range vision.

* * * 

Hopefully, this article has helped you to fill in the gaps in understanding what GitLab is now. 
I'm planning to write two more articles: about migrating personal projects to GitLab and about contributing to GitLab.
Stay tuned and [follow me on Twitter](https://twitter.com/inemation).

I'm always happy to answer your questions in comments or personally.
Over the next several weeks I will be speaking at the following Ukrainian Ruby-meetups, where we can catch up:

- [Ruby Meditation, Kiev](https://www.facebook.com/events/406794219490854/) (March 18)
- [Pivorak, Lviv](https://www.facebook.com/pivorak/) (March 26)

## Join our webcast about GitLab CI.

I mentioned Gitlab CI a few times in this blog post. If you're interested,
we'll have a live webcast all about GitLab CI.

- Date: Thursday, April 14, 2016 
- Time: 5pm (17:00) UTC; 12pm EST; 9am PST 
- [Register here][webcast]

Can't make these times? Register anyway, and we'll send you a link to watch later.
[webcast]: http://page.gitlab.com/apr-2016-gitlab-intro-ci-webcast.html
