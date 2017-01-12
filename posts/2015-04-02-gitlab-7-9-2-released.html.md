---
title: "GitLab 7.9.2 Released"
date: 2015-04-02
categories: release
author: Marin Jankovski, Valery Sizov
---

Today we release GitLab CE, GitLab EE and GitLab CI 7.9.2.

This release only affects GitLab CI. If you do not use GitLab CI, you do not need to upgrade to GitLab 7.9.2.

Versions affected: GitLab CI 7.9.1

Versions fixed: GitLab CI 7.9.2

In 7.9.1 (previous release) we added a project setting option "Allow shared runners".

After upgrading to this version all existing CI projects have this option enabled, so that all projects can be served by shared runners (runners which added by admin).

This introduced an issue: shared runners do not remove projects from the temporary directory because of performance reason. This means that by creating a special job script it is possible to get access to the repository of any project which has been ran on the shared runner.

This fix disables the option "Allow shared runners" in project settings for those projects that have at least one specific runner.

For installations from source we advise you to upgrade GitLab CI using traditional method.


<!-- more -->

## Upgrade barometer

Upgrading GitLab CI from 7.9.1 to 7.9.2 contains database migrations. Downtime is not required but it is recommended as existing records are updated.

Upgrading GitLab CE or EE from 7.9.1 requires no downtime as this release contains no changes related to GitLab.

## Upgrading

Omnibus-gitlab packages for GitLab 7.9.2 are [now available](https://about.gitlab.com/downloads/).

To upgrade a GitLab installation from source please use the
[upgrader](http://doc.gitlab.com/ce/update/upgrader.html) or the [patch update
guide](http://doc.gitlab.com/ce/update/patch_versions.html).

To upgrade a GitLab CI installation from source, please use the [upgrade guide](https://gitlab.com/gitlab-org/gitlab-ci/blob/master/doc/update/patch_versions.md).

## Enterprise Edition

Omnibus packages for GitLab Enterprise Edition 7.9.2 are available for subscribers [here](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/install/packages.md). For installations from source, use [this guide](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/update/patch_versions.md).

Interested in GitLab Enterprise Edition?
For an overview of feature exclusive to GitLab Enterprise Edition please have a look at the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.
