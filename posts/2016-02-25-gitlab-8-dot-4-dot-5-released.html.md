---
title: "GitLab 8.4.5 Released"
date: 2016-02-25
author: GitLab
author_twitter: gitlab
filename: 2016-02-25-gitlab-8-dot-4-dot-5-released.markdown
---

Today we are releasing version 8.4.5 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

Note that this is a patch for the previous major release (8.4), and not the
latest (8.5). An 8.5.2 patch is expected soon!

This patch contains only one change: LDAP groups will now be updated
asynchronously.

<!-- more -->

- **EE:** Update LDAP groups asynchronously ([!190])

[!190]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/190

## Upgrade barometer

This release does not include any migrations, so no downtime should be
necessary.

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
