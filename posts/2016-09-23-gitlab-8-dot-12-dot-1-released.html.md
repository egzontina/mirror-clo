---
title: "GitLab 8.12.1 released"
author: Rubén Dávila
author_twitter: rdavila
categories: release
---

Today we are releasing version 8.12.1 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version resolves a number of regressions and bugs in the [recent 8.12
release](/2016/09/22/gitlab-8-12-released).

Please read on for more details.

<!-- more -->

- **EE:** Prevent secrets being pushed into repository. ([!731])
- **EE:** Fix typo in protected_branches usage data. ([!758])
- **CE/EE:** Fixed search dropdown labels not displaying.([!6277])
- **CE/EE:** Fix a memory leak in HTML::Pipeline::SanitizationFilter::WHITELIST. ([!6456])
- **CE/EE:** Makes Cycle analytics mobile friendly. ([!6482])
- **CE/EE:** Fix Cycle Analytics landing widget state and improve state management in Vue. ([!6492])
- **CE/EE:** Add link to broadcast messages docs. ([!6495])
- **Omnibus:** Fix backslash issues in sv/gitlab-workhorse/run. ([!1005])

[!731]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/731
[!758]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/758

[!6456]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6456
[!6495]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6495
[!6482]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6482
[!6492]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6492
[!6277]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6277

[!1005]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/1005

## Upgrade barometer

This version has no migrations and should not require any downtime.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

## Updating

To update, check out our [update page](https://about.gitlab.com/update/).

## Enterprise Edition

Interested in GitLab Enterprise Edition? Check out the [features exclusive to
EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](https://about.gitlab.com/pricing/).
No time to upgrade GitLab yourself? Subscribers receive upgrade and installation
services.
