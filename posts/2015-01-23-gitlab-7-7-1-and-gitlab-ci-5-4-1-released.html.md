---
title: "GitLab 7.7.1 and GitLab CI 5.4.1 Released"
date: 2015-01-23
categories: release
author: Dmitriy Zaporozhets
---

Today we release GitLab 7.7.1 (both CE and EE) and GitLab CI 5.4.1.

GitLab 7.7.1 brings three fixes:

- Improve @mention autocomplete performance
- Show setup instructions for GitHub import if it is disabled
- Allow use of http for OAuth applications

GitLab CI 5.4.1 fixes several bugs:

- Fix 500 on builds page if a build has no jobs
- Truncate project token from build trace
- Allow users with access to a project see the build trace

<!-- more -->

## Upgrading

Omnibus-gitlab packages for GitLab 7.7.1 and GitLab CI 5.4.1 are [now available](https://about.gitlab.com/downloads/).

To upgrade a GitLab installation from source please use the
[upgrader](http://doc.gitlab.com/ce/update/upgrader.html) or the [patch update
guide](http://doc.gitlab.com/ce/update/patch_versions.html).

To upgrade a GitLab CI installation from source, please use the [upgrade guide](https://gitlab.com/gitlab-org/gitlab-ci/blob/master/doc/update/patch_versions.md).

## Enterprise Edition

Omnibus packages for GitLab Enterprise Edition 7.7.1 and GitLab CI 5.4.1 are available for subscribers [here](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/install/packages.md). For installations from source, use [this guide](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/update/patch_versions.md).

Interested in GitLab Enterprise Edition?
For an overview of feature exclusive to GitLab Enterprise Edition please have a look at the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.
