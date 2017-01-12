---
title: "GitLab 7.5.2 and GitLab CI 5.2.1 Release"
date: 2014-12-03
categories: release
author: Job van der Voort
---

Today we release GitLab 7.5.2 (both CE and EE) and GitLab CI 5.2.1.

GitLab 7.5.2 brings two fixes:

- Sidekiq arguments are no longer being logged. This prevents password reset tokens from appearing in the `sidekiq.log`
- Fixed a bug with restoring the backup of a wiki

GitLab CI 5.2.1 fixes several bugs:

- 500 error on /admin/builds
- Build API Request giving 400 / CSRF token authenticity error
- Build script info not being displayed well after update
- Problems with adding a project

<!-- more -->

## Upgrading

Omnibus-gitlab packages for GitLab 7.5.2 and GitLab CI 5.2.1 are [now available](https://about.gitlab.com/downloads/).

To upgrade a GitLab installation from source please use the
[upgrader](http://doc.gitlab.com/ce/update/upgrader.html) or the [patch update
guide](http://doc.gitlab.com/ce/update/patch_versions.html).

To upgrade a GitLab CI installation from source, please use the [upgrade guide](https://gitlab.com/gitlab-org/gitlab-ci/blob/master/doc/update/patch_versions.md).

## Enterprise Edition

Omnibus packages for GitLab Enterprise Edition 7.5.2 and GitLab CI 5.2.1 are available for subscribers [here](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/install/packages.md). For installations from source, use [this guide](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/update/patch_versions.md).

Interested in GitLab Enterprise Edition?
For an overview of feature exclusive to GitLab Enterprise Edition please have a look at the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.
