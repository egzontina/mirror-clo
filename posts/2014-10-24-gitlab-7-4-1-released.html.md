---
title: "GitLab 7.4.1 released"
date: 2014-10-24
categories: release
author: Valery Sizov
---

Update: Since 7.4.0 the title of newly created internal snippets is exposed to people who are not logged in.
The contents of internal snippets is not exposed, and private snippets are not affected.
We will fix this in 7.4.2 which will release today, October 24.

Today we released GitLab Community Edition 7.4.1 and GitLab Enterprise Edition
7.4.1. This is a patch release which fixes the following things:

- allow unauthenticated access to public snippets
- fix Git HTTP access with LDAP credentials
- fix LDAP security checks for logged in users after updating to the new LDAP configuration syntax
- fix 500 error on projects with nested submodules

## Upgrading
Omnibus-gitlab packages for GitLab 7.4.1 are [now
available](https://about.gitlab.com/downloads/). To upgrade an installation
from source please use the
[upgrader](http://doc.gitlab.com/ce/update/upgrader.html) or the [patch update
guide](http://doc.gitlab.com/ce/update/patch_versions.html).
