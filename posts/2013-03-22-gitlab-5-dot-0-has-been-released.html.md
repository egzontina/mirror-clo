---
title: "GitLab 5.0 release, standing on its own two feet"
date: 2013-03-22 12:02
categories: release
community: true
---

### GitLab 5.0 release, standing on its own two feet

Dear fellow GitLab enthusiasts,

Today marks the release of GitLab v5.0. In the last month a lot of work went into making GitLab faster, fully-featured and stable. And we have a lot of awesome changes to celebrate in this release. From now own GitLab is standing firmly on its own two feet with the introduction of GitLab shell.

<!-- more -->

GitLab is quickly maturing due to commercial support and cloud hosting. Since co-founding GitLab.com Dmitriy has been able to work on GitLab full-time, this means this release has more new features and better tests than ever. The GitLab Cloud service run by GitLab.com has grown to thousands of active users. This meant we had to improve GitLab performance and concurrency and these improvements all made their way into GitLab 5.0.

Before today every GitLab installation also meant installing Gitolite. Gitolite is a fine program but having the server standing on a GitLab foot and a Gitolite foot caused problems. Installing them and keeping the configurations in sync was a constant source of problems for many administrators of GitLab installation. Today Gitolite is replaced with GitLab-shell which will make installing and maintaining GitLab a lot easier.

### The 3 most important improvements in GitLab 5.0

1. GitLab-shell replaces Gitolite
2. Instead of needing __gitlab__ & __git__ users accounts on the system we now only need __git__ user to run GitLab
3. The wiki is stored in a git repository using the gollum library.

The wiki git repository was [contributed](https://github.com/gitlabhq/gitlabhq/pull/3183) by Dan Knox. We want to thank him for the great contribution and name him the Most Valuable Person (MVP) for this release.

At GitLab.com we are seeing that more organizations are interested in our [subscription service](http://blog.gitlab.com/subscription/). The cooperation with these organizations will lead to some cool new features for GitLab 5.1 and beyond.

We tried hard to make this major upgrade as easy as possible. Even before this release [more than 3.000 installations](http://rubygems.org/gems/gitlab_meta/versions/5.0) where already upgraded to 5.0.


### Changes

1. Features:

    * Import repository
    * Wiki on git using Gollum
    * Project, Group and Team description added
    * External issue tracker support

2. Dependencies:

    * Gitolite replaced with gitlab-shell

3. Security:

    * Use protected links for attachments
    * Rails, devise and other libraries updated
    * Several fixes to prevent XSS


Also a lot of usability & UI improvements and much more.

For full list see [CHANGELOG](https://github.com/gitlabhq/gitlabhq/blob/master/CHANGELOG)


### What we removed in 5.0:

* gitolite support

### What should be updated during migration:

Beside moving all stuff from __gitlab__ to __git__ user you also need to update next:

* gitlab.yml config
* init.d script
* nginx: replace home/gitlab with home/git
* config/unicorn.rb: replace home/gitlab with home/git


### SCREENSHOTS
Dashboard:

[![screenshot](/images/5_0/dashboard.png)](/images/5_0/dashboard.png)

Import repo:

[![screenshot](/images/5_0/import.png)](/images/5_0/import.png)

Project page:

[![screenshot](/images/5_0/project_page.png)](/images/5_0/project_page.png)

Wall behaves like chat now:

[![screenshot](/images/5_0/wall.png)](/images/5_0/wall.png)

Network Graph was improved too:

[![screenshot](/images/5_0/network.png)](/images/5_0/network.png)

One more theme for code review:

[![screenshot](/images/5_0/solarized.png)](/images/5_0/solarized.png)


- - -

### Guides:

* [Update from 4.2](https://github.com/gitlabhq/gitlabhq/wiki/From-4.2-to-5.0)
* [New Setup](https://github.com/gitlabhq/gitlabhq/blob/5-0-stable/doc/install/installation.md)

- - -
