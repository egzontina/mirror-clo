---
title: "GitLab 8.1 with deeper CI integration, MR improvements, and more. Released from our team summit in Amsterdam!"
date: 2015-10-22
categories: release
author: Job van der Voort
image_title: /images/8_1/team.jpg
author_twitter: Jobvo
---

With last month's release of 8.0, we made a lot of improvements to GitLab.
Today we bring you GitLab 8.1, which brings you a deeper CI integration, the ability to check out
any merge request, design updates, and more.

We as a team are really excited about this release not only for the increased performance and
great new features but also because we are all together in Amsterdam for our team summit.
Our team is [fully
remote](https://about.gitlab.com/2015/04/08/the-remote-manifesto/) from around the
world so this is a special update for us to be releasing GitLab 8.1 together from Amsterdam.
Next week the team will be attending [OSCON](https://about.gitlab.com/2015/10/14/gitlab-oscon-challenge-2015/)
so please let us know if you'll be there. We'd love to chat!

![The GitLab Inc Team](/images/8_1/team_sm.jpg)

GitLab now consists of [20,000 commits](https://gitlab.com/gitlab-org/gitlab-ce/commits/master)!
This is a great milestone for our community. With every release of GitLab, new people from
this great community contribute code and time. GitLab truly is a product built by the community
and we're honored to be part of it.

Zeger-Jan van de Weg did several nice contributions this release and we're happy
to elect him as this month's Most Valuable Person ([MVP](https://about.gitlab.com/mvp/))!
Thanks Zeger-Jan!

<!--more-->

## GitLab = GL + CI

In GitLab 8.0 we integrated GitLab CI into GitLab, making it a single application
where you can collaborate on, test, and deploy your code.

With GitLab 8.1, CI is everywhere.
You will find build status in the commit list view, in commits, and on the front page
of your projects. You'll also find graphs of CI in the graphs view and a new
builds page for quick access to your project's builds.

![GitLab CI Build status in the commit view](/images/8_1/ci1.png)

![GitLab CI build graphs under graphs](/images/8_1/ci2.png)

## Design Updates

In our ongoing effort to improve the look and feel of GitLab, we have
made many changes big and small this release.

We now have a new color scheme for major interface elements:

![Further improved looks](/images/8_1/design.png)

## Check out Merge Request

Previously, checking out a merge request from someone was only possible if the
branch was in a repository you can read. Right now, you can check out any merge
request made to your repository, even if it's from fork.

![Checkout any merge request](/images/8_1/co_mr1.png)

You could do this previously, but now we make the remote branch available
locally, making it much faster.

## Commit Status API

With the integration of GitLab CI in GitLab, we want to make it easier for
everyone to use CI. You can now get the status of any commit through the API.

```
GET /projects/:id/repository/commits/:sha/statuses
```

- [See the documentation on getting commit status through the API](http://doc.gitlab.com/ce/api/commits.html#get-the-status-of-a-commit)

In addition to this, you can even **set the commit status**. With this, you
can easily use any existing CI in combination with GitLab and still see the
commit status reflected in GitLab's interface!

```
POST /projects/:id/statuses/:sha
```

- [Docs on setting the commit status](http://doc.gitlab.com/ce/api/commits.html#post-the-status-to-commit)

The commit status API makes it easier to integrate your existing CI tools with GitLab.
We're looking forward to see what you'll use it for.


## Further improvements

### Auto-engage CI

GitLab will now automatically turn on CI for a project when you push
a `.gitlab-ci.yml` file. If you have some shared runner setup, this should
make it easier for your team to start using CI.

Of course, you can disable CI for projects you don't want to use it for.

### Fast, Faster!

We've been working hard to improve page speed. Issues, searching for users,
the trending page, signing in, and more will now load much faster.

### Create Directories from the Web Editor

You can now create directories straight from the interface!

![Create a directory from the GitLab interface](/images/8_1/create_dir.png)

### Activity on Dashboard

If you prefer to see activity on the Dashboard by default, you can now
easily set this in your profile:

![See relevant activity on your GitLab dashboard](/images/8_1/activity_dashboard.png)

### Sign in as other user

GitLab Administrators now have a simple, useful tool: you can sign in as
any other user.

![Log in as other user as GitLab Admin](/images/8_1/loginas.png)

Visit a user through the admin panel to find the button above.

### Quick Submit

Simply use `CMD+ENTER` on Mac or `CTRL+ENTER` on Win / Linux to quickly
submit an issue or comment.

### Faster and more reliable 'git archive' downloads

Each project in GitLab has a 'download' button that lets you grab
a ZIP file with the contents of the repository at the revision you
are viewing. In GitLab 8.1 we have reduced the delay before the
download starts and optimized the way the ZIP file is generated and
sent to the user by shifting some of the work from the main GitLab
Rails application to
[gitlab-git-http-server](https://gitlab.com/gitlab-org/gitlab-git-http-server).

***Note:*** if you are not using the Omnibus packages and their built-in
NGINX settings this means that you will have to
[update your
NGINX/Apache settings](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/lib/support/nginx/gitlab#L116-132)
when upgrading to 8.1.

## GitLab Mattermost Update

Omnibus-GitLab packages are bundled with the latest version of [Mattermost](http://www.mattermost.org/).
Mattermost version 1.1.1 comes with a large number of improvements and
is even more integrated with GitLab.
Realtime notifications from GitLab can now be received by Mattermost,
using incoming webhooks.

The latest version of Mattermost also includes a large number of config changes.
If you have any custom configuration **make sure you read the
[Upgrade from v0.7 to v1.1 notes](https://github.com/mattermost/platform/blob/master/doc/install/Upgrade-Guide.md)
and make sure you check the
[latest config options available for GitLab Mattermost](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/files/gitlab-config-template/gitlab.rb.template#L665-790)**.

![Mattermost is looking great with its latest release](/images/8_1/mattermost.png)

Rocket Chat is still working on
[adding PostgreSQL compatibility](https://github.com/RocketChat/Rocket.Chat/issues/533)
and there is no estimated time when it will ship.

## Other changes

This release has more improvements, including security fixes. Please check out [the Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG) to see the all named changes.

***Update (2015-10-27):*** When we [released GitLab 8.0 last month], we promised
to automatically remove the satellites directory in 8.1. This seems to have
slipped our minds for the official 8.1 release, but we included it in the 8.1.2
patch release. See [the release post] for more information.

[released GitLab 8.0 last month]: https://about.gitlab.com/2015/09/22/gitlab-8-0-released/
[the release post]: https://about.gitlab.com/2015/10/27/gitlab-8-dot-1-dot-2-released/

## Upgrade barometer

If you are upgrading from GitLab 8.0 and none of your users are using
GitLab CI then you can perform the upgrade to 8.1 without downtime.
If your users _are_ using CI you need to stop GitLab before performing
the upgrade.

***Note:*** If you are upgrading from a GitLab version prior to 8.0 *and* you have CI enabled, you have to upgrade to GitLab 8.0 [first](https://about.gitlab.com/2015/09/22/gitlab-8-0-released/).

To see if your users are using GitLab CI go to
`gitlab.example.com/ci/admin/projects` and look if there are any
projects. No projects means no CI.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

***Note:*** If you've encountered an `/etc/init.d/ci-{SERVICE} does not exist!` error during the reconfigure run, use the package 8.1.0-ce.1 or newer.

- - -

## Installation

If you are setting up a new GitLab installation please see the
[download GitLab page](https://about.gitlab.com/installation/).

## Updating

Check out our [update page](https://about.gitlab.com/update/).

## Enterprise Edition

GitLab EE-only features like LDAP group support can be found in GitLab Enterprise Edition.
For a complete overview of EE please have a look at the [feature list of GitLab EE](http://www.gitlab.com/gitlab-ee/).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/pricing/).
No time to upgrade GitLab yourself?
A subscription also entitles you to our upgrade and installation services.

- - -

Thanks to [Cyndi](https://cyndicaviedes.com/) for the picture of the GitLab Inc team.
