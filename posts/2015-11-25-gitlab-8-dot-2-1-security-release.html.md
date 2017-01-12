---
title: "GitLab 8.2.1 security release"
date: 2015-11-25
author: Jacob Vosmaer
author_twitter: jacobvosmaer
---

We have found a remote code execution vulnerability in gitlab-shell
2.6.6 and 2.6.7. This affects GitLab Community Edition 8.2.0 and
GitLab Enterprise Edition 8.2.0. GitLab 8.1.4 and earlier versions
are not affected by this vulnerability.

This release also contains a number of other fixes, please see 
below for details.

<!-- more -->

GitLab allows users to push and pull Git data over SSH. To prevent
full system access via SSH we use gitlab-shell, a program that
sanitizes and validates SSH commands that run on the GitLab server
to send and receive Git data. Due to a change in gitlab-shell
2.6.6-2.6.7, an attacker who has a user account on a GitLab server
can bypass the sanitization in gitlab-shell and run arbitrary
commands on the GitLab server.

The only versions of GitLab that include a vulnerable version of
gitlab-shell  are GitLab Community Edition 8.2.0 and GitLab Enterprise
Edition 8.2.0. If you are still running GitLab 8.1 or earlier then
you are not affected by this vulnerability.  As an administrator
you can check your gitlab-shell version by going to
gitlab.example.com/admin and looking in the upper right corner in
the 'Components' section. Only gitlab-shell versions 2.6.6 and 2.6.7
are affected.

If you installed GitLab 8.2.0 on your server then you should  [upgrade
immediately](https://about.gitlab.com/update/).

## Other changes in 8.2.1

- Fix saving GitLabCiService as Admin Template 
- Fix the artifacts storage path
- Update required version of LFS client and separate the docs for users and admins
- Omnibus: create directories for artifacts and lfs-objects
- Omnibus: Make deploy page show on all pages when up

See the
[CHANGELOG](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG)
for more information.
