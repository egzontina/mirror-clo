---
title: "GitLab 7.14.1 released"
date: 2015-08-25
author: GitLab
author_twitter: gitlab
---

Today we are releasing version 7.14.1 for GitLab Community Edition (CE),
Enterprise Edition (EE), and CI.

It includes the following fixes:

- **CE:** Only include base URL in OmniAuth full_host parameter
- **CE:** Fix Error 500 in API when accessing a group that has an avatar
- **CE:** Fix "Reload with full diff" URL button in compare branch view
- **CE:** Improve abuse reports management from admin area
- **EE:** Fix sign in form when just Kerberos is enabled
- **CI:** Fix "skipped" svg image
- **CI:** Fix commit ordering

<!-- more -->

## Upgrade barometer

This version does not include any new migrations, and should not require any
downtime.

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
