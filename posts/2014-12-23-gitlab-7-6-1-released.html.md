---
title: "GitLab 7.6.1 Release"
date: 2014-12-23
categories: release
author: Job van der Voort
---

Today we release GitLab 7.6.1 CE and 7.6.2 EE.

This release fixes a problem with the LDAP migrations and MySQL when upgrading.
If you've already upgraded to GitLab 7.6 without problems, there is no need
to upgrade to 7.6.1 CE or 7.6.2 EE.

If you've experienced a failed migration you can run this release to correct it.
If it exists you will have to manually remove the `identities` database table before upgrading.

<!-- more -->

## Upgrading

Omnibus-gitlab packages for GitLab 7.6.1 (including GitLab CI 5.3.0) are [now available](https://about.gitlab.com/downloads/).

To upgrade a GitLab installation from source please use the
[upgrader](http://doc.gitlab.com/ce/update/upgrader.html) or the [patch update
guide](http://doc.gitlab.com/ce/update/patch_versions.html).

To upgrade a GitLab CI installation from source, please use the [upgrade guide](https://gitlab.com/gitlab-org/gitlab-ci/blob/master/doc/update/patch_versions.md).

## Enterprise Edition

_Note: we skipped GitLab EE 7.6.1. If you've upgraded to 7.6.0 EE without issues,
there is no need to update to 7.6.2 EE._

Omnibus packages for GitLab Enterprise Edition 7.6.2 are available for subscribers [here](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/install/packages.md). For installations from source, use [this guide](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/update/patch_versions.md).

Interested in GitLab Enterprise Edition?
For an overview of feature exclusive to GitLab Enterprise Edition please have a look at the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.
