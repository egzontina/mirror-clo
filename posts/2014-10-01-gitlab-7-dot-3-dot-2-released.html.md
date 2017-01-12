---
title: "GitLab 7.3.2 released"
date: 2014-10-01 13:30:15 +0200
categories: release
author: Marin Jankovski
---

We have released GitLab Community Edition 7.3.2 that fixes two issues:

- Fix bug when changes to post-receive worker was not dumped properly
- Fix creating new file via web editor

GitLab Enterprise Edition 7.3.2 also includes the above mentioned fixes.

<!--more-->

Packages for GitLab Community Edition 7.3.2 have been released for Ubuntu 12.04, Ubuntu 14.04, Debian 7, CentOS 6.5, CentOS 7.
GitLab Enterprise Edition packages can be found in the subscribers repository.

## Upgrading

Omnibus-gitlab packages for GitLab 7.3.2 are [now
available](https://about.gitlab.com/downloads/).
Be sure to do 'sudo gitlab-ctl stop nginx' before upgrading from 7.3.0.

To upgrade an installation
from source please use the
[upgrader](http://doc.gitlab.com/ce/update/upgrader.html) or the [patch update
guide](http://doc.gitlab.com/ce/update/patch_versions.html).

- - -
