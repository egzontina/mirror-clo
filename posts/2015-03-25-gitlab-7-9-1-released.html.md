---
title: "GitLab 7.9.1 Released"
date: 2015-03-25
categories: release
author: Marin Jankovski
---

Today we release GitLab 7.9.1 CE, EE and GitLab CI 7.9.1.

Special thanks goes out to Stan Hu for providing majority of the fixes in GitLab CE 7.9.1.


GitLab 7.9.1 CE fixes:

  - Fix "Import projects from" button to show the correct instructions
  - Fix OAuth2 issue importing a new project from GitHub and GitLab
  - Fix for LDAP with commas in DN
  - Fix missing events and in admin Slack service template settings form
  - Don't show commit comment button when user is not signed in.
  - Downgrade gemnasium-gitlab-service gem to retain Ruby 2.0.x compatibility

Enterprise Edition 7.9.1 contains the fixes from Community Edition.

## 7.9.1 GitLab CI security release

In GitLab CI versions pre 7.9.1 it was possible, in certain cases, for specific runner to start behaving like a shared runner.
This is a security concern so we strongly advise upgrading to 7.9.1.

<!-- more -->

### Upgrade barometer

Upgrading GitLab CI from 7.9.0 to 7.9.1 requires downtime as this release contains database migrations which are changing existing records.

Upgrading from GitLab 7.9.0 requires no downtime as this release contains no migrations.

### Upgrading

Omnibus-gitlab packages for GitLab 7.9.1 are [now available](https://about.gitlab.com/downloads/).

To upgrade a GitLab installation from source please use the
[upgrader](http://doc.gitlab.com/ce/update/upgrader.html) or the [patch update
guide](http://doc.gitlab.com/ce/update/patch_versions.html).

To upgrade a GitLab CI installation from source, please use the [upgrade guide](https://gitlab.com/gitlab-org/gitlab-ci/blob/master/doc/update/patch_versions.md).

### Enterprise Edition

Omnibus packages for GitLab Enterprise Edition 7.9.1 are available for subscribers [here](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/install/packages.md). For installations from source, use [this guide](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/update/patch_versions.md).

Interested in GitLab Enterprise Edition?
For an overview of feature exclusive to GitLab Enterprise Edition please have a look at the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.
