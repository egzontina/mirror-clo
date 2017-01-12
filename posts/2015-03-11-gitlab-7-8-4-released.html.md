---
title: "GitLab 7.8.4 Released"
date: 2015-03-11
categories: release
author: Marin Jankovski
---

Today we release GitLab 7.8.4 CE, EE and GitLab CI 7.8.4.

You might have noticed that 7.8.3 was not announced. It contained a fix for annotated tags without a message which was required for the Gitorious import on GitLab.com.

GitLab 7.8.4 CE contains:

- Fix for custom issue trackers where `issue_tracker_id` is being replaced in all links.
- Fix for duplicate paths and names in namespaces.

Enterprise Edition 7.8.4 contains the fixes from 7.8.4 CE.


<!-- more -->

## Upgrade barometer

This upgrade contains a migration that removes and updates records in the database so downtime is required.

*We strongly advise creating a backup before upgrading to 7.8.4.*

## Upgrading

Omnibus-gitlab packages for GitLab 7.8.4 are [now available](https://about.gitlab.com/downloads/).

To upgrade a GitLab installation from source please use the
[upgrader](http://doc.gitlab.com/ce/update/upgrader.html) or the [patch update
guide](http://doc.gitlab.com/ce/update/patch_versions.html).

To upgrade a GitLab CI installation from source, please use the [upgrade guide](https://gitlab.com/gitlab-org/gitlab-ci/blob/master/doc/update/patch_versions.md).

## Enterprise Edition

Omnibus packages for GitLab Enterprise Edition 7.8.4 are available for subscribers [here](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/install/packages.md). For installations from source, use [this guide](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/update/patch_versions.md).

Interested in GitLab Enterprise Edition?
For an overview of feature exclusive to GitLab Enterprise Edition please have a look at the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.
