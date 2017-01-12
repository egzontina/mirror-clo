---
title: "GitLab 8.11.3 released"
author: Rubén Dávila
author_twitter: rdavila
categories: release
---

Today we are releasing version 8.11.3 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version resolves a number of regressions and bugs in the [recent 8.11
release](/2016/08/22/gitlab-8-11-released).

Please read on for more details.

<!-- more -->

- **EE:** [ES] Logging for indexer. ([!683])
- **EE:** Set the correct `GL_PROTOCOL` in the environment when rebasing. ([!691])
- **EE:** Fix missing EE-specific service parameters for Jenkins CI. ([!692])
- **EE:** [ES] Elastic workers should check settings each time when they are running. ([!693])
- **CE/EE:** Automatically expand hidden discussions when accessed via a permalink hash. ([!5585])
- **CE/EE:** Handle non-UTF-8 conflicts gracefully. ([!5961])
- **CE/EE:** Fix enormous IE11 fork button. ([!5982])
- **CE/EE:** Handle unavailable system info. ([!5989])
- **CE/EE:** Label list shows all issues (opened or closed) with that label. ([!5991])
- **CE/EE:** Fix external issue tracker "Issues" link leading to 404s. ([!6006])
- **CE/EE:** Use new image for Issue Board page. ([!6013])
- **CE/EE:** Handle conflict edge cases after push. ([!6017])
- **CE/EE:** Fix wrong Koding link. ([!6030])
- **Omnibus GitLab:** Make `docutils` work with Python3 to restore `.RST` rendering. ([!968])

[!5585]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5585
[!5961]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5961
[!5982]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5982
[!5989]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5989
[!5991]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5991
[!6006]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6006
[!6013]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6013
[!6017]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6017
[!6030]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6030

[!683]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/683
[!691]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/691
[!692]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/692
[!693]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/693

[!968]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/968

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
