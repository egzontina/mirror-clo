---
title: "GitLab 7.4 released with task lists and multiple LDAP servers support"
date: 2014-10-22
categories: release
author: Valery Sizov
---

Update: Since 7.4.0 the title of newly created internal snippets is exposed to people who are not logged in.
The contents of internal snippets is not exposed, and private snippets are not affected.
We will fix this in 7.4.2 which will release today, October 24.

GitLab is open source software to collaborate on code.
Today we announce the release of a new version of GitLab Community Edition (CE) and GitLab Enterprise Edition (EE), with new features, usability and performance improvements, and bug fixes.
The biggest new feature in Community Edition is task lists.
In addition to all the new features from Community Edition, GitLab Enterprise Edition gained support for multiple LDAP servers.

Other changes include reworked snippet access (now public, internal or private) and a README tab on the project home page for quick access. This version also includes a lot of bug fixes.

This month's Most Valuable Person ([MVP](/mvp)) is Vinnie Okada. He added cross-project references to the markdown parser, task lists to issue and merge request descriptions and improved event note display.
Thanks Vinnie!

<!--more-->

## Task lists.

You can define task list directly at the issue page by using special syntax `- [ ] title`. Check the [markdown tasks documentation](http://doc.gitlab.com/ce/markdown/markdown.html#task-lists) for details. When description has markdown tasks, issue will list progress on the issues index for [quick overview](/images/7_4/quick_task_overview.png). This feature makes the GitLab issue tracker more flexible.

[![screenshot](/images/7_4/task-list.png)](/images/7_4/task-list.png)


## The README tab on project show page.

This tab allows you to see readme page directly at the project main page. If a user selects the README tab, GitLab will remember this preference in the session. This means other projects will also directly show the README tab on the project main page.

[![screenshot](/images/7_4/project-readme.png)](/images/7_4/project-readme.png)


## Snippets can be public, internal or private.

You can now create snippets with various visibility levels. A public snippet is visible for everyone, even people that are not signed into your GitLab instance. Internal snippets are only visible to authorized users and private snippets are only visible to those with explicit access.

[![screenshot](/images/7_4/new-snippet.png)](/images/7_4/new-snippet.png)


## Support for multiple LDAP servers (EE only feature).

You can now hook up GitLab to multiple LDAP servers! When syncing LDAP groups, you can select the LDAP server. This way, a single GitLab instance can easily be used in very large enterprises.

[![screenshot](/images/7_4/ldap.png)](/images/7_4/ldap.png)

## Cross project references

GitLab will enable linking to commits, merge requests and issues in other projects by prepending a namespaced project path to the reference. What this means is that you can mention an issue from another project by using the special syntax:

* `namespace/project#123` : for issues
* `namespace/project!123` : for merge requests
* `namespace/project@1234567` : for commits

See [special GitLab references documentation](http://doc.gitlab.com/ce/markdown/markdown.html#special-gitlab-references) for more details.

## Other changes

This release has more improvements, please check out [the Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/7-4-stable/CHANGELOG) to see the all named changes.

## Cookbook GitLab is being deprecated

In the last few months the [Omnibus GitLab packages](https://about.gitlab.com/downloads/) have improved to the point where they have the same functionality as Cookbook GitLab. They allow much easier and faster installation than the cookbook.

Since the packages are more popular, keeping them up to date is a priority and any bugs are quickly found and solved.

For development environments we now recommend the [GitLab Development Kit](https://gitlab.com/gitlab-org/gitlab-development-kit/blob/master/README.md).

It is hard for us to justify updating the cookbook in addition to the packages.
For that reason, version 0.7.4 will be the last version of Cookbook GitLab updated by GitLab B.V.

We recognize that this will cause a difficult upgrade for the people currently using the cookbook but we think that it will be better in the long term.

For Chef environments we now offer [cookbook-omnibus-gitlab](https://gitlab.com/gitlab-org/cookbook-omnibus-gitlab) which will install and manage omnibus-gitlab package with Chef. We welcome any improvements and contributions.

- - -

# Installation

If you are setting up a new GitLab installation please see the [installing GitLab page](https://www.gitlab.com/installation/).

# Updating

Upgrade instructions for omnibus-gitlab packages can be found in [the omnibus-gitlab repository](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/update.md).

If you installed GitLab from source and you have version 6.4.2 or higher you can use the [upgrade script](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/upgrader.md).
If you still want to do it manually - see the [Update Guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/7.3-to-7.4.md).
There is an optional guide with [optimizations for GitLab setups with MySQL databases](https://gitlab.com/gitlab-org/gitlab-ce/blob/7-4-stable/doc/update/7.3-to-7.4.md#7-optional-optimizations-for-gitlab-setups-with-mysql-databases) to bring MySQL installations that have been around for a while up to the latest standards.

# Enterprise Edition

The mentioned EE only features and things like LDAP group support can be found in GitLab Enterprise Edition.
For a complete overview please have a look at the [feature list of GitLab EE](http://www.gitlab.com/gitlab-ee/).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.

- - -
