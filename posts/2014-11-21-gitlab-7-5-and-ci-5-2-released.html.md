---
title: "GitLab 7.5 and GitLab CI 5.2 released with new and custom git hooks and parallel builds"
date: 2014-11-21
categories: release
author: Job van der Voort
---

GitLab is open source software to collaborate on code.
Today we announce the release of a new version of GitLab Community Edition (CE) and GitLab Enterprise Edition (EE), with new features, usability and performance improvements, and bug fixes.
In addition we are releasing GitLab CI 5.2.

GitLab Community Edition 7.5 brings custom git hooks, various performance improvements, API extensions and better GitLab CI support.

In addition to the updates from Community Edition, GitLab Enterprise Edition has gained automatic daily LDAP sync and git hooks to restrict commit authors.

This month's Most Valuable Person ([MVP](https://about.gitlab.com/mvp/)) is Martijn van Bemmel.
Martijn is a very productive designer, having created the [cool](https://gitlab.com/gitlab-com/gitlab-artwork/blob/master/flyer/flyer_biker.png) [graphics](https://gitlab.com/gitlab-com/gitlab-artwork/blob/master/flyer/flyer_scar.png) for GitLab 7.0,
the [MVP Badge](https://about.gitlab.com/mvp/), the [Golden Gear medal](https://gitlab.com/gitlab-com/www-gitlab-com/merge_requests/318#note_296648) and the [various](https://about.gitlab.com/community/) [graphics](https://about.gitlab.com/features/) on our site.
We really appreciate his enthusiastic contributions, Thanks Martijn!

<!--more-->

## Custom Git Hooks

GitLab now supports custom Git Hooks! This means that you can run anything you want
on pre/post-receive and update actions. Please see [our documentation](http://doc.gitlab.com/ce/hooks/custom_hooks.html) for more information.

This has been a much requested feature and has been contributed by Drew Blessing and Jose Kahan.

Thanks Drew and Jose!


## API Improvements

The API has been extended and improved in several points:

- Project events API will expose the username (sponsored by O'Reilly Media)
- Deleting a branch will return valid JSON
- Annotated tags API improved (contributed by Sean Edge)


## Atlassian Bamboo CI Service

Thanks to the contribution of Drew Blessing, GitLab now integrates with Atlassian Bamboo CI.

[![screenshot](/images/7_5/bamboo.png)](/images/7_5/bamboo.png)


## Git Hooks to check author and filename (EE only feature)

We've added some cool new Git Hooks:

- Check whether the author of a commit is a member of the GitLab instance
- Restrict commit authors to a given regular expression
- Restrict commits by filenames to a given regular expression

[![screenshot](/images/7_5/githooks.png)](/images/7_5/githooks.png) ***Our complete list of Git Hooks in GitLab EE 7.5***

## Automatic Daily LDAP Sync (EE only feature)

GitLab Enterprise Edition will now automatically sync all LDAP members on a daily basis. You can configure the time that it happens.

LDAP group synchronization in GitLab Enterprise Edition works by GitLab periodically updating the group memberships of _active_ GitLab users.
If a GitLab user becomes _inactive_ however, their group memberships in GitLab can start to lag behind the LDAP server group memberships.
Starting with GitLab 7.5 Enterprise Edition, GitLab will also update the LDAP group memberships of inactive users, by doing a daily LDAP check for _all_ GitLab users.

> Example:
John Doe leaves the company and is removed from the LDAP server.
At this point he can no longer log in to GitLab 7.4 EE.
But because he is no longer active on the GitLab EE server (he cannot log in!), his LDAP group memberships in GitLab no longer get updated, and he stays listed as a group member on the GitLab server.

> Now with GitLab 7.5 Enterprise Edition, within 24 hours of John being removed from the LDAP server, his user will also stop being listed as a member of any GitLab groups.

## Other changes

This release has more improvements, please check out [the Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/7-5-stable/CHANGELOG) to see the all named changes.


## Upgrade barometer

Upgrading GitLab from 7.4 to 7.5 is an easy upgrade.

If you are using GitLab CI 5.1 or earlier then you need to upgrade your GitLab CI installation to 5.2 at the same time as you upgrade GitLab to 7.5.
GitLab 7.5 is incompatible with GitLab CI 5.1 and earlier.

# GitLab CI 5.2

We're proud to release GitLab CI 5.2 together with GitLab 7.5.

GitLab CI 5.2 requires GitLab 7.5.

## Parallel builds

You can now run parallel builds on GitLab CI. For instance, if you have two or more test suites, you are able to run them at the same time. This can significantly reduce buildtime and therefore speed up your CI process.

[![screenshot](/images/7_5/pa_build.png)](/images/7_5/pa_build.png)

# Installation

If you are setting up a new GitLab installation please see the [installing GitLab page](https://www.gitlab.com/installation/).

GitLab CI is [now bundled with GitLab](https://about.gitlab.com/2014/11/06/gitlab-omnibus-packages-now-include-gitlab-ci/)!
If you prefer to install GitLab CI manually, please see the [documentation](https://docs.gitlab.com/ce/ci/quick_start/README.html).

To run your tests, you need to setup one or more GitLab CI Runners.
Runners are quick and easy to setup, please see the [runner repository](https://gitlab.com/gitlab-org/gitlab-ci-runner/blob/master/README.md).

# Updating

Upgrade instructions for omnibus-gitlab packages can be found in [the omnibus-gitlab repository](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/update.md).

If you installed GitLab from source and you have version 6.4.2 or higher you can use the [upgrade script](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/upgrader.md).
You have to update GitLab Shell to ***2.2.0*** manually, see [point 3 of the upgrade guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/7.4-to-7.5.md#3-update-gitlab-shell).

If you still want to do it manually - see the [Update Guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/7.4-to-7.5.md).

# Updating GitLab CI

Use the omnibus package which includes the latest GitLab CI version or see the [update guide](https://gitlab.com/gitlab-org/gitlab-ci/blob/master/doc/update/5.1-to-5.2.md).

# Enterprise Edition

The mentioned EE only features and things like LDAP group support can be found in GitLab Enterprise Edition.
For a complete overview please have a look at the [feature list of GitLab EE](http://www.gitlab.com/gitlab-ee/).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.

- - -
