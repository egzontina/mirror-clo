---
title: "GitLab 8.5.8, 8.4.6, 8.3.5, and 8.2.4 Released"
date: 2016-03-21 14:15:00 UTC
author: GitLab
author_twitter: gitlab
---

Last Friday, we released versions 8.5.8, 8.4.6, 8.3.5, and 8.2.4 for GitLab
Community Edition (CE) and Enterprise Edition (EE).

These versions raise the minimum required Git version to 2.7.4 ([!692]) to
address the recent
[Git vulnerabilities](https://about.gitlab.com/2016/03/18/what-git-vulnerabilities-cve-2016-2324-and-2315-mean-for-gitlab-and-you/).
The Omnibus packages have been updated to include this new version.

<!-- more -->

GitLab Geo documentation ([!236]) was also added in 8.5.8.

[!236]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/236
[!692]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/692

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
