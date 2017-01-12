---
title: "GitLab 7.8 released with GitLab.com integration, never-lost comments and GitLab Annex for managing large files"
date: 2015-02-22
categories: release
author: Job van der Voort
author_twitter: Jobvo
---

This is an exciting day. Today we release GitLab 7.8, the biggest release of GitLab ever. This release alone contains over 60 entries in the [GitLab CE changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG)!
We're very proud to show you the new features and improvements of GitLab Community Edition (CE) and GitLab Enterprise Edition.

GitLab Community edition brings among others, a GitLab.com importer,
new files in an empty repository, never-lost comments and group mentions.
GitLab Enterprise Edition adds to this the GitLab Annex feature to manage your large files with GitLab, improved JIRA integration and a GitHub Enterprise integration.

This month's Most Valuable Person ([MVP](https://about.gitlab.com/mvp/)) is Hannes Rosenögger.
Hannes took stale or old merge requests, fixed them up and contributed them to GitLab.
This is a great way to contribute and we're excited for him to join the core team.
Thanks Hannes!

<!--more-->

## GitLab.com integration: login with GitLab.com account and import projects from GitLab.com

Moving from GitLab.com to your own GitLab instance? It just became a lot easier!

You can login with your GitLab.com account to your instance and quickly import projects from GitLab.com.

## New file in Empty Repository

Don't like to switch to your commandline just to bootstrap a new GitLab project?
It's no longer necessary! You can now create a file in an empty repository without leaving GitLab:

[![screenshot](/images/7_8/new_file.png)](/images/7_8/new_file.png)

## Commit calendar

See when you made the most commits in a single glance with the commit calendar.
Try to fill an entire year of beautiful commits!

[![screenshot](/images/7_8/commit_calendar.png)](/images/7_8/commit_calendar.png)

## Never lose unsaved comments!

You're going to love this one. From now on, unsaved comments are automatically restored when you reload the page.
It's like magic and prevents you from ever losing comments again.

## Project avatars

Give your project a face with its own avatar:

[![screenshot](/images/7_8/project_avatar.png)](/images/7_8/project_avatar.png)

## Mention groups

Another killer feature: you can now mention entire groups at once.
Have something awesome to share with your group `awesome-people`? Just mention them in the comment,
issue or merge request with `@awesome-people` and everyone will get notified.

[![screenshot](/images/7_8/mention_groups.png)](/images/7_8/mention_groups.png)

## Select email for notifications

For some time you've been able to add multiple email addresses to GitLab.
Now you can actually select which address you want to receive notifications on.

[![screenshot](/images/7_8/set_notification_mail.png)](/images/7_8/set_notification_mail.png)

## Manage large files in Git with GitLab Annex (EE only feature)

Organisations are struggling with handling big files in their Git repositories.
Git-annex came to the rescue, but wasn't supported by any Git hosting solution,
making permission management of large files impossible. Until now.

GitLab Annex allows you to easily include large files in your git
repository, managed just as any other commit in GitLab.

We already [blogged](https://about.gitlab.com/2015/02/17/gitlab-annex-solves-the-problem-of-versioning-large-binaries-with-git/)
about GitLab Annex, as we're very excited about it.

[![screenshot](/images/7_8/git_annex.png)](/images/7_8/git_annex.png)

## Improved JIRA integration (EE only feature)

We improved our JIRA in a big way! Closing a JIRA ticket with a commit is now reported
back to JIRA with a nice description and link.

[![screenshot](/images/7_8/jira_service_close_issue.png)](/images/7_8/jira_service_close_issue.png)

On top of that you can now mention your JIRA tickets anywhere in GitLab and
we'll put a comment on the issue in JIRA, so everything is linked together neatly!

[![screenshot](/images/7_8/jira_issue_reference.png)](/images/7_8/jira_issue_reference.png)

## GitHub Enterprise Importer (EE only feature)

Moving from GitHub Enterprise to GitLab Enterprise Edition? Easy!
You can quickly migrate entire repositories and issues in a single click
with the new GitHub Enterprise importer.

[![screenshot](/images/7_8/gh_import.png)](/images/7_8/gh_import.png)

## Other changes

This release has more improvements, including security fixes, please check out [the (MASSIVE) Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/7-8-stable/CHANGELOG) to see the all named changes.

## GitLab CI versioning

From version 7.8 we have decided to change the versioning of GitLab CI and had its version bumped from 5.4.x to 7.8. The reason for this change is to make releasing as quick and easy as possible. Previously, GitLab CI was not packaged with the omnibus-gitlab package and GitLab CI version was a separate entity not related to GitLab. However, since GitLab CI got packaged having different versions made our release process cumbersome.
It also caused various misunderstandings in which CI goes with which version of GitLab.

By having the same version for GitLab and GitLab CI, this problem is resolved.

## Upgrade barometer

This is a regular upgrade. It contains several migrations,
none of which particularly scary.

For installations from source, you will have to update your NGINX configuration. We've added a route change for /uploads/.
See the new config for /uploads/ [here for http](https://gitlab.com/gitlab-org/gitlab-ce/blob/8ae3112b3f303c897c70952dd162589b1c394221/lib/support/nginx/gitlab#L60) and [here for https](https://gitlab.com/gitlab-org/gitlab-ce/blob/8ae3112b3f303c897c70952dd162589b1c394221/lib/support/nginx/gitlab-ssl#L105).

- - -

# Installation

If you are setting up a new GitLab installation please see the [installing GitLab page](https://www.gitlab.com/installation/).

# Updating

Upgrade instructions for omnibus-gitlab packages can be found in [the omnibus-gitlab repository](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/update.md).

If you installed GitLab from source and you have version 6.4.2 or higher you can use the [upgrade script](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/upgrader.md).
You have to update GitLab Shell to ***2.5.3*** manually, see [point 3 of the upgrade guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/7.7-to-7.8.md#3-update-gitlab-shell).

If you still want to do it manually - see the [Update Guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/7.7-to-7.8.md).

# Enterprise Edition

The mentioned EE only features and things like LDAP group support can be found in GitLab Enterprise Edition.
For a complete overview please have a look at the [feature list of GitLab EE](http://www.gitlab.com/gitlab-ee/).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/pricing/).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.

- - -
