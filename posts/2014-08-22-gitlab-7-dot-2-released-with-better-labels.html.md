---
title: "GitLab 7.2 released with better labels"
date: 2014-08-22 12:50:22 +0200
categories: release
author: Marin Jankovski
---

GitLab is open source software to collaborate on code.
Today we announce the release of a new version of GitLab Community Edition (CE) and GitLab Enterprise Edition (EE), with new features, usability and performance improvements, and bug fixes.
The biggest new feature in Community Edition is new and improved labels.
In addition to the updates from Community Edition, GitLab Enterprise Edition allows administrator to send emails to users through the admin interface.

Other changes include the ability to star a project, an explore page for public projects and groups, an API for labels, improvements for diffs and various bug fixes.

This month's Most Valuable Person (MVP) is Robert Schilling for helping out on the issue tracker, with merge requests, writing code and fixing the website.
Thanks Robert!

<!--more-->

## Improved labels

You can now edit and delete labels and give them a (custom) color.

The characters '?', '&' and ',' are no longer allowed however, so those will be removed from your tags during the database migrations for GitLab 7.2.

[![screenshot](/images/7_2/labels1.png)](/images/7_2/labels1.png)
[![screenshot](/images/7_2/labels2.png)](/images/7_2/labels2.png)

## Star project

Thanks to the contribution by Ciro Santilli, projects can now be starred. Most starred projects can be viewed on the [public page](https://gitlab.com/explore/projects/starred).

[![screenshot](/images/7_2/star.png)](/images/7_2/star.png)


## Explore page

The Public Projects page has been redesigned. Popular projects are featured and it's easier to view all public groups and projects.

[![screenshot](/images/7_2/explore1.png)](/images/7_2/explore1.png)
[![screenshot](/images/7_2/explore2.png)](/images/7_2/explore2.png)

## Unfold the diff

You can now unfold hidden parts of the diff easily.

[![screenshot](/images/7_2/unfold.gif)](/images/7_2/unfold.gif)


## Renewed Google Authentication

If you are making use of Google Authentication you will need to enable Contacts API and Google+ API in the developer console of Google. This is because Google is deprecating some APIs September 1st.


## Send administrator emails to users (EE only feature)

Administrator can now send emails to all GitLab users or specific groups or projects. This is particularly convenient to quickly send a message to a group of people.

[![screenshot](/images/7_2/admin_email.png)](/images/7_2/admin_email.png)

## Other changes

Check out [the Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/7-2-stable/CHANGELOG) to see these and additional changes.

- - -

# Installation

If you are setting up a new GitLab installation please see the [installing GitLab page](https://www.gitlab.com/installation/).

# Updating

Upgrade instructions for omnibus-gitlab packages can be found in [the omnibus-gitlab repository](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/update.md).

If you installed GitLab from source and you have version 6.4.2 or higher you can use the [upgrade script](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/upgrader.md).
You have to update GitLab Shell to 1.9.7 manually, see [point 3 of the upgrade guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/7.1-to-7.2.md#3-update-gitlab-shell-and-its-config).
Cmake and pkg-config are an added dependencies, please install them before upgrading with the upgrader.

If you still want to do it manually - see the [Update Guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/7.1-to-7.2.md).

# Enterprise Edition

The mentioned EE only features and things like LDAP group support can be found in GitLab Enterprise Edition.
For a complete overview please have a look at the [feature list of GitLab EE](http://www.gitlab.com/gitlab-ee/).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.

- - -
