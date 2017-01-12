---
title: "GitLab 8.3.2 Released"
date: 2015-12-29
author: GitLab
author_twitter: gitlab
---

Today we are releasing version 8.3.2 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

It includes the following changes:

- **CE/EE:** Add support for Google reCAPTCHA in user registration ([#2216],
  [#2231])
- **CE/EE:** Disable `--follow` in `git log` to avoid loading duplicate commit
  data during infinite scroll ([#2210])

[#2210]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2210
[#2216]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2216
[#2231]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2231

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
