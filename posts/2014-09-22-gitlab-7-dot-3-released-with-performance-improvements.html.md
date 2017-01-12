---
title: "GitLab 7.3 released with performance improvements"
date: 2014-09-22 12:50:22 +0200
categories: release
author: Marin Jankovski
---

GitLab is open source software to collaborate on code.
Today we announce the release of a new version of GitLab Community Edition (CE) and GitLab Enterprise Edition (EE), with new features, usability and performance improvements, and bug fixes.
The biggest new feature in Community Edition is the improved performance with large pushes.
Other changes include the ability to edit a file in fullscreen (zen) mode, 'comment and close' button, wiki and snippets search and several API improvements.

In addition to the updates from Community Edition, GitLab Enterprise Edition allows assigning multiple LDAP groups to a single GitLab group.

This month's Most Valuable Person (MVP) is Robert Schilling for contributing zen mode, keyboard shortcuts and helping out on the issue tracker.
Thanks Robert!

<!--more-->

_Updated 2014-09-23 10:00 CEST:_ Added a paragraph about omnibus-gitlab changes.

## Improved performance on large pushes

Previously on a push that contained 1 thousand branches GitLab would create 1 thousand workers.

That would take some time to process during which other background tasks would be queued.

With the changes introduced in GitLab 7.3, a single push will only create a single worker which will handle all branches.

This allows other workers to be ready for new jobs and any long running workers can
easily be stopped if necessary and making it less likely that GitLab slows down due to large pushes.


## Keyboard shortcuts

Thanks to the contribution by Robert Schilling, keyboard shortcuts have been further improved with multiple shortcuts added. Navigation in GitLab just got easier!

[![screenshot](/images/7_3/keyboard.png)](/images/7_3/keyboard.png)


## Comment and close button

When commenting in an issue or merge request you can now easily close an issue while leaving the comment.

[![screenshot](/images/7_3/comment_and_close.gif)](/images/7_3/comment_and_close.png)

## Zen (fullscreen) mode

Thanks to the contribution by Robert Schilling, you can now switch into a fullscreen mode to have more room to edit your issue, merge request or a comment.

[![screenshot](/images/7_3/zen.gif)](/images/7_3/zen.gif)


## New commits linked in Merge Request

When new commits are pushed to the existing Merge Request, they will be shown in the Merge Request timeline.

[![screenshot](/images/7_3/linked_commits.png)](/images/7_3/linked_commits.png)

## New API features

Users can now filter issues by state and labels when interacting with the API.

Thanks to sponsoring by O'Reilly Media it is now possible to sort merge requests in ascending or descending order for updated_at and created_at fields.

In addition you can also get more detailed information about merge requests and comments.
You can read more about the GitLab API at [doc.gitlab.com/ce/api](http://doc.gitlab.com/ce/api/README.html).


## Assigning multiple LDAP groups to a GitLab group (EE only feature)

Synchronizing with more than one LDAP group is now possible with GitLab 7.3 EE.
You can link multiple LDAP groups to a single GitLab group and give them different permissions.

This makes our LDAP integration much more powerful and flexible.

Check the [documentation](http://doc.gitlab.com/ee/integration/ldap.html#synchronizing-with-more-than-one-ldap-group-gitlab-ee-7.3-and-newer) for more information.

[![screenshot](/images/7_3/multiple_ldap_groups.png)](/images/7_3/multiple_ldap_groups.png)

## Security: connect to Redis via sockets

Redis is an in-memory database used by GitLab for asynchronous inter-process communication, cache storage and session storage.
A standard Redis installation trusts all local TCP connections.
This means that an attacker who can create a TCP connection originating on the GitLab server could be able to modify or read user session data.
As a security measure against this risk we are changing the default settings for GitLab to connect to Redis via Unix domain sockets.
This allows system administrators to limit Redis access to the `git` user using file/directory permissions.

What do you need to do to switch to Redis via sockets?

- Omnibus-gitlab users switch to sockets automatically when they upgrade to 7.3.
Tip: if you changed your Redis port in gitlab.rb with `redis['port'] = xxxx` to avoid port conflicts, you can remove that line now.
- The required configuration changes for manual installations are [described in the 7.3 upgrade guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/7.2-to-7.3.md).
- Instructions for cookbook-gitlab are still a [work in progress](https://gitlab.com/gitlab-org/cookbook-gitlab/issues/68).

Unix domain sockets only work for connections between local processes.
If your Redis instance is running on another machine consider adding the firewall rules below.
Alternatively, you could create an encrypted connection between the GitLab server and the Redis server using [spiped](http://www.tarsnap.com/spiped.html).

```
# Iptables example for GitLab installations which cannot use sockets
# We assume the Redis server is listening at 192.168.99.1:6379

# Allow outgoing connections to 192.168.99.1:6379 for the git user.
# Disallow outgoing connections to 192.168.99.1:6379 for everybody else.
# Note: the order of these rules matters.
iptables -A OUTPUT -m owner --uid-owner git -p tcp -d 192.168.99.1 --dport 6379 -j ACCEPT
iptables -A OUTPUT -p tcp -d 192.168.99.1 --dport 6379 -j REJECT
```

We would like to thank Wyatt J. Brown for their responsible disclosure of this issue.

## Omnibus-gitlab now supports non-bundled web servers

The omnibus-gitlab packages provide a bundled NGINX web server which acts as a reverse proxy for GitLab, and which also serves static files such as Javascript, CSS files and user uploads.
Prior to omnibus-gitlab 7.3 it was not supported to use a web server other than the bundled NGINX, because the omnibus-gitlab directory layout prevented access to user uploads in the interest of security.
In omnibus-gitlab 7.3 we have changed the omnibus-gitlab directory layout and permissions to allow for non-bundled web servers.
As a side benefit, we now have a stronger privilege separation between NGINX and the GitLab Rails application.

To implement this change, omnibus-gitlab now creates a `gitlab-www` user which is intended to have read-only access to user uploads and read-write access to the Unicorn socket.
For practical reasons, the socket used for communication between NGINX and Unicorn was moved from `/var/opt/gitlab/gitlab-rails/tmp/sockets` to `/var/opt/gitlab/gitlab-rails/sockets`.
For more information about using a non-bundled web server with omnibus-gitlab, please see the [omnibus-gitlab README](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/7-3-stable/README.md#use-non-bundled-web-server).

In addition to the changes above, we changed the NGINX directory layout to avoid directories like `/opt/gitlab/embedded/proxy_temp` being created by NGINX.
These temporary directories now get created in `/var/opt/gitlab/nginx`.

## Other changes

Check out [the Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/7-3-stable/CHANGELOG) to see these and additional changes.

## Upgrade barometer

When upgrading to 7.3 there will be more time needed for migrations since there has been an important update to the GitLab structure, more specifically git hooks.

In addition to the hooks update there is a migration for the serialization of project services which loops through a lot of data. On installation with more than 10000 projects this migration alone took about 3 minutes.

** NOTE ** Users with large number of repositories (more than 1000) can expect prolonged downtime(up to 100 minutes depending on number or reporitories) if upgrading from versions <= 7.2.1 . For that reason, we advise
first upgrading to version 7.2.2, see [this blogpost for detailed information](https://about.gitlab.com/2014/09/19/gitlab-7-dot-2-2-security-release/#hooks-migration-script)

Users with smaller number of repositories (less than 1000) can safely upgrade directly to 7.3 expecting downtime similar to previous upgrades.

## Other news
We just [announced](https://about.gitlab.com/2014/09/22/wandisco-integrates-gitlab-enterprise-edition-in-their-git-multisite-offering/) that WANdisco will incorporate GitLab in their globally distributed git product.

- - -

# Installation

If you are setting up a new GitLab installation please see the [installing GitLab page](https://www.gitlab.com/installation/).

# Updating

Upgrade instructions for omnibus-gitlab packages can be found in [the omnibus-gitlab repository](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/update.md).

If you installed GitLab from source and you have version 6.4.2 or higher you can use the [upgrade script](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/upgrader.md).
You have to update GitLab Shell to 2.0.0 manually, see [point 3 of the upgrade guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/7.2-to-7.3.md#3-update-gitlab-shell).

If you still want to do it manually - see the [Update Guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/7.2-to-7.3.md).

# Enterprise Edition

The mentioned EE only features and things like LDAP group support can be found in GitLab Enterprise Edition.
For a complete overview please have a look at the [feature list of GitLab EE](http://www.gitlab.com/gitlab-ee/).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.

- - -
