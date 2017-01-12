---
title: "GitLab 8.8.1 Released"
comments: true
author: GitLab
author_twitter: gitlab
---

Today we are releasing version 8.8.1 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

It includes the following fixes:

- **CE/EE:** Allow anonymous user to access pipelines ([!4233])
- **CE/EE:** Fix MySQL compatibility in zero downtime migration helpers ([!4239])

<!-- more -->

## Upgrade barometer

This version does not include any new migrations, and should not require any
downtime.

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

[!4233]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4233
[!4239]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4239
