---
title: "GitLab 8.1.3 Released"
date: 2015-11-06
author: GitLab
author_twitter: gitlab
---

Today we are releasing version 8.1.3 for Community Edition (CE) and Enterprise
Edition (EE).

It includes the following fixes:

- **CE:** Add support for Facebook OAuth authentication
- **CE:** Use issue editor as cross reference comment author when issue is
  edited with a new mention
- **CE:** Spread out runner contacted_at updates
- **CE:** Force-update refs/merge-requests/X/head upon a push to the source
  branch of a merge request
- **EE:** Fix "Rebase onto master"

<!-- more -->

## Upgrade barometer

When upgrading to 8.1.3 using Omnibus packages, downtime is required because of
additions to the PostgreSQL configuration which will cause a database restart.

This version does not include any new migrations, and installations from source
should not require any downtime.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

## Updating

To update, check out our [update page](https://about.gitlab.com/update).

## Enterprise Edition

Interested in GitLab Enterprise Edition?
Check out the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/pricing).
No time to upgrade GitLab yourself?
Subscribers receive upgrade and installation services.
