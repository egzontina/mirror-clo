---
title: "GitLab 5.2 released"
date: 2013-05-22 13:04
categories: release
community: true
---

### GitLab 5.2 released

Hi everyone!

Today we release GitLab v5.2. We added forks, code search, turbolinks and much more awesome stuff.

### The 4 most important improvements in GitLab 5.2

1. Forking. You can a fork project into its own namespace now.
2. Code search. You search inside the project with a search bar on top panel.
3. Turbolinks. GitLab is much faster because almost all requests does not reload the page.
4. Shared deploy keys. You can use a deploy key for as many projects as you need and one project can use multiple keys.

This release most valuable person (MVP) is __Angus MacArthur__ for contributing the forking feature, thanks Angus!

<!-- more -->

### Changes

New Features:

  * Forks
  * Code search
  * Turbolinks
  * Shared Deploy keys
  * Advanced gfm autocomplete
  * Extra customization (google analytics, custom text on sign in page)

Security:
  
  * Public projects are more accessible for authenticated users(issues, merge requests)
  * You can push to git-http with ldap credentials

Fixed:

  * Git submodules listing under Files tab
  * Commit page error if there is a huge diff


- - -

_This release should be an easy upgrade from 5.1. Please use the upgrade guide doc :)_

- - -

### SCREENSHOTS

Fork:

[![screenshot](/images/5_2/fork.png)](/images/5_2/fork.png)

Search:

[![screenshot](/images/5_2/search_1.png)](/images/5_2/search_1.png)

Advanced autocomplete:

[![screenshot](/images/5_2/snapshot1.png)](/images/5_2/snapshot1.png)


### Links

For full list see [CHANGELOG](https://github.com/gitlabhq/gitlabhq/blob/master/CHANGELOG)

For new setup follow [Setup Guide](https://github.com/gitlabhq/gitlabhq/blob/5-2-stable/doc/install/installation.md)

__For update instructions see [Update Guide](https://github.com/gitlabhq/gitlabhq/blob/master/doc/update/5.1-to-5.2.md)__

No time to upgrade or maintain Gitlab yourself? GitLab.com offers [upgrade consulting services](http://www.gitlab.com/consultancy/) and [support subscriptions](http://www.gitlab.com/subscription/).
