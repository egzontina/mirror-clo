---
title: "GitLab 7.8.2 Released"
date: 2015-03-04
categories: release
author: Marin Jankovski
---

Today we release GitLab 7.8.2 CE, EE and GitLab CI 7.8.2.


GitLab 7.8.2 CE fixes:

- Fix service migration issue when upgrading from versions prior to 7.3
- Fix setting of the default use project limit via admin UI
- Fix display of already imported projects for GitLab and Gitorious importers
- Fix response of push to repository to return "Not found" if user doesn't have access
- Fix check if user is allowed to view the file attachment
- Fix import check for case sensitive namespaces

In addition to the fixes in 7.8.2 CE, Enterprise Edition 7.8.2 contains the following fixes:

- Check if LDAP admin group exists before querying for user membership
- Remove duplicate settings link in admin section

GitLab 7.8.2 CI fixes:

- Fix email notifications for build failures

<!-- more -->

## Upgrade barometer

This upgrade doesn't contain database migrations when upgrading from 7.8.1. so it can be done without downtime.

## Upgrading

Omnibus-gitlab packages for GitLab 7.8.2 are [now available](https://about.gitlab.com/downloads/).

To upgrade a GitLab installation from source please use the
[upgrader](http://doc.gitlab.com/ce/update/upgrader.html) or the [patch update
guide](http://doc.gitlab.com/ce/update/patch_versions.html).

To upgrade a GitLab CI installation from source, please use the [upgrade guide](https://gitlab.com/gitlab-org/gitlab-ci/blob/master/doc/update/patch_versions.md).

## Enterprise Edition

Omnibus packages for GitLab Enterprise Edition 7.8.2 are available for subscribers [here](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/install/packages.md). For installations from source, use [this guide](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/update/patch_versions.md).

Interested in GitLab Enterprise Edition?
For an overview of feature exclusive to GitLab Enterprise Edition please have a look at the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.
