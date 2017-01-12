---
title: "GitLab 8.13 Released with Multiple Issue Boards and Merge Conflict Editor"
categories:
author: Job van der Voort
author_twitter: Jobvo
image_title: /images/8_13/header.jpg
---

{::options parse_block_html="true" /}

<p  class="alert alert-orange" style="background-color: rgba(252,163,38,.3);
    border-color: rgba(252,163,38,.3); color: rgb(226,67,41) !important; text-align: center;">
    <i class="fa fa-gitlab" style="color:rgb(226,67,41); font-size:.85em" aria-hidden="true"></i>
    &nbsp;&nbsp;
    [Join us for our next release webcast](https://page.gitlab.com/20161027_8.13ReleaseWebcast_LandingPage.html){: .purple} on October 27 to
    learn more about GitLab 8.13!
    &nbsp;&nbsp;<i class="fa fa-gitlab" style="color:rgb(107,79,187); font-size:.85em" aria-hidden="true"></i>
</p>

We're [traveling around the world][world-tour] and having the pleasure
of meeting so many of you. This month we're proud to present many
changes that have been highly requested both in person and on [our issue tracker][issues-ce].

You're now able to create multiple issue boards and quickly create issues from
them. In addition, no merge conflict is safe anymore from being solved, as
you can now edit the conflict right in GitLab. We've made it
even easier to track what code is running where and get you immediate feedback
with improved Cycle Analytics.

This month's Most Valuable Person ([MVP](https://about.gitlab.com/mvp/)) is
Marc Siegfriedt for his contribution of the multi-file commit API endpoint.
Marc showed patience and determination getting this complex merge request
merged.
Thanks Marc!

[world-tour]: https://about.gitlab.com/2016/09/28/world-tour-amplify-your-code/
[issues-ce]: https://gitlab.com/gitlab-org/gitlab-ce/issues

<!--more-->

## Multiple Issue Boards (EE)

You can now have multiple Issue boards on a single project in GitLab
Enterprise Edition.

![Multiple Issue Boards in GitLab 8.13](/images/8_13/m_ib.gif)

This allows you to have multiple workflows, as issues are immediately updated
with the corresponding labels. For instance, create a board for the whole
organisation and one for only the UX team: an issue will be updated across
boards if the UX team moves it from UX to Frontend.

We're looking forward to see how you'll use multiple issue boards.

## New Issue from the Issue Board

While we're on the subject, you can now quickly add a new issue to a list:

![Create a new issue from the Issue Board in GitLab 8.13](/images/8_13/new_issue.gif)

Of course, it'll immediately be labeled correctly.

## Merge Conflict Editor

In [GitLab 8.11][8-11], we introduced merge conflict resolution,
allowing you to choose between _our_ and _their_ changes when attempting
to solve a conflict.

With GitLab 8.13, we've expanded the conflict resolution, allowing you
to edit the conflict right inside GitLab. This means you can now solve almost
any conflict without leaving your browser!

![Solve Merge Conflicts through the editor in GitLab 8.13](/images/8_13/inlinemergeconflictresolution.gif)

We believe this step is another in the direction of making merge conflict
headaches a thing of the past.

[8-11]: https://about.gitlab.com/2016/08/22/gitlab-8-11-released/

## Group Labels

With Issue Boards and label prioritization, managing labels across projects
can be a pain.
With GitLab 8.13 you're now able to create Group Labels. They work exactly
the same, but they are immediately available to all projects in the group.

![Group level labels in GitLab 8.13](/images/8_13/group_labels.png)

Currently you're required to make the group labels from the page of your
Group. We'll be adding the ability to change project labels into group labels
in a future release.

## Ability to stop Review Apps

Review apps give you the power to preview your changes in a live,
fully functional environment. You can now actually destroy these
dynamic environments straight from GitLab, whenever you don't need them anymore. Note this is a manual action, and automatic stopping of review apps when a branch is deleted is [scheduled for next release](https://gitlab.com/gitlab-org/gitlab-ce/issues/23218).

![Stop dynamic environments (review apps) in GitLab 8.13](/images/8_13/review_app.png)

## Ref per Deployment

To quickly check out the currently deployed commit, GitLab now
stores a ref in the repository. This means that, [after configuring this locally](https://docs.gitlab.com/ce/ci/environments.html#checkout-deployments-locally),
a single `git fetch` is all you need to check out the code that runs
in production.

## Pipelines for Commits

We now show related pipelines on the commit page, so you can
quickly see what happened with this particular commit.

![Pipelines for commits in GitLab 8.13](/images/8_13/commit_pipeline.png)

## Cycle Analytics Improvements

Previously, Cycle Analytics would only measure what's been shipped to production
in a given time range. We've changed this behavior and now measure
everything that happened in this time range.

Only the staging and production
stages will show what's actually been shipped to production, of course.

## Assign issues to MR author

Did you reference some issues in your commits or merge request,
but didn't assign them to yourself, or they aren't assigned to the merge request
author? There's now a quick link to do this:

![Quickly assign](/images/8_13/assign_yourself.png)

## Restrict the visibility of a project's repository

GitLab now does so much more, the repository doesn't have to be the
point of focus anymore. In fact, you might not use it at all! For that reason,
you can now disable or restrict access to the repository of any project.

If you restrict access, only project members can access the repository.
This allows you to run a public issue tracker on an otherwise private project.

![Project repository visibility](/images/8_13/restrict_access.png)

## /wip Slash Command

You can now use the [amazing slash commands][slash-cmds] to quickly
change the status of a merge request to/from Work-In-Progress (WIP).

Just type `/wip` and submit your comment or merge request description!

![WIP using slash commands in GitLab 8.13](/images/8_13/wip.gif)

[slash-cmds]: https://docs.gitlab.com/ce/user/project/slash_commands.html

## Debug tracing for CI

By default, GitLab Runner hides most of the details of what it is doing when
processing a job. This behavior keeps build traces short, and prevents secrets
from being leaked into the trace unless your script writes them to the screen.

If a job isn't working as expected, this can make the problem difficult to
investigate; in these cases, you can enable debug tracing in `.gitlab-ci.yml`.
Available on GitLab Runner v1.7+, this feature enables the shell's execution
trace, resulting in a verbose build trace listing all commands that were run,
variables that were set, etc.

Before enabling this, you should ensure builds are visible to team members
only. You should also erase all generated build traces before making them
visible again.

To enable debug traces, set the CI_DEBUG_TRACE variable to true:

```
job1:
  variables:
    CI_DEBUG_TRACE: "true"
```

> [Read more in our documentation on Debug tracing](https://docs.gitlab.com/ce/ci/variables/README.html#debug-tracing)

## Disable Git operations for CI

To speed up builds that don't require interaction with the repository,
you can disable Git operations now. Just specify the Git strategy in your
`.gitlab-ci.yml`:

```
variables:
  GIT_STRATEGY: none
```

> [Read more about Git Strategies for CI in our docs](https://docs.gitlab.com/ce/ci/yaml/README.html#git-strategy)

## Deployment date on Merge Request

Small, yet sweet change: We now show you right in the merge request when a deploy happened.

![See when a deploy happened in GitLab 8.13](/images/8_13/deployed_ago.png)

## GitLab Runner

We are also releasing GitLab Runner 1.7 today. Most interesting changes:

* Use Go 1.7 - which makes Runner usable on Mac OS X Sierra [!323](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/323)
* Introduce GIT_STRATEGY=none [!332](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/332)
* Add OffPeak support for autoscaling [!345](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/345)
* Introduce a variable to enable shell tracing on bash, cmd.exe and powershell.exe [!339](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/339)
* Try to load the InCluster config first, if that fails load kubectl config [!327](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/327)
* Godep: update github.com/Sirupsen/logrus to v0.10.0 [!344](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/344)
* Use git clone --no-checkout and git checkout --force [!341](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/341)
* Make runner name lowercase to work with GCE restrictions [!297](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/297)
* Add per job before_script handling for exec command [!355](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/355)
* Prevent caching failures from marking a build as failed [!359](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/359)
* Improve registration behavior [!356](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/356)

To see the full list of all changes please read [the Runner's CHANGELOG file](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/v1.7.0/CHANGELOG.md).

## GitLab Mattermost

GitLab 8.13 includes [Mattermost](https://about.mattermost.com/), an open source Slack-alternative for web, PC and phone with [over 700 app integrations via Zapier](https://about.mattermost.com/mattermost-3-4/).
New integrations this month [now support connecting to Slack, Gitter, XMPP, and IRC](https://about.mattermost.com/new-community-integrations-for-open-source-slack-alternative-as-mattermost-prepares-for-3-5/).
Mattermost now [releases 6 times a year](https://about.mattermost.com/changing-release-cycle-to-bi-monthly-from-monthly/) and new updates ship with GitLab in alternate months.


## API additions

This release contains several additions to the API. See below for more details.

### Multi-file commit

Thanks to the MVP of this month, Marc, you can now commit multiple
files at once through the API.

> [See the API docs on committing multiple files](https://docs.gitlab.com/ee/api/repository_files.html#update-existing-file-in-repository)

### Issue Board

Andre Guedes contributed a full API for Issue Boards. Thanks Andre!

### User contribution events

You can now get user contribution events through the api.

> [API reference on User contribution events](https://docs.gitlab.com/ce/api/users.html#get-user-contribution-events)

### Visible projects

Thanks to Ben Boeckel, you can now retrieve all projects that are visible
to you, through the API.

> [Read the projects API docs](https://docs.gitlab.com/ce/api/projects.html#list-projects)

## Performance Changes

CE changes:

* Performance of the group milestones page has been improved: [!6457](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6457)
* The number of queries executed when processing Markdown references has been decreased: [!6457](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6457) and [!6545](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6545)
* Sidekiq now uses a connection pool when using the Rails cache: [!6468](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6468) and [!6657](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6657)
* CI runners less frequently update the `ci_runners` table, leading to less database load: [!6537](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6537)
* The number of queries executed when pushing commits has been reduced slightly: [!6680](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6680)
* Trending projects are now pre-calculated on a daily basis and limited to the top 100 projects. This improves performance of the trending projects page: [!6749](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6749)
* When creating a new merge request the diffs are loaded asynchronously: [!5844](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5844)
* Resetting a project's last activity timestamp no longer relies on Redis leases, reducing the time it takes to refresh this timestamp: [!6678](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6678)
* The secret token used for gitlab-shell and the API is now stored in memory, instead of being read from disk on every API request: [!6599](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6599)
* The number of queries used for checking project policies has been reduced: [!6442](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6442)
* The worker used for expiring build artifacts now schedules jobs more efficiently and uses more efficient SQL queries: [!6732](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6732)
* Updating merge requests upon a push is now performed using a dedicated Sidekiq worker: [!6767](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6767)
* CI pipeline hooks are now updated asynchronously: [!6824](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6824)
* CI pipeline metrics are now updated using a Sidekiq worker: [!6896](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6896)
* Performance and memory usage of the GitHub importer has been improved: [!6552](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6552)
* Render timings of award emoji URLs have been improved: [!6848](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6848)
* When creating a project we immediately create a corresponding `project_features` row, instead of checking for this (and creating the row if needed) whenever we query a project from the database. This reduces the number of queries to retrieve a project from 2 back to 1: [!6908](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6908)
* CI pipeline commits are only updated once a pipeline is created, instead of doing so upon every update: [!6986](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6986)
* CI pipeline durations are only updated at the end of a pipeline, instead of doing so at every state transition: [!6987](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6987)
* Updating of project caches now occurs at most every 15 minutes per project.  This may lead to stale statistics (e.g. commit counts) but can significantly reduce disk load: [!7017](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7017)
* Sidekiq now uses separate queues for a wide variety of workers: [!7006](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7006)
* CI pipeline jobs are scheduled in a smarter way, preventing multiple jobs using the same parameters from being performed at the same time: [!7005](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7005)
* Cache markdown fields in the database [!6095](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6095)

EE changes:

* GitLab usage data is now cached: [!779](https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/779)

Changes to gitlab-shell:

* gitlab-shell now measures the time it takes to perform certain steps and logs these to the gitlab-shell log file using the DEBUG log level: [!98](https://gitlab.com/gitlab-org/gitlab-shell/merge_requests/98) and [!100](https://gitlab.com/gitlab-org/gitlab-shell/merge_requests/100)
* Tracing of Git performance can now be enabled using an environment variable: [!91](https://gitlab.com/gitlab-org/gitlab-shell/merge_requests/91)
* Moving repositories between shards has been improved: [!97](https://gitlab.com/gitlab-org/gitlab-shell/merge_requests/97) and [!96](https://gitlab.com/gitlab-org/gitlab-shell/merge_requests/96)

## Omnibus GitLab package changes

* Jemalloc is now used as a default memory allocator which should decrease the
memory footprint.
* Bundled NGINX now has a Status endpoint, enabled by default. Thanks to Luis Sagastume!
* Multiple configuration options got introduced in the [gitlab.rb file](
https://gitlab.com/gitlab-org/omnibus-gitlab/compare/8-12-stable...8-13-stable#diff-34)

## Other changes

This release has more improvements, including security fixes. Please check out [the Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG.md) to see the all named changes.

## Upgrade barometer

This release contains a significant amount of migrations that require downtime.
Administrators should prepare for at least 30 minutes of downtime. Small
installations (e.g. those with a few hundred projects) should be able to
complete the migration process in 5-10 minutes.

Keep in mind that these times are estimates,
they may vary between installations.

Among the migrations are migrations that:

* add foreign keys to existing tables
* move Sidekiq jobs from one queue to another
* remove duplicate labels
* fix label priorities
* perform other data cleanups

### Sidekiq Queues

This release includes some changes to Sidekiq. Previously GitLab used a limited amount of queues that were hardcoded in `bin/background_jobs` and in Omnibus GitLab. Starting with 8.13 all queue names that are used can be found in `config/sidekiq_queues.yml`. Users using either `bin/background_jobs` to start Sidekiq or Omnibus GitLab don't need to make any manual changes. Users building from source may have to make changes to their setup to ensure Sidekiq uses this configuration file. To do so, make sure that Sidekiq is started as follows:

```bash
sidekiq -C path/to/gitlab/config/sidekiq_queues.yml
```

If you are using a custom Sidekiq configuration file you either have to merge the contents of `sidekiq_queues.yml` into this file (and keep it up to date), or use `sidekiq_queues.yml` and specify your custom options using the `sidekiq` CLI.

This configuration file also specifies a weight for every queue. This means a slight increase in Redis load but allows Sidekiq to more fairly distribute work, instead of processing queues in order. Queue names and priorities can not be customized by the user.

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
