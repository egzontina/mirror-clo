---
title: "GitLab CI 2.2 released"
date: 2013-04-09 16:56
categories: release
community: true
---

### GitLab CI version 2.2 released

Hi everyone!

Today we released new version of GitLab CI. 
We fixed some bugs, updated libraries to recent versions and made some ui imporvements.

We strongly recommend to update since this release include security fixes from rails & devise.
Also it should save you additional 50-100MB RAM by replacing unicorn with puma.

<!-- more -->

![Scrrenshot](/images/ci_2_2/gitlab_ci_2_2.png)

### CHANGELOG

* updated rails to 3.2.13
* updated bunch of gems
* added gravatar support
* increased test coverage (85% now)
* fixed bug with timeout in builds 
* fixed issue when build left in running status if exception triggered
* build runner is more transactional safe now
* replaced unicorn(web server) with puma
* fixed issue with saving user profile changes


### [Update from 2.1](https://github.com/gitlabhq/gitlab-ci/wiki/Migrate-from-2.1-to-2.2)

### [Setup](https://github.com/gitlabhq/gitlab-ci/blob/2-2-stable/doc/installation.md)
