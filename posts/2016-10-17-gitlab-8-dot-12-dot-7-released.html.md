---
title: "GitLab 8.12.7 released"
author: Rémy Coutable
author_twitter: rymai
categories: release
---

Today we are releasing version 8.12.7 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version resolves a number of regressions and bugs in the [recent 8.12
release](/2016/09/22/gitlab-8-12-released).

Please read on for more details.

<!-- more -->

- **CE/EE:** Prevent running `GfmAutocomplete` setup for each diff note. ([!6569])
- **CE/EE:** Fix long commit messages overflow viewport in file tree. ([!6573])
- **CE/EE:** Use `gitlab-markup` gem instead of `github-markup` to fix `.rst` file rendering. ([!6659])
- **CE/EE:** Prevent flash alert text from being obscured when container is fluid. ([!6694])
- **CE/EE:** Fix due date being displayed as `NaN` in Safari. ([!6797])
- **CE/EE:** Fix JS bug with select2 because of missing `data-field` attribute in select box. ([!6812])
- **CE/EE:** Do not alter `force_remove_source_branch` options on MergeRequest unless specified. ([!6817])
- **CE/EE:** Fix GFM autocomplete setup being called several times. ([!6840])
- **CE/EE:** Handle case where deployment ref no longer exists. ([!6855])

- **Omnibus GitLab:** Use forked `gitlab-markup` gem. ([!1015])

[!6569]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6569
[!6573]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6573
[!6659]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6659
[!6694]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6694
[!6797]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6797
[!6812]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6812
[!6817]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6817
[!6840]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6840
[!6855]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6855

[!1015]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/1015

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
