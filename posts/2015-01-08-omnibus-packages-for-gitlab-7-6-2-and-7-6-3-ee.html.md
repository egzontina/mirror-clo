---
title: "Omnibus packages for GitLab 7.6.2 and 7.6.3-ee"
date: 2015-01-08 11:28:58 +0100
categories:
author: Marin Jankovski

---

Today we have released updated versions of GitLab Omnibus packages for the existing GitLab 7.6.2 Community Edition and GitLab 7.6.3
Enterprise Edition.

<!-- more -->

These updated packages contain a fix for a problem that affected limited amount of installations.
The problem was caused by a wrongly linked Kerberos library which caused issues on GitLab installations with Kerberos authentication enabled.


If you recently updated your Omnibus GitLab installation to 7.6.2 CE or 7.6.3 EE and encountered issues with Kerberos library, this package will only update the library. Upgrade instructions for omnibus-gitlab packages can be found in [the omnibus-gitlab repository](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/update.md).

If you haven't experienced any issues or are not using Kerberos authentication there is no need to update the packages.

This problem is not affecting installations from source.

