---
title: "GitLab 8.5.5 Released"
date: 2016-03-10 17:00
author: GitLab
author_twitter: gitlab
filename: 2016-03-10-gitlab-8-dot-5-dot-5-released.markdown
---

Today we are releasing version 8.5.5 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version includes a new GitLab Geo feature and fixes, several minor EE fixes
as well as fixes for Todos and project lists.

Read on for all the details!

<!-- more -->

- **EE:** GitLab Geo: Repository synchronization between primary and secondary nodes ([!179])
- **EE:** Refactor user documentation for GitLab Pages ([!212])
- **EE:** Fix importing projects from GitHub Enterprise Edition ([!219])
- **EE:** Fix syntax error in init file ([!223])
- **EE:** GitLab Geo: Improve GeoNodes Admin screen ([!251])
- **EE:** GitLab Geo: Avoid locking yourself out when adding a GeoNode ([!252])
- **EE:** Only show group member roles if explicitly requested ([!3044])
- **CE/EE:** Ensure removing a project removes associated Todo entries ([!3141])
- **CE/EE:** Prevent a 500 error in Todos when author was removed ([!3141])
- **CE/EE:** Fix pagination for filtered dashboard and explore pages ([!3149])
- **CE/EE:** Fix "Show all" link behavior on profile page ([!3159])
- **Omnibus GitLab:** Add ldap_sync_time global configuration as the EE is still supporting it ([!679])

[!179]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/179
[!212]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/212
[!219]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/219
[!223]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/223
[!251]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/251
[!252]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/252
[!3044]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3044
[!3141]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3141
[!3149]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3149
[!3159]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3159
[!679]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/679

## Upgrade barometer

This release includes one minor database migration for CE and two minor
migrations for EE. All the migrations can be run without causing any downtime.

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
