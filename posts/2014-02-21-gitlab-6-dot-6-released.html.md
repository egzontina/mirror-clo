---
title: "GitLab CE 6.6 released"
date: 2014-02-21 11:47
categories: release
community: true
author: Marin Jankovski
---

### GitLab CE 6.6 released!

[![screenshot](/images/6_6/dash.png)](/images/6_6/dash.png)

Hello everyone!

As you know, Gitlab is open source software made for collaborative coding.
Today we released a new version of GitLab Community Edition (CE), with new features and bug fixes.


The MVP of this release is Drew Blessing for his contribution ["Mobile UI improvement"](https://github.com/gitlabhq/gitlabhq/pull/6159)

In this release we updated Rails to 4.0.3, which solves some security issues.
For more information see [rails blog post](http://weblog.rubyonrails.org/2014/2/18/Rails_3_2_17_4_0_3_and_4_1_0_beta2_have_been_released/).
We advise everyone to upgrade.

<!--more-->

## Changes

* Improved performance for large groups (with 100+ members) 
* Developers can manage the issue tracker (modify and reassign any issue)
* Links to markdown headers
* Large diffs are handled better
* The user page of a user is now publicly visible if the person is a member of a public project.
* Ability to filter by multiple labels for Issues page

For a full list of changes see the [CHANGELOG](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG).


## Group avatars

[![screenshot](/images/6_6/group.png)](/images/6_6/group.png)

## Issue redesign

[![screenshot](/images/6_6/issue.png)](/images/6_6/issue.png)

## Notification settings redesign

[![screenshot](/images/6_6/notify.png)](/images/6_6/notify.png)

## File view: Highlight.js and last commit for file

We moved the file syntax highlighting from the server side to the client side, thanks to this awesome library. http://highlightjs.org/


[![screenshot](/images/6_6/last_commit.png)](/images/6_6/last_commit.png)

## Nice violet theme

[![screenshot](/images/6_6/violet.png)](/images/6_6/violet.png)

- - -

# Install

If you are setting up a new GitLab installation see the [installation section of the README](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/README.md#toc_6).

# Update 

If you have version 6.4.2 or 6.5 you can use the [upgrade script](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/upgrader.md).

If you still want to do it manually - see the [Update Guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/6.5-to-6.6.md).

# Enterprise

For LDAP group support and more have a look at the [feature list of GitLab Enterprise Edition](http://www.gitlab.com/gitlab-ee/).

Access to GitLab Enterprise Edition is included with a [GitLab.com subscription](http://www.gitlab.com/subscription/).

No time to upgrade or maintain Gitlab yourself?
GitLab.com also offers upgrade and installation services as part of a [GitLab.com subscription](http://www.gitlab.com/subscription/) or alternatively on a [consultancy basis](http://www.gitlab.com/consultancy/).

- - -
