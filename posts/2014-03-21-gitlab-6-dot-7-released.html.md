---
title: "GitLab CE 6.7 released!"
date: 2014-03-21
categories: release
community: true
---

[![screenshot](/images/6_7/public_group_pages.png)](/images/6_7/public_group_pages.png)

Hello everyone!

Gitlab is open source software made for collaborative coding.
Today we announce the release of a new version of GitLab Community Edition (CE), with new features, usability improvements and bug fixes.
The most notable new feature is the addition of public group profiles (see screenshot above).

This release's most valuable person (MVP) is Jason Hollingsworth for contributing the public group profile feature.

<!--more-->

## Markdown, wiki links and emoji

GitLab now renders newlines in Markdown text according to the specification, as [previously discussed](/2014/02/21/markdown-newline-behaviour/).

Relative links inside wiki pages stay inside the wiki, instead of pointing back to the accompanying repository.

Due to [licensing reasons](http://words.steveklabnik.com/emoji-licensing), GitLab 6.7 uses a new set of emoji based on the [emoji gem](https://github.com/steveklabnik/emoji) and [PhantomOpenEmoji](https://github.com/Genshin/PhantomOpenEmoji).
We thank Rei from [Emojidex](https://www.emojidex.com/) for creating freely licensed emoji's for GitLab.

## Repository imports

In previous versions, a Git repository import could get stuck leaving the user no option but removing the repository from GitLab and recreating it.
In GitLab 6.7, we have added an import timeout so that your import will not get stuck, and we have added a 'Retry' button in case the import failed due a transient condition.

## Technical changes

Due to a rewrite of our Git access authorization system, Git over HTTP now requires that your GitLab server has at least 2 Unicorn workers (which is the default value).
This means that small GitLab instances with only one Unicorn worker will only support SSH Git access going forward.

We advise users are running into the maximum HTTP push size of Nginx to [update their configuration](https://gitlab.com/gitlab-org/gitlab-ce/commit/6bf5215b2378fdb9cb442a053ddd12570c69d00c).

For a full list of changes see the [CHANGELOG](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG).

# Contributing guide link on the 'New Issue' page

When a user creates a new issue in a repository containing a 'CONTRIBUTING' file, GitLab reminds them to read the contributing guide.

[![screenshot](/images/6_7/contributing_guide.png)](/images/6_7/contributing_guide.png)

# Merge Request diff view improvements

It is now possible to add commits to a branch in a Merge Request using the web editor: just click 'Edit' in the Merge Request diff view.
In addition, you can now choose to hide diff comments.

[![screenshot](/images/6_7/diff_features.png)](/images/6_7/diff_features.png)

# New integrations: Gemnasium and Slack

[![screenshot](/images/6_7/gemnasium_slack.png)](/images/6_7/gemnasium_slack.png)

- - -

# Install

If you are setting up a new GitLab installation see the [installation section of the README](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/README.md#installation).

# Update 

If you have version 6.4.2 or higher you can use the [upgrade script](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/upgrader.md).
But you have to update GitLab Shell to 1.9.1 manually, see [point 3 of the upgrade guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/6.6-to-6.7.md#3-update-gitlab-shell-and-its-config).

If you still want to do it manually - see the [Update Guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/6.6-to-6.7.md).

# Enterprise

For LDAP group support and more have a look at the [feature list of GitLab Enterprise Edition](http://www.gitlab.com/gitlab-ee/).

Access to GitLab Enterprise Edition is included with a [GitLab.com subscription](http://www.gitlab.com/subscription/).

No time to upgrade or maintain Gitlab yourself?
GitLab.com also offers upgrade and installation services as part of a [GitLab.com subscription](http://www.gitlab.com/subscription/) or alternatively on a [consultancy basis](http://www.gitlab.com/consultancy/).

- - -
