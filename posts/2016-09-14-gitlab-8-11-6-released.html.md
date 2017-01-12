---
title: "GitLab 8.11.6, 8.10.9 and 8.9.9 released"
author: Rubén Dávila
author_twitter: rdavila
categories: security release
date: 2016-09-14 17:00
---

Today we are releasing versions 8.11.6, 8.10.9 and 8.9.9 for GitLab Community
Edition (CE) and Enterprise Edition (EE).

Version 8.11.6 contains two security fixes for GitLab, plus fixes for minor
regressions. Version 8.10.9 only contains the two security fixes, while version
8.9.9 contains only one.

Please read on for more details.

<!-- more -->

- **CE/EE:** Fix unnecessary horizontal scroll area in pipeline visualizations. ([!6005])
- **CE/EE:** Fix merge conflict size limit. ([!6052])
- **CE/EE:** Fix an error where we were unable to create a CommitStatus for running state. ([!6107])
- **CE/EE:** Optimize discussion notes resolving and unresolving. ([!6141])
- **CE/EE:** Fix GitLab import button. ([!6167])
- **CE/EE:** Restore SSH Key title auto-population behavior. ([!6186])
- **CE/EE:** Fix DB schema to match latest migration. ([!6256])
- **CE/EE:** Exclude some pending or inactivated rows in Member scopes. ([#21650])

- **EE:** Exclude blocked users from potential MR approvers (`8.11.6` & `8.10.9` only). ([#976])

- **Omnibus GitLab:** Fix registry build by enabling vendor feature. ([!991])

[!6005]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6005
[!6052]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6052
[!6107]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6107
[!6141]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6141
[!6167]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6167
[!6186]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6186
[!6256]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6256

[#21650]: https://gitlab.com/gitlab-org/gitlab-ce/issues/21650
[#976]: https://gitlab.com/gitlab-org/gitlab-ee/issues/976

[!991]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/991

## Information disclosure through "access requested" emails

Blocked owners & masters of a group or project would still receive notification
emails for access requests, leaking the requesters's name to the blocked user.
See [the issue][#21650] for more information.

## Upgrade barometer

This version has no migrations and should not require any downtime.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

## Updating

To update, check out our [update page](https://about.gitlab.com/update/).

## Sign up for security notices

Want to be alerted to new security patches as soon as they're available? Sign up
for our [Security Newsletter](https://about.gitlab.com/contact/).

## Enterprise Edition

Interested in GitLab Enterprise Edition? Check out the [features exclusive to
EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](https://about.gitlab.com/pricing/).
No time to upgrade GitLab yourself? Subscribers receive upgrade and installation
services.
