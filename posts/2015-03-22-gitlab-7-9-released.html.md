---
title: "GitLab 7.9 released with drag and drop for all files and group hooks"
date: 2015-03-22
categories: release
author: Marin Jankovski
---

GitLab is open source software to collaborate on code.
Today we announce the release of a new version of GitLab Community Edition (CE) and GitLab Enterprise Edition (EE), with new features, usability and performance improvements, and bug fixes.
This is the biggest release of GitLab ever. This release alone contains over 70 entries in the [GitLab CE changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG) and more than 800 commits!
The biggest new features in Community Edition are Bitbucket importer, unsubscribe button and the possibility to drag-and-drop any file-type in issues and merge requests markdown.
In addition to the updates from Community Edition, GitLab Enterprise Edition has gained group level webhooks.

This month's Most Valuable Person ([MVP](https://about.gitlab.com/mvp/)) is Stan Hu for contributing number of features and fixes in GitLab Community Edition and omnibus-gitlab project.
Thanks Stan!

<!--more-->

## Dashboard

Dashboard received a facelift so you can see your starred projects, groups and milestones in one menu.

[![screenshot](/images/7_9/dashboard.png)](/images/7_9/dashboard.png)


## Bitbucket importer

With 7.9 comes a new way of importing your projects. Bitbucket importer is added so you can now import all your projects.


## Save web edit in new branch

When editing file in web editor UI you can save it to a new branch. This can speed up your workflow considerably as you can now easily create a merge request after.

[![screenshot](/images/7_9/new-branch.png)](/images/7_9/new-branch.png)


## Drag and drop any file in markdown

In previous versions it was easy to add a screenshot to a discussion. Now it is also possible to drag and drop pdf file or a zip archive in an issue description or comment!

[![screenshot](/images/7_9/drag-and-drop.png)](/images/7_9/drag-and-drop.png)

## Emoji One

With GitLab 7.9 we change the emoji library to Emoji One. What we like about Emoji One, apart from the gorgeous emojis, is that the software license matches our MIT license.

[![screenshot](/images/7_9/emoji.png)](/images/7_9/emoji.png)

## Subscribe/Unsubscribe from issue or merge request

Did you ever get mentioned in an issue just to be informed and then wanted to get away from the discussion? Every issue and merge request got
a subscribe/unsubscribe button so you can follow conversations that you find most important.

## Backup with git-annex files

With GitLab 7.8 we had the possibility to manipulate large binaries with git-annex. Backups did not include files uploaded with git-annex but with 7.9 all files will be archived (using tar) and included in the backup. Of course, if you used snapshots of your GitLab server everything was backed up anyway!

## Blocking users is non-destructive

Blocking user will not remove users from their projects and groups. GitLab 7.9 will disable their access so if you change your mind and unblock the user, they can get up and running quickly.


## Group level webhooks (EE only feature)

In earlier versions of GitLab you were able to add a webhook for a project.
Share the same webhooks between multiple projects - just setup it once in group.

[![screenshot](/images/7_9/group-hooks.png)](/images/7_9/group-hooks.png)

## Other changes

This release has more improvements, please check out [the Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG) to see the all named changes.


## Upgrade barometer

A new dependency is added, for installations from source `nodejs` is required. For Debian/Ubuntu it should be as easy as `sudo apt-get install nodejs`. For CentOS `yum install nodejs`.

Omnibus packages are shipped with nodejs already compiled so no action is needed if you are installing using a package.

When upgrading from 7.8.4 no downtime is required as database migrations are only adding new columns.

When upgrading from versions prior to 7.8.4 downtime is required due to database changes.

- - -

## Installation

If you are setting up a new GitLab installation please see the [installing GitLab page](https://www.gitlab.com/installation/).

## Updating

Upgrade instructions for omnibus-gitlab packages can be found in [the omnibus-gitlab repository](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/update.md).

If you installed GitLab from source and you have version 6.4.2 or higher you can use the [upgrade script](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/upgrader.md).
You have to update GitLab Shell to v2.6.0 manually, see [point 3 of the upgrade guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/7.8-to-7.9.md#3-update-gitlab-shell-and-its-config).

If you still want to do it manually - see the [Update Guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/7.8-to-7.9.md).

## Enterprise Edition

The mentioned EE only features and things like LDAP group support can be found in GitLab Enterprise Edition.
For a complete overview please have a look at the [feature list of GitLab EE](http://www.gitlab.com/gitlab-ee/).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/pricing/).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.

- - -
