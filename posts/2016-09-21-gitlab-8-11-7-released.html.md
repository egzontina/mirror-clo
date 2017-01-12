---
title: "GitLab 8.11.7, 8.10.10 and 8.9.10 released"
author: Rémy Coutable
author_twitter: rymai
categories: security release
date: 2016-09-21 09:30
---

Today we are releasing versions 8.11.7, 8.10.10 and 8.9.10 for GitLab Community
Edition (CE) and Enterprise Edition (EE).

Version 8.11.7 contains a security fix for GitLab, plus fixes for minor
regressions. Version 8.10.10 and 8.9.10 only contain the security fix.

Please read on for more details.

<!-- more -->

- **CE/EE:** Avoid conflict with admin labels when importing GitHub labels. ([!6158])
- **CE/EE:** Restores `fieldName` to allow only string values in `gl_dropdown.js`. ([!6234])
- **CE/EE:** Allow the Rails cookie to be used for API authentication. ([#18302])

- **EE:** Refactor Protected Branches dropdown. ([!687])
- **EE:** Fix mirrored projects allowing empty import urls. ([!700])

[!6158]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6158
[!6234]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6234

[!687]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/687
[!700]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/700

[#18302]: https://gitlab.com/gitlab-org/gitlab-ce/issues/18302

## Information disclosure through `gon.private_token` JavaScript variable

The private user token was available through the `gon.private_token` JavaScript
variable, leading to a potential security risk since it could be stolen through
XSS or other attacks.
See [the issue][#18302] for more information.

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
