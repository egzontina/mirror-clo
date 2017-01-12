---
title: "GitLab 8.5.4 Released"
date: 2016-03-04 15:00
author: GitLab
author_twitter: gitlab
filename: 2016-03-04-gitlab-8-dot-5-dot-4-released.markdown
---

Today we are releasing version 8.5.4 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version includes one important fix for GitLab Enterprise Edition when
Elasticsearch is enabled, as well as a minor fix for GitLab Community Edition.

Read on for all the details!

<!-- more -->

- **EE:** Fix a Notes exposure in Elasticsearch results
- **CE/EE:** Do not cache requests for badges (including builds badge) ([!3086])

[!3086]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3086

## Upgrade barometer

This version does not include any new migrations, and should not require 
any downtime.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

## Updating

To update, check out our [update page](https://about.gitlab.com/update).

## Enterprise Edition

Interested in GitLab Enterprise Edition? Check out the [features exclusive to
EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](https://about.gitlab.com/pricing/).
No time to upgrade GitLab yourself? Subscribers receive upgrade and installation
services.
