---
title: "GitLab 8.12.6 released"
author: Stan Hu
author_twitter: stanhu
categories: release
date: 2016-10-12 02:35
---

Today we are releasing version 8.12.6 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

Version 8.12.6 contains a fix for the mail_room package not being included in
the package. This update is only necessary for users who use mail_room for
Reply by email.

Please read on for more details.

<!-- more -->

- **CE/EE:** Update mail_room to 0.8.1 in Gemfile.lock ([!6814])

[!6814]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6814

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
