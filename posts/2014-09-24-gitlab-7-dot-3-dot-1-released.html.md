---
title: "GitLab 7.3.1 released"
date: 2014-09-24 11:30:15 +0200
categories: release
author: Marin Jankovski
---

We have released GitLab Community Edition 7.3.1 that fixes several issues:

- pushing to protected branches
- viewing diffs of files with changed permissions no longer gives a 500 error
- comments with new commits in merge requests now only show the relevant commits
- searching descriptions with relative links no longer causes 500 errors

GitLab Enterprise Edition 7.3.1 also includes the above mentioned fixes.

<!--more-->

Packages for GitLab Community Edition 7.3.1 have been released for Ubuntu 12.04, Ubuntu 14.04, Debian 7, CentOS 6.5, CentOS 7.
GitLab Enterprise Edition packages can be found in the subscribers repository.

## Upgrading

Omnibus-gitlab packages for GitLab 7.3.1 are [now
available](https://about.gitlab.com/downloads/).
Be sure to do 'sudo gitlab-ctl stop nginx' before upgrading from 7.3.0.

To upgrade an installation
from source please use the
[upgrader](http://doc.gitlab.com/ce/update/upgrader.html) or the [patch update
guide](http://doc.gitlab.com/ce/update/patch_versions.html).

- - -
