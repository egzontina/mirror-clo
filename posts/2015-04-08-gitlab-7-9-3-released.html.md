---
title: "GitLab 7.9.3 released"
date: 2015-04-08
categories: release
author: Patricio Cano
---

Today we release GitLab 7.9.3 CE, EE and GitLab CI 7.9.3.


GitLab 7.9.3 EE fixes:

  - Fixes a link in LDAP groups page that linked to the group's member page and the redirect URL after clearing
  the LDAP permission cache.

Community Edition 7.9.3 and GitLab CI 7.9.3 contain no changes.

<!-- more -->

## Upgrade barometer

Upgrading from GitLab 7.9.2 requires no downtime as this release contains no migrations.

## Upgrading

Omnibus-gitlab packages for GitLab 7.9.3 are not necessary, since the code for CE hasn't changed.

To upgrade a GitLab installation from source please use the
[upgrader](http://doc.gitlab.com/ce/update/upgrader.html) or the [patch update
guide](http://doc.gitlab.com/ce/update/patch_versions.html).

To upgrade a GitLab CI installation from source, please use the [upgrade guide](https://gitlab.com/gitlab-org/gitlab-ci/blob/master/doc/update/patch_versions.md).

## Enterprise Edition

Omnibus packages for GitLab Enterprise Edition 7.9.3 are available for subscribers [here](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/install/packages.md).
For installations from source, use [this guide](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/update/patch_versions.md).

**Interested in GitLab Enterprise Edition?**
For an overview of feature exclusive to GitLab Enterprise Edition please have a look at the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).

**No time to upgrade GitLab yourself?**
A subscription also entitles to our upgrade and installation services.
