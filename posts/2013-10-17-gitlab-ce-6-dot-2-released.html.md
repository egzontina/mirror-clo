---
title: "GitLab CE 6.2 released"
date: 2013-10-17 14:50
categories: release
community: true
---

### GitLab CE 6.2 released!

Hello everyone!

Today we release a new minor GitLab version, with new features, bug fixes and stability improvements.
GitLab is open source software to collaborate on code.
The main feature of the 6.2 release is fully browsable public projects. 

### Public projects

As of version 6.2 a user can visit public project pages (files, issues, wiki, etc.) without having a GitLab account.
Make sure you do not store private information in a public project wiki or issue tracker. :)

[![screenshot](/images/6_2/public_project.png)](/images/6_2/public_project.png)

<!--more-->

### User profile

In this version, we have made significant changes to the user's profile.

* You are able to upload your own avatar
* The current password is required when changing your password
* The password settings have moved to a separate page
* In order to change your email address you must confirm it

[![screenshot](/images/6_2/profile.png)](/images/6_2/profile.png)

### UI improvements

We have a fresh sign-in page for GitLab 6.2. :)

[![screenshot](/images/6_2/sign-in.png)](/images/6_2/sign-in.png)

Admin page

[![screenshot](/images/6_2/admin.png)](/images/6_2/admin.png)

### And much more. Just update to GitLab 6.2 and enjoy!

This release's most valuable person (MVP) is __Steven Thonus__ for contributing the avatar upload feature.

### Changes

Project:

  - Public projects are visible from the outside
  - PivotalTracker integration (Johannes Becker)
  - Flowdock integration (Boyan Tabakov)

Profile:

  - Require current password to change one
  - User must confirm his email if signup enabled
  - User must confirm changed email 
  - Avatar upload on profile page with a maximum of 200KB (Steven Thonus)

API: 

  - Feature: Search for projects by name to api (Izaak Alpert)
  - Feature: Remove group
  - Feature: Remove project
  - Feature: Download repo archive (Izaak Alpert)


Security:

  - Add more security specs
  - Extended User API to expose admin and can_create_group for user creation/updating (Boyan Tabakov)
  - Store the sessions in Redis instead of the cookie store
  - Respect authorization in Repository API

Misc:

  - Group owner or admin can remove other group owners
  - Make default user theme configurable (Izaak Alpert)
  - Update logic for validates_merge_request for tree of MR (Andrew Kumanyaev)
  - Rake tasks for webhooks management (Jonhnny Weslley)
  - Fixed relative links in markdown

- - -

### Links

For a full list of changes see the [CHANGELOG](https://github.com/gitlabhq/gitlabhq/blob/master/CHANGELOG).

If you are setting up a new GitLab installation follow the [Setup Guide](https://github.com/gitlabhq/gitlabhq/blob/6-2-stable/doc/install/installation.md).

__For update instructions see the [Update Guide](https://github.com/gitlabhq/gitlabhq/blob/master/doc/update/6.1-to-6.2.md).__

For LDAP group support and more have a look at the [feature list of GitLab Enterprise Edition](http://www.gitlab.com/gitlab-ee/).
Access to GitLab Enterprise Edition is included with a [GitLab.com subscription](http://www.gitlab.com/subscription/).
No time to upgrade or maintain Gitlab yourself?
GitLab.com also offers upgrade and installation services as part of a [GitLab.com subscription](http://www.gitlab.com/subscription/) or alternatively on a [consultancy basis](http://www.gitlab.com/consultancy/).

Updated on October 22 2013 to add the MVP and a description of GitLab in the opening paragraph.
