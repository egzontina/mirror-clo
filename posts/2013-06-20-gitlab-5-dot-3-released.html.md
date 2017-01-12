---
title: "GitLab 5.3 released"
date: 2013-06-20 09:28
categories: release
community: true
---

### GitLab 5.3 released

Hi everyone!

Today we release GitLab v5.3. We were mostly concentrated on bugs fixes and usability improvements in this version.
But we also added some new features like: Repository Graphs, Campfire/HipChat services integration, Code Snippet for users etc.

### The 3 most important improvements in GitLab 5.3

1. Repository Graph

    [![screenshot](/images/5_3/graph.png)](/images/5_3/graph.png)

2. HipChat/Campfire Services integration with your projects
3. Code Snippets now available for personal use. Create own snippets. Share public snippets with your colleagues

    [![screenshot](/images/5_3/snippets.png)](/images/5_3/snippets.png)

This release most valuable person (MVP) is __Karlo Nicholas T. Soriano__ for contributing the Repository Graph feature, thanks Karlo!

<!-- more -->

### Changes

New Features:

  * Repository Graph
  * HipChat/Campfire services integration
  * Advanced snippets: public/private, project/personal
  * Rename repository

Security:

  * Generate the Rails secret token on first run
  

Fixed:

  * Fixed bug with LDAP + git over http
  * Fixed bug with google analytics code being ignored
  * Respect newlines in wall messages
  * Fix project events duplicate on project page
  * Fix postgres error when displaying network graph.
  * Fix dashboard event filter when navigate via turbolinks
  * Fix dashboard lost if comment on commit
  * Fix bug with team assignation on project from #4109
  * Init.d: remove gitlab.socket on service start
  * Fixes issue with --depth option
  
API:

  * Api: Prevent blob content being escaped
  * Api: added teams api
  * Api: Smart deploy key add behaviour
  * Api: projets/owned.json return user owned project

- - -

_This release should be an easy upgrade from 5.2. Please use the upgrade guide doc :)_

- - -



### Links

For full list see [CHANGELOG](https://github.com/gitlabhq/gitlabhq/blob/master/CHANGELOG)

For new setup follow [Setup Guide](https://github.com/gitlabhq/gitlabhq/blob/5-3-stable/doc/install/installation.md)

__For update instructions see [Update Guide](https://github.com/gitlabhq/gitlabhq/blob/master/doc/update/5.2-to-5.3.md)__

No time to upgrade or maintain Gitlab yourself? GitLab.com offers [upgrade consulting services](http://www.gitlab.com/consultancy/) and [support subscriptions](http://www.gitlab.com/subscription/).

There is onging work to [integrate GitLab CI with GitLab to enable distributed builds](/2013/06/20/integrating-gitlab-ci-with-gitlab).
