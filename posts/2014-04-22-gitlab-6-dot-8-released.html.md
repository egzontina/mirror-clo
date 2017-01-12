---
title: "GitLab CE 6.8 released"
date: 2014-04-22 10:04:04 +0100
categories: release
author: Marin Jankovski, Jacob Vosmaer
community: false
---

Hello everyone!

Gitlab is open source software made for collaborative coding.
Today we announce the release of a new version of GitLab Community Edition (CE), with new features, usability and performance improvements, and bug fixes.
The main new feature of this release is protection against force pushes.
Other changes include improvements to mentioning in comments, Merge Request UI improvements and new API features.

This month's Most Valuable Person is Jeroen van Baarsen for contributing many small fixes and helping people on the issue trackers.
Thanks Jeroen!

<!--more-->

## Force push protection

In GitLab 6.8 we are changing the behavior of protected branches: force pushes to protected branches will be blocked.
This allows users to protect against history rewriting on their protected branches (e.g. `master`) while preserving developer flexibility in unprotected feature branches.
If you really need to force-push to a protected branch you can temporarily 'unprotect' the branch.
Steven Thonus helped implement this feature.

Note: you need gitlab-shell 1.9.3 or newer to enable force push protection.

## Commenting

In GitLab comments, issues, merge requests and commit messages you can reference GitLab users using the `@username` notation, sending them a notification.
This is called 'mentioning a user'.
Besides notifications, mentioning is also used to address invididuals in a larger conversation.
Before GitLab 6.8, you could only mention project members.
In GitLab 6.8, you can also mention issue _participants_ who are not necessarily project members.

In addition to extending the reach of mentions, we have also improved the readability of comments; see the screenshot below.

[![screenshot](/images/6_8/comment_layout.png)](/images/6_8/comment_layout.png)

## Merge Request UI

We have restyled the widget that contains the build status and 'Accept merge request' controls.

[![screenshot](/images/6_8/mr_widget.png)](/images/6_8/mr_widget.png)

In addition, it is now also possible to remove a source branch after the merge if you forgot to check the 'Remove source-branch' checkbox.

[![screenshot](/images/6_8/remove_source_branch.png)](/images/6_8/remove_source_branch.png)

## New API features

Thanks to sponsoring by O'Reilly Media it is now possible to create Git branches through the API.

In addition you can also get more detailed information about merge requests and comments.
You can read more about the GitLab API at [doc.gitlab.com/ce/api](http://doc.gitlab.com/ce/api/README.html).

## OAuth sign-in flow

GitLab can be integrated with external authentication providers such as Twitter or Google through OAuth.
When a user signs into GitLab through OAuth for the first time, a GitLab user is created for them based on the OAuth user attributes.
In GitLab 6.8 we no longer assume that all OAuth providers supply an email attribute for the new GitLab user.
Instead, new OAuth users must now enter and confirm an email address after signing into GitLab for the first time.
This change does not apply to GitLab LDAP integration.

Also see the [new OAuth documentation page](http://doc.gitlab.com/ce/integration/omniauth.html) compiled by Drew Blessing.

## GZipped assets

Previously, GitLab was not equipped to serve assets with compression.
This increased the load time since the browser had to download all assets.
We've added the option to the example Nginx config to serve the pre-gzipped version of the assets.
Nginx has this module enabled by default in Ubuntu but if you are using the compiled version of Nginx, make sure that you have compiled it with `--with-http_gzip_static_module` flag.
More information on GZip compression [can be found here](http://guides.rubyonrails.org/asset_pipeline.html#gzip-compression).

To enable Nginx asset compression you need to [edit your configuration files](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/6.7-to-6.8.md#5-update-config-files).

## Many, many other improvements

There are over 500 commits in this release, including many small fixes and performance improvements.
Please see the [CHANGELOG](https://gitlab.com/gitlab-org/gitlab-ce/blob/6-8-stable/CHANGELOG) for more information.

- - -

# Install

If you are setting up a new GitLab installation see the [installation section of the README](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/README.md#installation).

# Update 

Upgrade instructions for omnibus-gitlab packages can be found in [the omnibus-gitlab repository](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/update.md).

If you installed GitLab from source and you have version 6.4.2 or higher you can use the [upgrade script](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/upgrader.md).
But you have to update GitLab Shell to 1.9.3 manually, see [point 3 of the upgrade guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/6.7-to-6.8.md#3-update-gitlab-shell-and-its-config).

If you still want to do it manually - see the [Update Guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/6.7-to-6.8.md).

# Enterprise

For LDAP group support and more have a look at the [feature list of GitLab Enterprise Edition](http://www.gitlab.com/gitlab-ee/).

Access to GitLab Enterprise Edition is included with a [GitLab.com subscription](http://www.gitlab.com/subscription/).

No time to upgrade or maintain Gitlab yourself?
GitLab.com also offers upgrade and installation services as part of a [GitLab.com subscription](http://www.gitlab.com/subscription/) or alternatively on a [consultancy basis](http://www.gitlab.com/consultancy/).

- - -