---
title: "GitLab's 50th Release: 8.4"
date: 2016-01-22
categories: release
author: Job van der Voort
author_twitter: Jobvo
filename: 2016-01-22-gitlab-8-4-released.markdown
image_title: /images/8_4/building_gitlab.jpg
---

What better way to kick off a new year than with the 50th release of GitLab,
8.4!

No matter how you use GitLab, you're going to like this release.
Your diffs will look better than ever, you can browse through your
build artifacts in CI and search has been super powered with Elasticsearch
in EE!

We're extremely happy to receive some amazing contributions this release.
Kyungchul Shin contributed a fuzzy file finder to GitLab this release,
a much requested and truly MVP-worthy contribution.

Thanks Kyungchul Shin and congratulations on being
[this month's MVP](https://about.gitlab.com/mvp/)!

<!--more-->

<div style="width: 112px; margin: 0 auto;">
  <img src="/images/8_4/loading_tanuki2.gif" alt="GitLab's Tanuki is loading" />
</div>

## Super-powered Search with Elasticsearch (EE only)

If you have a lot of data, searching through everything in GitLab can
require a lot of number crunching, which can take a while.
Search is the last thing you want to wait for, which is why GitLab can now
leverage [Elasticsearch](https://www.elastic.co/products/elasticsearch)
to speed up those searches!

Elasticsearch is a flexible, scalable and powerful search service that lives
on its own server(s). Connecting it to GitLab is
[easy as pie][es].

Just like good-old search, Elasticsearch will search through your
issues, merge requests, milestones, comments, projects, repositories,
snippets and wikis.

> [Read about setting up Elasticsearch in our documentation][es]

## Artifacts browser

Since [GitLab 8.2](https://about.gitlab.com/2015/11/22/gitlab-8-2-released/),
you've been able to have CI output artifacts, which you could then
download as a single compressed file containing all artifacts of a build.

![Build artifacts browser in GitLab 8.4](/images/8_4/artifacts_browser.jpg)

With GitLab 8.4, you can now browse all your artifacts directly in GitLab's
interface and download files individually. GitLab does not extract the entire
compressed file when viewing and when downloading, it'll only extract the
requested file. This can save you a lot of storage space and makes it much
easier to work with large files or large volumes of artifacts, as you don't need
to download everything to get a single file.

> [Read the documentation on build artifacts browser](http://doc.gitlab.com/ce/ci/build_artifacts/README.html)

## Improved GitHub Importer

Want to move your projects from GitHub?
GitLab now imports your repositories, wikis, issues and pull requests from
GitHub!

On the new project page `/projects/new`, simply click on the GitHub link
and click to import any or all projects. GitLab will automatically take care
of the rest.

> [Read the documentation on the GitHub importer](http://doc.gitlab.com/ce/workflow/importing/import_projects_from_github.html)

## Fuzzy File Finder

The new Fuzzy File Finder lets you quickly navigate to a file by name
in the current repository without having to reach for the mouse!

![Find files easily with GitLab 8.4](/images/8_4/fuzzy_file_finder.gif)

You can quickly access the Fuzzy File Finder by pressing `t` anywhere
in a project.

_For more shortcuts, press `?` anywhere in GitLab!_

> [Read the documentation on the File finder](http://doc.gitlab.com/ce/workflow/file_finder.html)


## Code highlighting in Diffs

Diffs in GitLab now have highlighted syntax!

![Diffs are now highlighted in GitLab 8.4](/images/8_4/diff_highlighting.jpg)

![Diffs are now highlighted in GitLab 8.4](/images/8_4/diff_highlighting_2.jpg)

## Unsubscribe from Threads in Email

If you're getting notifications from issues or merge requests you're no
longer interested in, there is now a quick link in every email to
unsubscribe from that thread.


<div style="width: 400px; margin: 0 auto;">
  <img src="/images/8_4/unsub.jpg" alt="Quickly unsubscribe from a thread in GitLab 8.4" style="max-width: 400px" />
</div>

The link doesn't require you to sign in, so you can easily use it from your
phone, watch, or VR headset.

## Better links in other apps (Slack unfurls!)

When pasting a GitLab link in Slack, Twitter or Facebook,
it now automagically becomes a little bit prettier and informative
by making use of the Open Graph standard.

For instance, if you post a GitLab link in Slack, you now get some
extra information about the issue or merge request:

![Slack unfurls in GitLab 8.4](/images/8_4/unfurl.png)

We're looking forward to seeing pretty GitLab links all over the internet!

## CAS Support

GitLab user [tduehr](https://gitlab.com/u/tduehr) contributed
[CAS support](https://en.wikipedia.org/wiki/Central_Authentication_Service)
for GitLab, allowing you to use your CAS single sign-on server to sign
into GitLab.
Thanks, tduehr!

> [Read the documentation on using CAS with GitLab](http://doc.gitlab.com/ce/integration/cas.html)

## Performance Monitoring

We've said in
[multiple](https://about.gitlab.com/2016/01/15/making-gitlab-better-for-large-open-source-projects/)
[places](https://news.ycombinator.com/item?id=10923379) that improving
performance of GitLab.com is a big priority for us.
To give us more insights into this,
we've built performance monitoring into GitLab.

GitLab can now send performance data to an InfluxDB database, which in turn
can be connected to graphing software such as Grafana (shown below).

Data gathered by Performance Monitoring includes:

- The time it took to complete a transaction (a web request or Sidekiq job).
- The time spent in running SQL queries and rendering HAML views.
- The time spent executing Ruby methods.
- Ruby objects that have not yet been released by the garbage collector.
- System statistics such as the process' memory usage and open file descriptors.
- Ruby garbage collection statistics.

![Using Grafana to plot GitLab Performance Monitoring data](/images/8_4/perf_1.png)
![Using Grafana to plot GitLab Performance Monitoring data](/images/8_4/perf_2.png)

Right now Performance Monitoring still requires some setup to be
useful, but we're planning to bundle all the required software with
our EE Omnibus packages in the coming releases.

> [View the documentation on GitLab Performance Monitoring](http://doc.gitlab.com/ce/monitoring/performance/introduction.html)

## Filter Commit Messages

Want to quickly find a specific commit in the list of commits?
You can now quickly filter them by commit message, using the input on
top!

![Filter commits in GitLab 8.4](/images/8_4/commit_filter.gif)

Find the commit filter on the commits page of any of your projects.

## Emoji Picker Improvements

Now you can quickly search all available emoji!

![Search and find your favorite Emoji quickly in GitLab 8.4](/images/8_4/emoji_picker.gif)

The new Emoji picker also stores your favorite Emoji and is available
in any issue and merge request.

## Design Updates

Upgrading the looks and usability of GitLab is very important to us.
GitLab 8.4 introduces several design changes that will be built upon in
future releases.

Groups now look cleaner:

![Upgraded Group page for GitLab 8.4](/images/8_4/design_group.png)

And issues are also easier on the eyes, especially if you're using a smaller
window:

![Renewed issue design in GitLab 8.4](/images/8_4/design_issue.png)

We're working hard to improve the design of GitLab and put more emphasis
on content, while making everything easier to use. We'd love to get your
feedback on the latest changes.

## New CI features in API

The build artifacts browser is not the only enhancement in GitLab CI. With
GitLab 8.4 we are introducing new CI features in our API:

- [builds][] - list, cancel or retry any build in your project
- [build triggers][] - manage your project's [triggers][]
- [build variables][] - manage your project's variables

## Other changes

Some other notable changes include:

- Do some housekeeping and use `git gc` on your projects [right from your browser][gc-doc]
- [Enforce Two-factor authentication][2fa-doc] for all users on your GitLab
  instance
- Sign-in using your [Microsoft Azure account][azure-doc]

This release has many more improvements. Please check out
[the Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/8-4-stable/CHANGELOG)
to see the all named changes.

## Upgrade barometer

### Downtime required

This upgrade **requires downtime** as it brings a couple of migrations that are
updating a large set of records.

Most notably, the update iterates through all services, updating default values.
For instances that have LDAP enabled, it iterates through the whole user base
to update LDAP email settings.

On GitLab.com these migrations took around 5 minutes to complete. Do note that
GitLab.com doesn't have LDAP enabled so on instances that do have it enabled,
migration will take longer.

### Upgrading from 7.x or prior?

*Note* If you are upgrading from a GitLab version prior to 8.0 *and* you have CI enabled,
you have to upgrade to GitLab 8.0 [first](https://about.gitlab.com/2015/09/22/gitlab-8-0-released/).

### Default upgrade behavior

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

- - -

## Installation

If you are setting up a new GitLab installation please see the
[download GitLab page](https://about.gitlab.com/installation/).

## Updating

Check out our [update page](https://about.gitlab.com/update/).

## Enterprise Edition

The mentioned EE only features and things like LDAP group support can be found in GitLab Enterprise Edition.
For a complete overview please have a look at the [feature list of GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a
[subscription]( https://about.gitlab.com/pricing/).
No time to upgrade GitLab yourself?
A subscription also entitles you to our upgrade and installation services.

## Join us for a live Q & A

If you'd like to find out more about GitLab 8.4, [sign up to the webcast][webcast].
We'll give a live walk-through for this release and talk about what's coming up
next for GitLab. It's on Thursday, January 28, 5pm (17:00) UTC; 12pm EST; 9am PST.

[es]: http://doc.gitlab.com/ee/integration/elasticsearch.html "Elasticsearch documentation for GitLab 8.4 and up"
[gc-doc]: http://doc.gitlab.com/ce/administration/housekeeping.html "Housekeeping documentation"
[2fa-doc]: http://doc.gitlab.com/ce/security/two_factor_authentication.html "Two-factor authentication security documentation"
[azure-doc]: http://doc.gitlab.com/ce/integration/azure.html "Microsoft Azure integration documentation"
[builds]: http://doc.gitlab.com/ce/api/builds.html "Builds API documentation"
[build triggers]: http://doc.gitlab.com/ce/api/build_triggers.html "Build triggers API documentation"
[build variables]: http://doc.gitlab.com/ce/api/build_variables.html "Build variables API documentation"
[triggers]: http://doc.gitlab.com/ce/ci/triggers/README.html "Triggers documentation"
[webcast]: http://page.gitlab.com/Jan282016Webcast.html "Webcast: 8.4 Feature Walk-through"
