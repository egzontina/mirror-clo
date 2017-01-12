---
title: "GitLab 7.14.2 released"
date: 2015-09-09
author: GitLab
author_twitter: gitlab
---

Today we are releasing version 7.14.2 for Community Edition (CE), Enterprise
Edition (EE), and Continuous Integration (CI).

It includes the following fixes:

- **CE:** Fix `git blame` errors with ISO-encoded files
- **CE:** Handle broken symlinks in create-hooks
- **CE:** ***Security Fix*** Escape user-provided content in preserved Haml
  sections
- **EE:** Fix rebase before merge.
- **CI**: ~~Fix commits ordering when using PostgreSQL~~

***Update*** *(2015-09-10 20:30 UTC)*: The CI fix mentioned above was mistakenly
omitted and a [new version has been released](/2015/09/10/gitlab-7-dot-14-dot-3-released/)
to include it.

<!-- more -->

## Upgrade barometer

This version does not include any new migrations, and should not require any
downtime.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

This version includes required updates to external dependencies. Users
installing from source should be sure to follow the [update guide], particularly
the "[Update gitlab-shell]" and "[Install libs, migrations, etc.]" sections.

## Updating

To update, check out our [update page](https://about.gitlab.com/update).

## Enterprise Edition

Interested in GitLab Enterprise Edition?
Check out the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/pricing).
No time to upgrade GitLab yourself?
Subscribers receive upgrade and installation services.

[update guide]: https://gitlab.com/gitlab-org/gitlab-ce/blob/7-14-stable/doc/update/7.13-to-7.14.md
[Update gitlab-shell]: https://gitlab.com/gitlab-org/gitlab-ce/blob/7-14-stable/doc/update/7.13-to-7.14.md#4-update-gitlab-shell
[Install libs, migrations, etc.]: https://gitlab.com/gitlab-org/gitlab-ce/blob/7-14-stable/doc/update/7.13-to-7.14.md#5-install-libs-migrations-etc
