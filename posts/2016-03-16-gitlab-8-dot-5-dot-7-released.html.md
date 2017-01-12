---
title: "GitLab 8.5.7 Released"
date: 2016-03-16 00:20
author: GitLab
author_twitter: gitlab
filename: 2016-03-16-gitlab-8-dot-5-dot-7-released.markdown
---

Today we are releasing version 8.5.7 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version raises the minimum required Git version to 2.7.3 to address the
recent [remote code execution](http://seclists.org/oss-sec/2016/q1/645)
vulnerability. The Omnibus packages have been updated to include this new
version.

<!-- more -->

- **Omnibus:** Update Git to 2.7.3 ([!687])
- **CE/EE:** Bump Git version requirement to 2.7.3 ([!3240])

[!687]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/687
[!3240]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3240

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
