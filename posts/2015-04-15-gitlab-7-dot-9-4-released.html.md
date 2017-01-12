---
title: "GitLab 7.9.4 security release"
date: 2015-04-15
author: Jacob Vosmaer
author_twitter: jacobvosmaer
---

We have just released GitLab 7.9.4 which fixes an unrestricted local repository
import vulnerability. Additionally, this version addresses LDAP group
synchronization problems in GitLab Enterprise Edition and a bug that would
prevent more than 25 commit messages from being loaded in the file browser.

<!-- more -->

## Unrestricted local repository import vulnerability

GitLab allows users to import an existing repository when creating a new
project using `git clone`. Insufficient sanitization of user input made it
possible for an attacker with the rights to create new projects to clone any
git repository on disk accessible to the `git` user on the GitLab server. If
the attacker could guess the path on disk to a Git repository they could clone
it, allowing them to read Git data that they perhaps should not have access to.
An attacker needs to be authenticated as a GitLab user and to have the right to
create new projects to exploit this vulnerability.

Versions affected: GitLab Community Edition 7.9.3 and older, GitLab Enterprise
Edition 7.9.3 and older.

See below for update instructions.

## LDAP group syncronization problems (Enterprise Edition only)

We have recently discovered an incompatibility between the support for multiple
LDAP servers (added in GitLab EE 7.4) and the support for multiple identities
per user (e.g. LDAP, OAuth, Kerberos, added in GitLab 7.6). This
incompatibility causes the gradual introduction of invalid data into the SQL
database, which in turn causes LDAP group synchronization to stop working. In
GitLab 7.9.4 we have made application code changes to avoid this prolem in the
future. When you upgrade to GitLab 7.9.4 or newer any existing invalid data
related to this issue is automatically purged and corrected.

## Other fixes

GitLab 7.9.4 also fixes an issue where not all commit messages would get
displayed in the file browser.

## Upgrade barometer

We recommend shutting down your GitLab instance before upgrading to 7.9.4
because this release includes database migrations. The migrations themselves
run very quickly.

## Upgrading

Omnibus packages for GitLab 7.9.4 can be found via [our downloads
page](/downloads/).

For installations from source, use [this
guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/patch_versions.md).

**Interested in GitLab Enterprise Edition?**
For an overview of feature exclusive to GitLab Enterprise Edition please have a
look at the [features exclusive to GitLab
EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a
[subscription](http://www.gitlab.com/subscription/).
