---
title: "Patch releases for GitLab 7.2, 7.3 and 7.4 CE & EE"
date: 2015-01-20
categories: release
author: Patricio, Job
---

Today we are releasing a patch release for three previous GitLab CE and GitLab EE versions.

The patch releases fix a bug found in the `rugged` gem that could cause a segmentation fault when accessing a repository.

GitLab 7.2 and 7.3 will now use `gitlab_git` v6.2.2 and 7.4 will use `gitlab_git` v.7.0.0.rc12,
which depend on rugged.

<!-- more -->

## Upgrading

The new Omnibus-gitlab packages for GitLab 7.2.3, 7.3.3 and 7.4.5 are [now available](https://about.gitlab.com/downloads/archives).

To upgrade a GitLab installation from source please use the
[upgrader](http://doc.gitlab.com/ce/update/upgrader.html) or the [patch update
guide](http://doc.gitlab.com/ce/update/patch_versions.html).

## Enterprise Edition

Omnibus packages for GitLab Enterprise Edition 7.2.3, 7.3.3 and 7.4.5 are available for subscribers [here](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/install/packages.md). For installations from source, use [this guide](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/update/patch_versions.md).

Interested in GitLab Enterprise Edition?
For an overview of feature exclusive to GitLab Enterprise Edition please have a look at the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.
