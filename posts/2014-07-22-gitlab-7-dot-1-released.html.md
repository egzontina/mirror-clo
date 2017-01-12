---
title: "GitLab 7.1 released"
date: 2014-07-22 13:06:50 +0300
categories: release
author: Dmitriy Zaporozhets
---

GitLab is open source software to collaborate on code.
Today we announce the release of a new version of GitLab Community Edition (CE) and GitLab Enterprise Edition (EE), with new features, usability and performance improvements, and bug fixes.
With this release we introduce Group Milestones. Group Milestones allow you to see a grouped list of milestones from all projects in a group. This makes working with multiple projects much easier.
Also new are @all mentions in comments and improved code highlighting.
In addition to the updates from Community Edition, GitLab Enterprise Edition received various bug fixes.

This release's most valuable person (MVP) is Jeroen van Baarsen for his work as a merge marshal on the issue trackers, thanks Jeroen!


<!--more-->

## Group milestones

This feature allows you to see all milestones in a group, grouped by title. This makes it much easier to release software when working with multiple projects.

[![screenshot](/images/7_1/group_milestone.png)](/images/7_1/group_milestone.png) 

The milestone page shows you all issues from all projects that have the same milestone name.

[![screenshot](/images/7_1/group_milestone_show.png)](/images/7_1/group_milestone_show.png) 

## Show VERSION file in sidebar

If your repository has VERSION file - it will be rendered on the project sidebar. For instance, if you need to check the version of a library, this can save you some time.

[![screenshot](/images/7_1/version.png)](/images/7_1/version.png) 

## New login page

In GitLab Enterprise Edition we've previously changed the sign in page to implement customization. 
In order to reduce the difference between CE and EE we've ported the new look to CE.

[![screenshot](/images/7_1/login.png)](/images/7_1/login.png)

## Improved discussions

We've put some effort into improving discussion. 
Now, outdated comments will be hidden under the cut. 
If you still want to see these, you can easily expand the outdated comments.

[![screenshot](/images/7_1/discussion.png)](/images/7_1/discussion.png)

## Contributors API

Thanks to sponsoring by [Mobbr](https://mobbr.com), it is now possible to get all repository contributors with a single API call.
[Changelog entry](https://gitlab.com/gitlab-org/gitlab-ce/blob/7-1-stable/CHANGELOG#L18).

## Fetch SSH keys from LDAP account (EE only feature)

It is possible to configure GitLab Enterprise Edition so that users have their SSH public keys synchronised with an attribute that contains their key in their LDAP object.
Existing SSH public keys that are manually managed in GitLab are not affected by this feature.
To enable LDAP SSH key synchronization you need to [tell GitLab which LDAP attribute holds the SSH keys](http://doc.gitlab.com/ee/integration/ldap.html#synchronising-user-ssh-keys-with-ldap).

## Synchronize LDAP-enabled GitLab administrators with an LDAP group (EE only feature)

A group on the LDAP server can be given GitLab administrator access.
This ensures that the list of administrators in GitLab is always up to date.
The LDAP Common Name of the group that holds your administrators needs to be [configured on your GitLab server](http://doc.gitlab.com/ee/integration/ldap.html#define-gitlab-admin-status-via-ldap).

- - -

# Installation

If you are setting up a new GitLab installation please see the [installing GitLab page](https://www.gitlab.com/installation/).

# Updating

Upgrade instructions for omnibus-gitlab packages can be found in [the omnibus-gitlab repository](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/update.md).

If you installed GitLab from source and you have version 7.0.0 or higher you can use the [upgrade script](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/upgrader.md).
You have to update GitLab Shell to ***1.9.6*** manually, see [point 3 of the upgrade guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/7.0-to-7.1.md#4-update-gitlab-shell-and-its-config).

If you still want to do it manually - see the [Update Guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/7.0-to-7.1.md).

# Enterprise

For LDAP group support and more have a look at the [feature list of GitLab Enterprise Edition](http://www.gitlab.com/gitlab-ee/).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).

No time to upgrade or maintain Gitlab yourself?
GitLab B.V. also offers upgrade and installation services as part of a [subscription](http://www.gitlab.com/subscription/) or alternatively on a [consultancy basis](http://www.gitlab.com/consultancy/).

- - -
