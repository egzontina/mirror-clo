---
title: "GitLab 7.8.1 Released"
date: 2015-02-24
categories: release
author: Marin Jankovski
author_twitter: maxlazio
---

Today we release GitLab 7.8.1 CE, EE and GitLab CI 7.8.1.


GitLab 7.8.1 CE fixes:

- Fix run of custom post receive hooks
- Fix migration that caused issues when upgrading to version 7.8 from versions prior to 7.3
- Fix the warning for LDAP users about need to set password
- Fix avatars which were not shown for non logged in users
- Fix urls for the issues when relative url was enabled

In addition to the fixes in 7.8.1 CE, Enterprise Edition 7.8.1 contains the following fix:

- Fix the custom logo and logo upload

<!-- more -->

## Upgrading

Omnibus-gitlab packages for GitLab 7.8.1 are [now available](https://about.gitlab.com/downloads/).

To upgrade a GitLab installation from source please use the
[upgrader](http://doc.gitlab.com/ce/update/upgrader.html) or the [patch update
guide](http://doc.gitlab.com/ce/update/patch_versions.html).

To upgrade a GitLab CI installation from source, please use the [upgrade guide](https://gitlab.com/gitlab-org/gitlab-ci/blob/master/doc/update/patch_versions.md).

## Enterprise Edition

Omnibus packages for GitLab Enterprise Edition 7.8.1 are available for subscribers [here](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/install/packages.md). For installations from source, use [this guide](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/update/patch_versions.md).

Interested in GitLab Enterprise Edition?
For an overview of feature exclusive to GitLab Enterprise Edition please have a look at the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.
