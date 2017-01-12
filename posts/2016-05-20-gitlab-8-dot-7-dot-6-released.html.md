---
title: "GitLab 8.7.6 Released"
comments: true
author: GitLab
author_twitter: gitlab
---

Today we are releasing version 8.7.6 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

It includes the following fixes:

- **EE:** Bump GitLab Pages to 0.2.4 to fix Content-Type for predefined 404
  ([!394]).
- **CE/EE:** Fix links on wiki pages for relative url setups ([!4131]).
- **CE/EE:** Fix import from GitLab.com to a private instance failure ([!4181]).
- **CE/EE:** Fix external imports not finding the import data ([!4106]).

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

[!394]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/394
[!4131]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4131
[!4181]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4181
[!4106]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4106
