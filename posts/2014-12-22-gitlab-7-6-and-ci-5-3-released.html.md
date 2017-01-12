---
title: "GitLab 7.6 and GitLab CI 5.3 released with Audit log, Rebasing and more authentication options"
date: 2014-12-22
categories: release
author: Job van der Voort
---

GitLab is open source software to collaborate on code.
Today we announce the release of a new version of GitLab Community Edition (CE) and GitLab Enterprise Edition (EE), with new features, usability and performance improvements, and bug fixes.

GitLab Community Edition now supports multiple Omniauth providers for a single user,
meaning you can link your accounts from Google, Twitter and others.

In addition to the updates from Community Edition, GitLab Enterprise Edition has gained **Audit Log**, **Rebasing** before a merge request and **Kerberos support**.

This month's Most Valuable Person ([MVP](https://about.gitlab.com/mvp/)) is Ben Bodenmiller. Ben sweats the small stuff, which adds much appreciated polish to GitLab. Thanks Ben!

<!--more-->

### Link your social accounts

GitLab now support multiple Omniauth providers for a single user. That means
you can easily link your Google, Twitter and GitHub accounts and use them
to log into your GitLab instance.

[![screenshot](/images/7_6/omniauth.png)](/images/7_6/omniauth.png)

### Better Mobile UI

We improved GitLab for small screens, so it's easier to merge while
on the road!

[![screenshot](/images/7_6/small.png)](/images/7_6/small.png)

### Fork to Group

You can now fork a project to a group of your choosing.

[![screenshot](/images/7_6/fork.png)](/images/7_6/fork.png)

### Rebase before Merge (EE only)

Do you want to rebase your branch before merging?
GitLab can now do this for you!
This will ensure that you have a linear git history on master, making it easier to reason about it.

Simply turn on the feature for the project that you want to use this for
and check the box on merge.

[![screenshot](/images/7_6/rebase.png)](/images/7_6/rebase.png)

### Audit log (EE only)

From 7.6 EE on, GitLab will automatically track member changes in the audit log for each project and group.

[![screenshot](/images/7_6/audit.png)](/images/7_6/audit.png)

### Kerberos support (EE only)

GitLab 7.6 introduces support for authentication with Kerberos, in addition
to the various OAuth providers, LDAP and Active Directory authentication.

### Other changes

This release has more improvements, please check out [the Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/7-6-stable/CHANGELOG) to see the all named changes.


### Upgrade barometer

This is a straightforward upgrade, coming from 7.5.

- - -

## Installation

If you are setting up a new GitLab installation please see the [installing GitLab page](https://www.gitlab.com/installation/).

## Updating

Upgrade instructions for omnibus-gitlab packages can be found in [the omnibus-gitlab repository](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/update.md).

If you installed GitLab from source and you have version 6.4.2 or higher you can use the [upgrade script](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/upgrader.md).
You have to update GitLab Shell to ***2.4.0*** manually, see [point 3 of the upgrade guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/7.5-to-7.6.md#3-update-gitlab-shell-and-its-config).

If you still want to do it manually - see the [Update Guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/7.5-to-7.6.md).

## Enterprise Edition

The mentioned EE only features and things like LDAP group support can be found in GitLab Enterprise Edition.
For a complete overview please have a look at the [feature list of GitLab EE](http://www.gitlab.com/gitlab-ee/).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/pricing/).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.
