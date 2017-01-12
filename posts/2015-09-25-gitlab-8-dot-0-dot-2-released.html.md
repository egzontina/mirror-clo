---
title: "GitLab 8.0.2 Released"
date: 2015-09-25
author: GitLab
author_twitter: gitlab
---

Today we are releasing version 8.0.2 for Community Edition (CE) and Enterprise
Edition (EE).

It includes the following fixes:

- **CE/EE**: Fix default avatar not rendering in network graph
- **CE/EE**: Skip check_initd_configured_correctly on omnibus installs
- **CE/EE**: Prevent double-prefixing of help page paths
- **CE/EE**: Clarify confirmation text on user deletion
- **CE/EE**: Make commit graphs responsive to window width changes
- **CE/EE**: Fix LDAP attribute mapping
- **CE/EE**: Remove git refs used internally by GitLab from network graph
- **CE/EE**: Fix Reply by email for non-UTF-8 messages
- **CE/EE**: Add option to use StartTLS with Reply by email IMAP server

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
