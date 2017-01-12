---
title: "GitLab 8.6.7, 8.5.11, 8.4.9, and 8.3.8 Released"
date: 2016-04-20 16:00
author: GitLab
author_twitter: gitlab
---

Today we are releasing versions 8.6.7, 8.5.11, 8.4.9, and 8.3.8 for GitLab
Community Edition (CE) and Enterprise Edition (EE).

Versions 8.3.8, 8.4.9, and 8.5.11 contain fixes for one persistent XSS
vulnerability and an information leak for private groups. Version 8.6.7 contains
both of those fixes as well as a fix for one additional persistent XSS
vulnerability that was only present in the 8.6 release.

Please read on for more details.

<!-- more -->

## Persistent XSS vulnerability in commit author emails

The contents of a user-supplied Git commit author or committer email were being
inserted into the page without proper escaping. [See the
issue](https://gitlab.com/gitlab-org/gitlab-ce/issues/15126) for more details.

Thanks to Teun Beijers for responsibly disclosing this issue to us.

## Persistent XSS vulnerability in label and milestone dropdowns

The contents of milestone and label titles were being inserted into the
Milestone and Label dropdowns without proper escaping. [See the
issue](https://gitlab.com/gitlab-org/gitlab-ce/issues/15389) for more details.

This vulnerability was only present in versions 8.6.0 through 8.6.6.

Thanks to [RonMurz](https://hackerone.com/ronmurz) on HackerOne for responsibly
disclosing this issue to us.

## Enumeration of private projects belonging to a group

[Jobert Abma](https://twitter.com/jobertabma) of [HackerOne](https://hackerone.com/jobert)
alerted us to a [security vulnerability] related to the "share project with
group" feature.

An unprivileged user was able to share a project with a group he didn't have
access to, and therefore gain partial access to that group, which opened
possibilities for further actions like listing private projects in that group.

[security vulnerability]: https://gitlab.com/gitlab-org/gitlab-ce/issues/15330

## Upgrade barometer

These versions do not include any new migrations, and should not require any
downtime.

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
services
