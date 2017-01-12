---
title: "GitLab 8.6.6 Released"
date: 2016-04-15 17:00
author: GitLab
author_twitter: gitlab
---

Today we are releasing version 8.6.6 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version includes a few bug fixes for both editions.

Read on for all the details!

<!-- more -->

- **EE:** Concat AD group recursive member results with regular member results. ([!333])
- **EE:** Fix LDAP group sync regression for groups with member value `uid=<username>`. ([!335])
- **EE:** Don't attempt to include too large diffs in e-mail-on-push messages. ([!338])
- **CE/EE:** Expire the exists cache before deletion to ensure project dir actually exists. ([!3413])
- **CE/EE:** Fix error on language detection when repository has no HEAD (e.g., master branch). ([!3654])
- **CE/EE:** Fix revoking of authorized OAuth applications. ([!3690])

[!333]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/333
[!335]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/335
[!338]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/338

[!3413]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3413
[!3654]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3654
[!3690]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3690

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

Access to GitLab Enterprise Edition is included with a [subscription](https://about.gitlab.com/pricing/).
No time to upgrade GitLab yourself? Subscribers receive upgrade and installation
services
