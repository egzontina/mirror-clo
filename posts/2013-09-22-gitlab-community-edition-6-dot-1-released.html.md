---
title: "GitLab Community Edition 6.1 released"
date: 2013-09-22 18:00
author: Jacob Vosmaer
categories: release
community: true
---

### GitLab Community Edition 6.1 released!

Hello everyone!
Today we release a new minor GitLab version, with new features, bug fixes and stability improvements.

<!--more-->

With GitLab 6.1 Community Edition you can now automatically close Issues using commit messages, see when an Issue was referenced in a commit or a comment, and add a description to a Merge Request.
Moreover, Issue and Merge Request ID's now start at 1 for each Project.

### Automatically close issues using commit messages
When you create a commit with a message [starting with 'Fixes #1' or 'Closes #1'](https://github.com/gitlabhq/gitlabhq/blob/6-1-stable/config/gitlab.yml.example#L49) and push it to master GitLab will close the issue you referred to.
If you create a Merge Request targeting master with commits in it that will close Issues, GitLab will tell you which Issues will be closed.

![gitlab](/images/6_1/link-MR-to-Issue.png)

### See when an Issue was referenced in a commit or a comment
When you refer to an Issue in a commit message or a comment on a Merge Request or another Issue, GitLab shows you that the issue was referenced.
![gitlab](/images/6_1/Issue-mentioned-elsewhere.png)

### Issue and Merge Request ID's start at 1 for each Project
The ID's for Issues and Merge Requests now start at 1 for each Project.
This means that bookmarked issue URL's will change.
Old issue URL's are redirected to the new one if the issue ID is too high for an internal ID.

### Add a description to a Merge Request
When you create a new Merge Request you can now add a description to it.
![gitlab](/images/6_1/description-for-MR.png)

This release's most valuable person (MVP) is __Ash Wilson__ for contributing the automatic issue closing and issue reference linking features.

### Changes
User Interface

  - Project specific IDs for issues, mr, milestones
  - Description field added to Merge Request
  - Improved commit diff
  - Link issues, merge requests, and commits when they reference each other with GFM (Ash Wilson)
  - Close issues automatically when pushing commits with a special message
  - Improve user removal from admin area
  - Add event filter for group and project show pages
  - Add links to create branch/tag from project home page
  - Add public-project? checkbox to new-project view
  - Improved compare page. Added link to proceed into Merge Request
  - New landing page when you have 0 projects

API

  - API: Sudo api calls (Izaak Alpert)
  - API: Group membership api (Izaak Alpert)

Other

  - Improved large commit handling (Boyan Tabakov)
  - Rewrite: Init script now less prone to errors and keeps better track of the service (Rovanion Luckey)
  - Invalidate events cache when project was moved
  - Remove deprecated classes and rake tasks
  - Send email to user when he was added to group

- - -

### Links

For a full list of changes see the [CHANGELOG](https://github.com/gitlabhq/gitlabhq/blob/master/CHANGELOG).

If you are setting up a new GitLab installation follow the [Setup Guide](https://github.com/gitlabhq/gitlabhq/blob/6-1-stable/doc/install/installation.md).

__For update instructions see the [Update Guide](https://github.com/gitlabhq/gitlabhq/blob/master/doc/update/6.0-to-6.1.md).__

For LDAP group support and more have a look at the [feature list of GitLab Enterprise Edition](http://www.gitlab.com/gitlab-ee/).
Access to GitLab Enterprise Edition is included with a [GitLab.com subscription](http://www.gitlab.com/subscription/).
No time to upgrade or maintain Gitlab yourself?
GitLab.com also offers upgrade and installation services as part of a [GitLab.com subscription](http://www.gitlab.com/subscription/) or alternatively on a [consultancy basis](http://www.gitlab.com/consultancy/).
