---
title: "GitLab 7.0 released with drag and drop images and performance improvements"
date: 2014-06-22 16:18:54 +0300
categories: release
author: Dmitriy Zaporozhets
---

GitLab is open source software to collaborate on code.
Today we announce the release of a new version of GitLab Community Edition (CE) and GitLab Enterprise Edition (EE), with new features, usability and performance improvements, and bug fixes.
The biggest new feature in Community Edition is the ability to drag and drop an image with automatic upload in every markdown-area.
Other changes include drag and drop between columns in milestones for issues and merge requests, use of identicons when user doesn't have an avatar set and various peformance and UI updates.
In addition to the updates from Community Edition, GitLab Enterprise Edition received various bug fixes.

This month's Most Valuable Persons (MVP) are Earle Randolph Bunao and Neil Francis Calabroso for implementing drag and drop upload of image in every markdown-area.
Thanks Earle Randolph Bunao and Neil Francis Calabroso!

<!--more-->

GitLab has seen enormous progress since version 6.0 was released in August 2013.
Throughout the past ten months GitLab became more stable, simpler to install and easier to upgrade.
The most important factor in improving GitLab's stability was the launch of the Enterprise Edition in 6.0.
Introducing a commercial product allowed us to finance the expansion of the GitLab B.V. team and focus on doing more testing and fixing.
The Omnibus packages made GitLab easier to install than ever before. What used to be a 10-page manual of copy-paste is now a simple OS package installation.
Both the Omnibus packages and the upgrader script for manual installations introduced in GitLab 6.4 made GitLab much easier to upgrade.
Of course, most of the improvements in GitLab came not from the highlights above, but from all other contributions totaling 3554 commits from hundreds of contributors!
This caused GitLab usage to grow by leaps and bounds during the 6.x time-frame. GitLab is now used in over 100.000 organizations, a fourfold increase from the 25.000 when 6.0 launched.
We would like to thank everyone that contributed for helping to make GitLab the most installed software to collaborate on code.

## Attach images (JPG, PNG, GIF) by dragging & dropping or selecting them

Now you can easily attach several images to issue description or comment using drag & drop feature.

[![screenshot](/images/7_0/upload.gif)](/images/7_0/upload.gif)

## Permissions changes

We indroduced some changes to permissions model:

Developers: 

* can remove branch via UI and push
* can not remove or owerwrite git tags

Masters: 

* can not remove or force push to branch if it is protected
* can create projects in group (only if master is a group access level)

## Drag & drop issues inside milestone

Thanks to sponsoring by Codethink it is now possible to drag and drop issues and merge requests between the columns in milestones. This should make milestones even more user friendly and should make organizing milestones even easier. [changelog entry](https://gitlab.com/gitlab-org/gitlab-ce/blob/7be80fd89954a248527ca9be4bb9d9c320390811/CHANGELOG#L28).

[![screenshot](/images/7_0/milestone.gif)](/images/7_0/milestone.gif)

## Improved performance

Application is much faster now.

We have improved the performance of projects that have a large number of members.

When browsing files of a project that has large amount of files and directories, commit messages would take a lot of time to load and could potentially fail to load.
With the improvements introduced in 7.0, commit messages are loaded only for visible part of the screen which increases the load speed dramatically.

## Deprecations

GitLab 7.0 is dropping support for ruby 1.9.3. Starting with version 7.0 we recommend using latest ruby which is now supported, ruby 2.1.

We are also removing Wall from projects because we feel that the time needed for developing and keeping bug free is not justified if compared to the usefulness of the feature.

## Other changes

This release has many improvements, it includes more than 550 commits!
Please check out [the Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/7be80fd89954a248527ca9be4bb9d9c320390811/CHANGELOG) to see the 40 named changes.

- - -

# Installation

If you are setting up a new GitLab installation please see the [installing GitLab page](https://www.gitlab.com/installation/).

# Updating

Upgrading to this major release from 6.x should be relatively easy since there are no major changes in the architecture of GitLab.

Upgrade instructions for omnibus-gitlab packages can be found in [the omnibus-gitlab repository](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/update.md).

You can't use the upgrader, you'll have to upgrade manually - see the [Update Guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/6.9-to-7.0.md).

# Enterprise

For LDAP group support and more have a look at the [feature list of GitLab Enterprise Edition](http://www.gitlab.com/gitlab-ee/).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).

No time to upgrade or maintain Gitlab yourself?
GitLab B.V. also offers upgrade and installation services as part of a [subscription](http://www.gitlab.com/subscription/) or alternatively on a [consultancy basis](http://www.gitlab.com/consultancy/).

- - -
