---
title: "Gitlab 5.1 released"
date: 2013-04-22 11:11
categories: release
community: true
---

### GitLab 5.1 released

Hi everyone!

Today we release GitLab v5.1 live from [Railsberry](http://www.railsberry.com/) with 4 major improvements.

### The 4 most important improvements in GitLab 5.1

1. Notification settings. You can choose from 3 levels of notifications for every project.
2. Backup functionality was refactored. Now we backup attachments, write hooks in restored projects and update ssh permissions on restore.
3. Network graph becomes even cooler. Now with vertical orientation, commit messages and much more.
4. Improved performance and reduced memory consumption, among other things by switching the application server from Unicorn to Puma.

This release most valueable person (MVP) is Hiroyuki Sato for contributing the improved Network Graph, thanks Hiroyuki!

<!-- more -->

### Changes

New Features:

  * Notification settings
  * Login with username
  * File history now tracks renames
  * Show last commit on top of tree view

Dependencies:

  * Unicorn replaced with [Puma](http://puma.io/)

Security:

  * Admin has access to all projects now
  * Several fixes to prevent XSS

Improved:

  * Dashboard performance
  * Merge Request diff dump
  * Backup tools
  * Project transfer

Miscellaneous
Usability & UI improvements and more.

- - -

### Important upgrade note

We've fixed some bugs in the diff view for merge requests.
Merge requests that were closed before the upgrade will display "Nothing to merge" after the upgrade.
This can't be prevented, please make sure you don't need to revisit any closed merge requests before upgrading. Open merge requests are not affected, they will display the correct diff view.


- - -

### Links

For full list see [CHANGELOG](https://github.com/gitlabhq/gitlabhq/blob/master/CHANGELOG)

For new setup follow [Setup Guide](https://github.com/gitlabhq/gitlabhq/blob/5-1-stable/doc/install/installation.md)

__For update instructions see [Update Guide](https://github.com/gitlabhq/gitlabhq/blob/5-1-stable/doc/update/5.0-to-5.1.md)__

No time to upgrade or maintain Gitlab yourself? GitLab.com offers [upgrade consulting services](http://www.gitlab.com/consultancy/) and [support subscriptions](http://www.gitlab.com/subscription/).
