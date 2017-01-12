---
title: "GitLab 7.5.3 Release"
date: 2014-12-05
categories: release
author: Job van der Voort
---

Today we release GitLab 7.5.3 CE and EE.

GitLab 7.5.3 updates Rugged to 0.21.2 to solve [issues](https://github.com/libgit2/rugged/issues/431) with 'finding too many commits'.
This issue could cause the PostReceive job triggered by a `git push` to take a very long time and consume a lot of memory.

For GitLab Enterprise Edition, 7.5.3 additionally fixes 'Redis::InheritedError',
which caused problems when creating new groups or projects in GitLab 7.5.0-7.5.2 Enterprise Edition.


<!-- more -->

## Upgrading

Omnibus-gitlab packages for GitLab 7.5.3 (including GitLab CI 5.2.1) are [now available](https://about.gitlab.com/downloads/).

To upgrade a GitLab installation from source please use the
[upgrader](http://doc.gitlab.com/ce/update/upgrader.html) or the [patch update
guide](http://doc.gitlab.com/ce/update/patch_versions.html).

To upgrade a GitLab CI installation from source, please use the [upgrade guide](https://gitlab.com/gitlab-org/gitlab-ci/blob/master/doc/update/patch_versions.md).

## Enterprise Edition

Omnibus packages for GitLab Enterprise Edition 7.5.3 are available for subscribers [here](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/install/packages.md). For installations from source, use [this guide](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/update/patch_versions.md).

Interested in GitLab Enterprise Edition?
For an overview of feature exclusive to GitLab Enterprise Edition please have a look at the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.
