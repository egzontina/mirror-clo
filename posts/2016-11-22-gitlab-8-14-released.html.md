---
title: "GitLab 8.14 Released with Time Tracking Beta and Chat Commands"
categories:
author: Job van der Voort
author_twitter: Jobvo
image_title: /images/8_14/pic.jpg
---

You're doing code review of a new feature and wonder how it'll actually
feel, look and work when it's live. Yesterday, you had to sacrifice your
local development environment's state, checkout the remote branch, run
migrations, and then spin up the entire development environment.
Today, you can just go to GitLab and click the link in
the merge request to play with a fully functional, live environment.

<!--more-->

Maybe you have some feedback on what you saw and start talking with your
colleague on chat. Rather than having to communicate on who moves the result to
issues, you just create an issue directly from chat.
You can immediately add a time estimate to the issue
and anyone peeking at the cycle analytics will see the new issue come by and
over time, move to production, giving you feedback on where things might get
stuck.

You can do all of the above and much more with GitLab 8.14, today. Time
tracking, Review Apps, Chat commands, Cycle Analytics improvements and much
more.

This month's Most Valuable Person ([MVP](https://about.gitlab.com/mvp/)) is Toon Claes. Toon contributed the button to delete all merged branches,
a great addition to GitLab.
Thanks Toon Claes!

{::options parse_block_html="true" /}

<i class="fa fa-gitlab" style="color:rgb(107,79,187); font-size:.85em" aria-hidden="true"></i>&nbsp;&nbsp;
Tune in on Nov. 30 for our 8.14 release webcast with a live demo of Review Apps and Time Tracking for EE! [Register here](https://page.gitlab.com/20161124_ReviewAppsWebcast_LandingPage.html)!
&nbsp;&nbsp;<i class="fa fa-gitlab" style="color:rgb(107,79,187); font-size:.85em" aria-hidden="true"></i>
{: .alert .alert-webcast}

## Time Tracking Beta (EE)

Whether you're a contractor that needs to keep track of their time,
or you're managing time spent on issues and projects,
time tracking has traditionally been a painful experience: You have various
systems to keep track or log your time and these never seem to fit in your
day-to-day workflow.

You can now track your time right where you're working, with Time Tracking
in GitLab.

With Time Tracking, you're able to set estimates for how much time is necessary
for a particular issue. All you have to do is use a new slash command,
which can be entered in the issue description or a comment:

```
/estimate 6h
```

You can adjust this at any time with the same command. Once you've spent time
on an issue, you can log this simply with:

```
/spend 3h
```

You'll see this reflected in the interface.

![Time Tracking Beta in GitLab 8.14](/images/8_14/time.gif){: .shadow}

Time Tracking is made available as trial to all our Enterprise Edition
customers during the beta period,
[after which it becomes available as a paid Product][paid-product-issue].

We're interested in hearing how we can improve time tracking to fit your
workflow. Let us know by [creating an issue][create-tt-issue] or below in the comments.

Some things we're thinking about: [reporting][reporting], [an API][tt-api],
[Time Tracking in Issue Boards][tt-issue-boards] and [others][other-issues].

> [Read the docs on how to use Time Tracking in GitLab](https://docs.gitlab.com/ee/workflow/time_tracking.html)

[paid-product-issue]: https://gitlab.com/gitlab-org/gitlab-ee/issues/1264
[reporting]: https://gitlab.com/gitlab-org/gitlab-ee/issues/1271
[tt-api]: https://gitlab.com/gitlab-org/gitlab-ee/issues/1228
[tt-issue-boards]: https://gitlab.com/gitlab-org/gitlab-ee/issues/1265
[other-issues]: https://gitlab.com/gitlab-org/gitlab-ee/issues?label_name%5B%5D=time+tracking
[create-tt-issue]: https://gitlab.com/gitlab-org/gitlab-ee/issues/new

## Chat Commands (experimental)

It seems like communication has moved from the conference room to the online
chatroom in the last few years. In particular, collaboration and idea generation
seem to happen here, and that's an important part of the
[idea-to-production vision](/2016/09/13/gitlab-master-plan/#the-master-plan)
that we aim to capture with GitLab. With Chat Commands you can now bridge the
gap between chat and GitLab's repositories, issue tracker, and CI/CD pipelines
quickly and easily.

![Chat Commands in GitLab 8.14 with Mattermost](/images/8_14/chat1.gif){: .shadow}

With this first iteration, you can quickly create or view an issue, for
instance, using this to make an issue with the title and description already filled in:

```
/gitlab issue create Even Better Issue Boards
Let's make Issue boards _even_ better!
```

You can also embrace ChatOps and trigger deploys to production (using the
proper identity and permissions of the user):

```
/gitlab deploy staging to production
```

This iteration supports Mattermost, which ships with GitLab Omnibus. Slack
support is [coming soon](https://gitlab.com/gitlab-org/gitlab-ce/issues/22182).
The command set is limited, but we're [looking to add
more](https://gitlab.com/gitlab-org/gitlab-ce/issues/24768) soon and would love
your feedback.

> [Read the documentation on Mattermost Slash Commands](https://docs.gitlab.com/ce/project_services/mattermost_slash_commands.html)

## Review Apps

Review Apps are the future of reviewing work. Rather than just looking at code,
Review Apps will serve you with a fully functioning environment in which your
app is running, ready for any kind of testing, trying or poking.

We initially offered experimental support for Review Apps in GitLab 8.12, and
improved it in the 8.13, but today we're shipping the last bit to call it
"complete".

Now with Review Apps properly set up, an app will spin up automatically
for each branch and be destroyed automatically when the branch is removed from
GitLab. We're [using it with this blog](https://gitlab.com/gitlab-com/www-gitlab-com/blob/master/.gitlab-ci.yml#L33-71), and it's awesome. This feature is so exciting, there's a whole other blog
post about it.

> [Read the blog post introducing review apps](/2016/11/22/introducing-review-apps/)

> [Read the documentation on Review Apps](https://docs.gitlab.com/ce/ci/review_apps/)

## Cycle Analytics Events

With Cycle Analytics you get actionable feedback on how fast your ideas are moving to product and where they might be getting stuck. This can seem a little abstract, so to make it more obvious what is happening, we'll now show you the latest events in each stage.

![Improved Cycle Analytics in GitLab 8.14](/images/8_14/cycle_events.png)

This should make it easier to get an overview of what is happening in each
stage, but also to quickly jump in and see if you can move things forward
faster.

> [Read the documentation on Cycle Analytics](https://docs.gitlab.com/ce/user/project/cycle_analytics.html)

## Prevent merge until Review is done

You shouldn't merge code before all tests have passed and review is done.
The first was enforceable for a while in GitLab, but the second not yet.

With GitLab 8.14, you can now prevent merges until all discussions on a merge
request have been resolved. This makes it impossible to miss those last
comments on the bottom of the page (even if we didn't have that handy widget on
top) and make sure only code that has been checked and verified makes it to
production.

![Prevent merge until review is done in GitLab 8.14](/images/8_14/dis1.png){: .shadow}

Enable this option in the project settings.

![Prevent merge until review is done in GitLab 8.14](/images/8_14/dis2.png)

Thanks to Rodolfo Arruda for contributing this awesome feature!

> [Read the documentation on merge request discussions](https://docs.gitlab.com/ee/user/project/merge_requests/merge_request_discussion_resolution.html)

## Delete all Merged Branches

Toon Claes contributed an amazingly obvious, yet dubiously missing feature: a
single button to quickly delete all merged branches in GitLab.

We'll make sure to confirm your choice and then quickly set off a process to do
as requested. Find the button under your project's **Repository ➔ Branches**.

![Quickly delete all merged branches in GitLab 8.14](/images/8_14/delete_mr.png){: .shadow}

Deleting all merged branches will not delete any of your
protected branches.

Thanks Toon Claes!

## Subscribe to Group Labels

We've introduced the convenient Group Labels in GitLab 8.13.
You can now finally subscribe to them, so you get notified on things that
matter to you, across entire groups. For instance, get notified whenever
a new issue is made with the `customer` label, so you'll get a good overview
of customer issues across all projects in a group.

## Better Pipeline emails

Now when a pipeline fails, we'll email you what went wrong, so you know whether
to simply retry a build, or call for all-hands-on-deck, without having to dive
into the logs immediately.


![Better pipeline notifications in GitLab 8.14](/images/8_14/emails.png)

## JIRA integration improvements

We know many of you use JIRA intensively. We're working very hard on
improving GitLab's integration with it. Below are some of the improvements
we've made this release. We're interested in hearing what else.

> [Read the revamped documentation on JIRA integration](https://docs.gitlab.com/ce/project_services/jira.html)

### Remote issue links to JIRA

To make it super easy how a JIRA ticket relates to commits in GitLab, now
whenever you mention a JIRA ticket in a commit or merge request,
we'll add it to the remote issue links in the ticket. You can write
that it `Fixes` a JIRA ticket or just mention it and we'll make sure
it appears correctly.

![Remote Issue Links to JIRA with GitLab 8.14](/images/8_14/jira.png){: .shadow}

Related MR: <https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7413>

### A more silent GitLab in JIRA

When you setup the JIRA service within GitLab, by default, every commit and
merge request in GitLab that referenced a JIRA issue created a comment in this
issue in JIRA. Some people like having the complete details of what's going on,
others prefer this to be more silent.

With GitLab 8.14, you can now disable the creation of comments when referencing
a JIRA issue in a commit or in a merge request.

## Improved Looks!

GitLab also got prettier and easier to use with 8.14, some highlights below:

You can now _see_ who you are mentioning:

![](/images/8_14/mention.png){: .shadow}

Pipelines and the meta information are looking even better than they did:

![](/images/8_14/pipes.png){: .shadow}

We now show you environment information on the build page:

![](/images/8_14/env_info.png){: .shadow}

Pipelines will now show whether specific builds are skipped:

![](/images/8_14/pipes2.png){: .shadow}

And we made it easier to see what is left in the current pipeline:

![](/images/8_14/pipes3.png){: .shadow}

## Improved Accessibility

Our amazing UX and frontend teams have been working hard on improving
the accessibility of GitLab. We've made a few changes worth highlighting this month:

- We've added a 'Skip to Content' button when tabbing, This allows you
to reach the content faster and skip navigation items.
- All dropdowns, buttons and anchors now have focus states
- We've increased the contrast between background and anchors

We're always interested in hearing how we can improve GitLab's accessibility
further.

## GitLab Mattermost 3.5

GitLab 8.14 includes [Mattermost 3.5](https://about.mattermost.com/mattermost-3-5/),
an [open source Slack-alternative](https://about.mattermost.com) whose newest
release offers improved performance on mobile and web through reduced loading
times, mobile UI improvements and faster server-side processing, Minio as a
self-hosted S3-alternative to local file storage, Russian language translation,
favorite channels and much more.

This version also includes [security updates](http://about.mattermost.com/security-updates/)
and upgrade from earlier versions is recommended.

## GitLab Runner 1.8

We are also releasing GitLab Runner 1.8 today. Most interesting changes:

- Add initial Prometheus metrics server to runner manager [!358](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/358)
- Add support for docker registries on non standard ports [!376](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/376)
- Use correct constant for kubernetes resource limits. [!367](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/367)
- Add PullPolicy config option for kubernetes [!335](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/335)
- Fix/unplug stalled endpoints [!390](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/390)
- Fix {Bash,Cmd,Ps}Writer.IfCmd to escape its arguments [!364](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/364)

## Support for private container registries in GitLab CI builds

In GitLab 8.14 and GitLab Runner 1.8 we've improved support for private docker images.

From now on you can use private/protected images stored in GitLab's Container
Registry automatically, without any changes. GitLab will send registry
credentials with build data, and Runner will use them to authorize docker pull
requests.

You can also use `DOCKER_AUTH_CONFIG` Secure Variable to add credentials
for other private registries. Thanks to this you can use any image from any registry - public or private - which is accessible from build's host, to be a base of your build or a service used by it.

Runner 1.8 fixes also the mechanism that is generating aliases from service
name, when registry is available on non standard port.

You can read more about private container registries support in [GitLab Runner's configuration](https://docs.gitlab.com/runner/configuration/advanced-configuration.html#using-a-private-container-registry) documentation.

## Performance Improvements

* Commits that are pushed are now processed in a separate Sidekiq worker: [!6802](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6802)
* The authorised projects for a user are now stored in a dedicated database table. This list is updated whenever you are granted access to a new project, project access has been removed, etc: [!6839](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6839)
* Defer saving of project services to reduce database queries: [!6958](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6958)
* Getting the merge requests that close an issue now uses a cache: [!6996](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6996)
* Queries to get events have been optimised by removing the default ORDER BY where possible: [!7130](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7130)
* GitLab can now limit the amount of Sidekiq workers per queue to a certain percentage: [!7292](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7292)
* An index has been added for `project_import_data.project_id` to improve finding project import data: [!7316](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7316)
* Certain database associations are now eager loaded on the merge requests and issues index pages: [!7564](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7564)
* Refreshing of caches upon a push has been improved. Previously GitLab would refresh all caches, starting with 8.14 it will only refresh the caches of data that has been changed: [!7360](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7360)

## Omnibus GitLab package changes

### Redis in HA configuration

In GitLab 8.11 [we've announced](https://about.gitlab.com/2016/08/22/gitlab-8-11-released/#redis-sentinel-support)
experimental Redis Sentinel support.
We've improved this further and also introduced ways of configuring Redis HA, all within the package.

With Omnibus GitLab 8.14 Enterprise Edition package, you can fully configure
Redis in Highly Available configuration which also includes configuring
Redis Sentinel. This is a step forward in the direction of having a
[fully HA ready Enterprise Edition package](https://gitlab.com/gitlab-org/gitlab-ee/issues/77).

When using the Community Edition package, Redis Sentinel needs to be
installed and configured manually separately.

> [Read more about Redis HA setup in our docs](https://docs.gitlab.com/ee/administration/high_availability/redis.html)

### Omnibus GitLab packages on OpenSUSE

With GitLab 8.14 we are introducing omnibus-gitlab packages for OpenSUSE 13.2 and 42.1.
The packages are served through zypper repositories from our package server.

Go to [our download page](https://about.gitlab.com/downloads/) for installation
details.

### Package repositories for Oracle Linux and Scientific Linux

Omnibus GitLab packages for Oracle Linux and Scientific Linux have been supported
for a long time however, they required a manual change in the yum repo list.
Starting with GitLab 8.14, this is no longer necessary and you can use the directions
from [our download page](https://about.gitlab.com/downloads/) without any alterations.

### Further Omnibus Package changes

* Packaged NGINX is upgraded to 1.10.2
* Packaged Redis is upgraded to 3.2.5
* Multiple configuration options got introduced in the [gitlab.rb](https://gitlab.com/gitlab-org/omnibus-gitlab/compare/8-13-stable...8-14-stable#diff-25) file
* See omnibus-gitlab [Changelog](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/8-14-stable/CHANGELOG.md) for more details

## Other changes

This release has more improvements, including security fixes. Please check out
[the changelog] to see all the named changes.

[the changelog]: https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG.md

## Upgrade barometer

To upgrade to GitLab 8.14, about 15 to 30 minutes downtime is required depending
on the size of your instance. See below for details.

* The column `application_settings.repository_storage` has been renamed, this requires downtime but takes very little time
* Some indexes with stricter constraints are being added and they require corresponding code changes to be deployed, this requires downtime
* The subscriptions data is being migrated in a way that can't be done online, this process may take a few minutes
* Project records with invalid visibility level are fixed, this can take a few minutes and requires downtime

### Note

We assume you are upgrading from the latest version. If not, then also consult the upgrade barometers of any intermediate versions you are skipping.
If you are upgrading from a GitLab version prior to 8.0 *and* you have CI enabled, you have to upgrade to GitLab 8.0 [first](https://about.gitlab.com/2015/09/22/gitlab-8-0-released/).

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

----

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

----
