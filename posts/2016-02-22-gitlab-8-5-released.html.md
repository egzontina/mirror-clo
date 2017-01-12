---
title: "GitLab's fastest release ever: 8.5, with Todos and Geo"
date: 2016-02-22
categories: release
author: Job van der Voort
author_twitter: Jobvo
image_title: /images/8_5/header.jpg
---

If there is one GitLab release that you'll want to upgrade to as soon as
possible, it's this one.

GitLab 8.5 is faster. _A lot faster_. Not only have we increased performance
for everyone, getting to what is important is now super quick with Todos (yes,
_all_ important things for those of you that speak Spanish or Portuguese).

With GitLab 8.5 Enterprise Edition, we're also introducing the alpha of
GitLab Geo, which allows you to have a remote replicate of your entire
GitLab instance.

Once again, we received some amazing contributions this release.
One of these is the support for [relative URLs in Omnibus installations][rel],
which was one of the many contributions we received from Artem Sidorenko.

Thanks Artem Sidorenko and congratulations on being
[this month's MVP](https://about.gitlab.com/mvp/)!

[rel]: http://doc.gitlab.com/omnibus/settings/configuration.html#configuring-a-relative-url-for-gitlab
<!--more-->

## Performance for Scale

At GitLab, making sure everything runs smoothly with thousands of projects
has always been a priority. But with GitLab 8.5, we've raised the bar for
ourselves.

Average mean performance is up at least 1.4 times, up to 1.6 times for 99th
percentile response times. For slower pages, the response time has been improved
way beyond this.

For instance, displaying individual issues is now up to 3.5 times faster
for very large issues. The graph below shows you the slowest 95th percentile
response times for loading issues on GitLab.com before and after we deployed
the first release candidate of 8.5:

![Response times for single issues in GitLab 8.5](/images/8_5/issue_timings.png)

And here's a graph showing the overall response timings (per 30 minutes) from
10 to 12 February. The vertical arrow indicates the 8.5.0 RC1 deploy on
GitLab.com.

![Overall Response times in GitLab 8.5](/images/8_5/gitlab_timings.png)

There are many performance improvements that you will notice with 8.5.
Especially if you're running a very large server, this release will make
all your users happy.

Some notable performance notes are:

- Broadcast messages are cached, reducing the impact they have on page loading
  times [!2633](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2633)
- Performance of `Repository#empty?` and `Repository#has_visible_content?` has
  been improved and their output is cached, reducing project specific page
  (issues, project dashboard, etc) loading times by about 3 to 3.5 times. This
  was changed in [gitlab_git!62](https://gitlab.com/gitlab-org/gitlab_git/merge_requests/62)
  followed by [!2752](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2752)
- Caches for branch commit ahead/behind statistics are only flushed when needed.
  For example, when pushing to a non default branch only the statistics for
  said branch are flushed, whereas previously the statistics for all branches
  would be flushed. This was changed in [!2769](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2769)
- Performance of retrieving the issues that should be closed by a merge request
  has been improved in [!2625](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2625)
- Performance of Atom feeds has been greatly improved in
  [!2613](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2613),
  leading to a reduction of up to roughly 10 seconds per page load
  (depending on the amount of events involved)
- [!2859](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2859) changes
  the way the Git `core.autocrlf` option is set. Previously this would be
  written (regardless of whether it was already set) on every request. As of
  now, this is only set by the web editor/API before creating/updating files
  (as this is the only case where it's actually needed).
- 'Raw' file contents from Git repositories are served by gitlab-workhorse now,
  which prevents timeouts.
- GitLab no longer loads large Git blobs (e.g. binary files) into memory when
  browsing a Git repository. This prevents timeouts and memory leaks.

## Todos

GitLab is where you do your work, so being able to get started quickly is
very important. Therefore, we're now introducing Todos.

Todos is a chronological list of to-dos that are waiting for your input.
Whenever you're assigned to an issue or merge request
or have someone mention you, a new to-do is created automatically.

Then when you've made a change, like replying to a comment or updating an issue,
the to-do is automatically set to **Done**. You can also manually mark to-dos
as done.

![Todos in GitLab 8.5](/images/8_5/todos.png)

Todos has been designed to be as actionable as possible, so that you can focus
on what is important. Having a personal space to work from has been a long-time
request and we're looking forward to your feedback after having given it a go.

## GitLab Geo Alpha (EE)

If you have two or more teams geographically spread out,
but your GitLab instance is in a single location,
fetching large repositories can take a long time.

With GitLab Geo, you can have a secondary GitLab instance that mirrors your
main GitLab instance. Your Geo instance can be used for cloning and fetching
projects, in addition to reading any data. This will make working with large
repositories over large distances much faster.

![GitLab Geo available as Alpha in GitLab 8.5 EE](/images/8_5/geo.png)

With GitLab 8.5, we're offering GitLab Geo as an Alpha to all our Enterprise
Edition customers. Once GitLab Geo has left Alpha / Beta state, a special
license will be required to use it.

## GitLab Pages now support custom domains and custom TLS certificates (EE)

GitLab Pages was first introduced in GitLab EE 8.3, giving you the ability to
host your own static website in GitLab under a separate domain name.
[Dmitriy's blog](https://dzaporozhets.gitlab.io/) is hosted with it,
for example!

With GitLab 8.5 EE we're adding support for custom domains and TLS certificates.
You can even point multiple domains to GitLab and easily upload your own TLS
certificates.

To make it easier to set this all up, GitLab Pages now has its own
settings page in your projects at **Settings > Pages**.

![Pages new area](/images/8_5/pages_new_area.png)

You can add custom domains and certificates if this
functionality is enabled by your GitLab administrator:

![Pages domain list](/images/8_5/pages_domain_list.png)

The new functionality of GitLab Pages was made possible with the help of a new
HTTP server written in Go. We call
it the [GitLab Pages daemon][pages-daemon] and it supports dynamic certificates
through SNI and exposes pages using HTTP2 by default.

The upgrade path from GitLab 8.3 to 8.5 has changed quite a bit and we added
new comprehensive documentation how GitLab Pages work and the multiple ways to
set them up.

For GitLab.com users: Pages with CNAME and TLS support are fully live and
ready to use!

> [Learn how to setup your own page in our Gitlab Pages user documentation](http://doc.gitlab.com/ee/pages/README.html)

> [GitLab Pages administration documentation](http://doc.gitlab.com/ee/pages/administration.html)

[pages-daemon]: https://gitlab.com/gitlab-org/gitlab-pages

## Revert any Commit

If your motto is "Move fast and break things", you must be familiar with the
usage of `git revert`. In GitLab it's now much easier to use revert:
just press the button on any commit to create a merge request that reverts
it:

![Revert any commit in GitLab 8.5](/images/8_5/revert.png)

> [Read about reverting changes in our documentation](http://doc.gitlab.com/ce/workflow/revert_changes.html)

## Updated Issue Sidebar

We created the issue sidebar so we could free up the most important content
from other interface elements. With GitLab 8.5 we're doing this in a
smarter, prettier, and more accessible way:

![Updated Issue Sidebar in GitLab 8.5](/images/8_5/sidebar1.png)

To focus on your content, fold it in:

![Updated Issue Sidebar in its folded state in GitLab 8.5](/images/8_5/sidebar2.png)

Besides the sidebar, we've updated many things, big and small, in the interface.
Expect more improvements over the coming releases.

## Labels in Milestone View

We want to make GitLab the best place to manage your projects,
whether they are
[open source](https://about.gitlab.com/2016/01/15/making-gitlab-better-for-large-open-source-projects/) or not.

To get a better overview of a milestone, we're now showing labels in the
milestone view:

![See labels in Milestones in GitLab 8.5](/images/8_5/milestone.png)

> [Read about milestones in our documentation](http://doc.gitlab.com/ee/workflow/milestones.html)

## Render SVGs in Diffs

As big fans of SVGs ourselves, we made it possible to view rendered SVGs
in diffs:

![Rendered SVG in GitLab 8.5](/images/8_5/svg.png)

## Markdown in Broadcast messages

When broadcasting important messages to all users on your instance,
it can be useful to include formatting or links. That's possible now
with Markdown support for broadcast messages.

![Broadcast messages with markdown in GitLab 8.5](/images/8_5/broadcast_md.gif)

## Highlighted File Renames

Small changes can be great too!
We now highlight file renames in diffs:

![See differences on file renames in Gitlab 8.5](/images/8_5/filenames.png)

## Sort by Votes

You can now easily sort issues by votes!
This should make it easier to find popular or important issues.

![Sort by votes in GitLab 8.5](/images/8_5/votes.png)

## Erase Build Content in CI

Accidentally exposed some information in your build logs or in a
faulty build artifact in CI? You can now delete artifacts
and build traces from CI.

![Erase builds in GitLab 8.5](/images/8_5/erase_builds.png)

## New CI features in API

Every month we strive to expose more and more CI features to our API. With
GitLab 8.5 here's what's new:

- [runners](http://doc.gitlab.com/ce/api/runners.html) - enable, disable, edit
  and see the details of a runner
- [builds artifacts](http://doc.gitlab.com/ce/api/builds.html#get-build-artifacts) -
  download the artifacts

---

## Other changes

This release has more improvements, including security fixes. Please check out [the Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG.md) to see all the named changes.

### Updates in the omnibus-gitlab package

As GitLab gets improved every release, so does the omnibus-gitlab package.
You can see the changes that package receives for every release in the
[omnibus-gitlab CHANGELOG](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/CHANGELOG.md).

In this release there are some major changes in the bundled software:

* Nginx is updated from version 1.7.12 to 1.9.10
* Nginx spdy protocol was replaced with http2
* OpenSSL is updated from version 1.0.1r to 1.0.2f

### Mattermost 2.0

[Mattermost 2.0](http://www.mattermost.org/open-source-localizable-slack-alternative-mattermost-2-0/)
ships with GitLab 8.5 and includes localization support,
Spanish-language translation, and API support for GitLab single-sign-on in iOS
and Android apps.

Mattermost can now also skip 1 major build version. This means GitLab Mattermost
upgrades from GitLab 8.3 to 8.5 without needing to upgrade to 8.4.
The new 2.0 iOS app for Mattermost with GitLab SSO requires Mattermost server
2.0 and higher due to a breaking change in mobile API incompatible with
Mattermost 1.x.

---

## Upgrade barometer

A migration affecting projects having a path ending in '.atom' has been added,
as they are no longer supported. This migration updates both the database and
the filesystem and previous versions of this migration have proven to be fragile.

If you have no projects with paths ending in '.atom' in your database (most likely, you don't)
you can perform this upgrade online. If you do have them, we recommend to take downtime.
You can find the current number of affected database records with the following command:

```
sudo gitlab-rails runner "puts Project.where(%q{path LIKE '%.atom'}).count"
```

*Note* If you are upgrading from a GitLab version prior to 8.0 *and* you have CI enabled, you have to upgrade to GitLab 8.0 [first](https://about.gitlab.com/2015/09/22/gitlab-8-0-released/).

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

_Note to early adopters: the 8.5.0 release candidates recommended using Ruby 2.2
but we have found
[some issues](https://gitlab.com/gitlab-org/gitlab-ce/issues/13514).
We recommend everybody to keep using Ruby 2.1 for now._


- - -

## Installation

If you are setting up a new GitLab installation please see the
[download GitLab page](https://about.gitlab.com/installation/).

## Updating

Check out our [update page](https://about.gitlab.com/update/).

## Enterprise Edition

The mentioned EE only features and things like LDAP group support can be found in GitLab Enterprise Edition.
For a complete overview please have a look at the [feature list of GitLab EE]( https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a
[subscription]( https://about.gitlab.com/pricing/).
No time to upgrade GitLab yourself?
A subscription also entitles you to our upgrade and installation services.

- - -

## Join us for a live demo and Q+A

[Sign up to our webcast](http://page.gitlab.com/Feb252016Webcast_LandingPage.html).
[Job](https://twitter.com/Jobvo/) will give a live walkthrough for GitLab 8.5
and he'll talk about GitLab Flow.
It's on Thursday, February 25th, 5pm (17:00) UTC; 12pm EST; 9am PST.
Can't make that time?
[Register](http://page.gitlab.com/Feb252016Webcast_LandingPage.html) anyway,
and we'll send you the recording.
