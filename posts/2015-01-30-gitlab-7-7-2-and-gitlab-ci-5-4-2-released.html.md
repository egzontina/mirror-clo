---
title: "GitLab 7.7.2 and GitLab CI 5.4.2 Released"
date: 2015-01-30
categories: release
author: Job van der Voort
---

Today we release GitLab 7.7.2 (CE and EE) and GitLab CI 5.4.2.

This release contains two security fixes. We recommend everyone that
uses protected branches, GitLab CI or LDAP to upgrade.

GitLab 7.7.2 fixes:

- Security fix: Fix a bug where developers can push to a protected branch
- Fix an issue where a LDAP user can't login with an existing GitLab account

GitLab CI 5.4.2 contains a single security fix:

- Security fix: Fix a bug where a CI user can get the CI project token
even if the user does not have access to the project

<!-- more -->

## Upgrading

Omnibus-gitlab packages for GitLab 7.7.2 and GitLab CI 5.4.2 are [now available](https://about.gitlab.com/downloads/).

To upgrade a GitLab installation from source please use the
[upgrader](http://doc.gitlab.com/ce/update/upgrader.html) or the [patch update
guide](http://doc.gitlab.com/ce/update/patch_versions.html).

To upgrade a GitLab CI installation from source, please use the [upgrade guide](https://gitlab.com/gitlab-org/gitlab-ci/blob/master/doc/update/patch_versions.md).

## Enterprise Edition

Omnibus packages for GitLab Enterprise Edition 7.7.2 and GitLab CI 5.4.2 are available for subscribers [here](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/install/packages.md). For installations from source, use [this guide](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/update/patch_versions.md).

Interested in GitLab Enterprise Edition?
For an overview of feature exclusive to GitLab Enterprise Edition please have a look at the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.
