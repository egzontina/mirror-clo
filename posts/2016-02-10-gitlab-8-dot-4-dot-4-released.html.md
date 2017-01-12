---
title: "GitLab 8.4.4 Released"
date: 2016-02-10
author: GitLab
author_twitter: gitlab
filename: 2016-02-10-gitlab-8-dot-4-dot-4-released.markdown
---

Today we are releasing version 8.4.4 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version includes more fixes for Elasticsearch, a re-introduction of the
"Send email to users" administration link that was mistakenly removed, and
addresses one potential security issue concerning public CI build logs.

Read on for all the details!

<!-- more -->

- **CE/EE:** Update omniauth-saml gem to 1.4.2 ([!2684])
- **CE/EE:** Prevent long-running backup tasks from timing out the database
  connection ([!2757])
- **CE/EE:** Add a Project setting to allow guests to view build logs (defaults
  to true)
- **EE:** Re-introduce "Send email to users" link in Admin area ([!161])
- **EE:** Fix category values for Jenkins and JenkinsDeprecated services ([!163])
- **EE:** Fix Elasticsearch indexing for newly added Snippets ([!165])
- **EE:** Make Elasticsearch indexer more stable ([!167])
- **EE:** Update gitlab-elasticsearch-git to 0.0.10 ([!170])

[!161]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/161
[!163]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/163
[!165]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/165
[!167]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/167
[!170]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/170
[!2684]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2684
[!2757]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2757
[!2761]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2761

## Possible information leak via GitLab CI logs

In GitLab 8.3, we made CI build logs share the visibility level of their parent
project for the sake of simplicity. However, we failed to properly document this
change and some users may have been surprised by previously-hidden build logs
suddenly becoming visible, possibly exposing sensitive information such as
environment variables.

We've addressed this in 8.4.4 by adding a project-level setting to allow anyone
(including guests) to access the build logs for a public or internal project.
This setting is enabled by default but can be disabled for additional security.
Build logs in private projects will still be visible only to members of that
project.

## Elasticsearch Snippet indexing

If you enabled Elasticsearch indexing prior to this version, Snippets added
since that time may not be properly indexed.

To ensure those Snippets are properly indexed, run one of the following commands:

```sh
# For Omnibus installations
sudo gitlab-rails runner "Snippet.import"

# For source installations
cd /home/git/gitlab && sudo -u git -H bundle exec rails runner "Snippet.import"
```

## `ruby-saml` update

This release includes an update to the `omniauth-saml` gem (which itself
includes an update to the `ruby-saml` gem) in order to properly allow SAML
responses that did not include an X.509 certificate in the response body; it now
properly fetches the certificate indicated in the settings and uses that one to
validate the response.

## Upgrade barometer

This release includes one minor database migration which can be run without
causing any downtime.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

## Updating

To update, check out our [update page](https://about.gitlab.com/update).

## Enterprise Edition

Interested in GitLab Enterprise Edition? Check out the [features exclusive to
EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself? Subscribers receive upgrade and installation
services.
