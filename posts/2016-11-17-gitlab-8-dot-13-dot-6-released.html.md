---
title: "GitLab 8.13.6 released"
author: Rémy Coutable
author_twitter: rymai
categories: release
---

Today we are releasing version 8.13.6 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version resolves a number of regressions and bugs in the [recent 8.13
release](/2016/10/22/gitlab-8-13-released).

Please read on for more details.

<!-- more -->

- **CE/EE:** Omniauth auto link LDAP user falls back to find by DN when user cannot be found by UID. ([!7002])
- **CE/EE:** Fix Milestone dropdown not stay selected for `Upcoming` and `No Milestone` option. ([!7117])
- **CE/EE:** Fix relative links in Markdown wiki when displayed in "Project" tab. ([!7218])
- **CE/EE:** Fix project "Visibility Level" selector not using default values. ([!7264])
- **CE/EE:** Fix no "Register" tab if LDAP auth is enabled. ([!7274])
- **CE/EE:** Clicking "force remove source branch" label now toggles the checkbox again. ([!7356])
- **CE/EE:** Fix cache for commit status in commits list to respect branches. ([!7372])
- **CE/EE:** Fix issue causing labels not to appear in sidebar on MR page. ([!7416])
- **CE/EE:** Limit labels returned for a specific project as an administrator. ([!7496])
- **CE/EE:** Allow commit note to be visible if repo is visible. ([!7504])

- **EE:** Disable retries for remote mirror update worker. ([!848])
- **EE:** Geo: Fix cache clearing on secondary Geo nodes. ([!869])
- **EE:** Geo: Fix a problem that prevented git cloning from secondary node. ([!873])

[!7002]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7002
[!7117]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7117
[!7218]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7218
[!7264]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7264
[!7274]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7274
[!7356]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7356
[!7372]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7372
[!7416]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7416
[!7496]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7496
[!7504]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7504

[!848]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/848
[!869]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/869
[!873]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/873

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
