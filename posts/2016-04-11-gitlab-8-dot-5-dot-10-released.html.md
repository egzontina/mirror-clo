---
title: "GitLab 8.5.10, 8.4.8, and 8.3.7 Released"
date: 2016-04-11 17:05
author: GitLab
author_twitter: gitlab
---

Earlier today we [released version 8.6.5][8-6-5] for GitLab Community Edition
(CE) and Enterprise Edition (EE).

We've backported the Two-factor Authentication security fix mentioned in that
release post to previous months' releases, and are releasing versions 8.5.10,
8.4.8, and 8.3.7.

[8-6-5]: /2016/04/11/gitlab-8-dot-6-dot-5-released/

<!-- more -->

- **CE/EE:** Prevent Two-factor Authentication spoofing

## Two-factor Authentication spoofing

[Jobert Abma](https://twitter.com/jobertabma) of [HackerOne](https://hackerone.com/jobert)
alerted us to a [security vulnerability] related to the two-factor authentication
(2FA) method used in GitLab CE and EE.

It was possible for an attacker to bypass password authentication of users that
have 2FA enabled, and consequently sign in as a different user without knowing
their password, if he could guess the user's current six-digit 2FA validation
code.

It was also possible to enumerate users and check if they have 2FA enabled,
because GitLab responded with a different error for each case.

[security vulnerability]: https://gitlab.com/gitlab-org/gitlab-ce/issues/14900

## Upgrade barometer

This version does not include any new migrations, and should not require
any downtime.

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
