---
title: "GitLab 8.15 Released with Auto Deploy and Web Terminal"
categories: release
author: Job van der Voort
author_twitter: Jobvo
image_title: /images/8_15/pic.jpg
---

With this last release of the year, we're not only completing our [Master Plan](https://about.gitlab.com/2016/09/14/gitlab-live-event-recap/), but we
want to show you something cool we've been working on:

<figure class="video_container">
  <iframe src="https://www.youtube.com/embed/m0nYHPue5RU" frameborder="0" allowfullscreen="true"> </iframe>
</figure>

<!--more-->

<br>

With GitLab 8.15, we're introducing Auto Deploy (shown in the video at
[1:42](https://youtu.be/m0nYHPue5RU?t=102)), which automates setting up deploys and review apps. For a
Ruby on Rails project, this brings setup time to under a minute.

Plus, to make accessing your environments easier and faster, you can now
access them directly through a terminal in GitLab (shown in the video at [5:18](https://youtu.be/m0nYHPue5RU?t=318)).

We want to give the power of containers, continuous integration and deployment,
review apps and container schedulers to everyone. With GitLab 8.15, we
take away all the hard work without hiding anything. In the demonstration we
setup and deploy a Ruby application with review apps, multiple environments,
chatops to a Kubernetes cluster in about 12 minutes. This typically takes days,
if not weeks to setup and use without GitLab.

For many people, December is a month of celebration and gift giving.
This month, GitLab was again so lucky to receive many great contributions.

The MVP of this month is [Michael Munch](https://gitlab.com/Munken) for bringing beautifully-typeset math
(LaTeX) to GitLab. Michael worked over a period of 6 months in merge requests
with in total more than three hundred comments to bring this to GitLab.

We'd also like to thank [Warren Postma](https://gitlab.com/warren.postma) for his contributions on the issue trackers, and the [community forum](https://forum.gitlab.com/users/warren.postma/activity) and [generally being a great advocate of the product and the company](https://gitlab.com/warren.postma/gitlab-ce/wikis/home).
And lastly, we want to thank [Elan Ruusamäe](https://gitlab.com/glensc) and [Dirk Hörner](https://gitlab.com/dirker) for their
contributions in technical design and implementation that have given super
powers to Git Hooks.

Thanks Warren, Michael, Elan, and Dirk!

## Auto Deploy

We want everyone to quickly get a fully functioning CI/CD pipeline that deploys
to a container scheduler. It shouldn't require any effort to get started,
but should also be scalable and not hide any of the magic.

Auto Deploy does this. Auto Deploy adds a single button to your project,
that when clicked, will create a merge request with a template that will
automatically deploy your application using Docker to your container scheduler.
The cool thing about this is that this immediately leverages Review Apps,
meaning you can see it working before even merging the merge request!

![Auto deploy in GitLab 8.15](/images/8_15/auto_deploy.png)

This is as close as you can get to one-click deploys, while exposing what
is happening and having all this version-controlled, ready
to collaborate and iterate on.

See [1:42](https://youtu.be/m0nYHPue5RU?t=102) in the video for a quick demo of
Auto Deploy, as it is available in GitLab 8.15.

For this first iteration, we ship Auto Deploy with a template for deploying to an external OpenShift cluster. We use [Herokuish](https://github.com/gliderlabs/herokuish) and Heroku Buildpacks to
package your application into a Docker Image that then is deployed to
Kubernetes on Openshift. We want to add support for more container
schedulers and cloud platforms later (vanilla Kubernetes cluster, Mesos, Docker
Swarm). Contributions are very welcome in [our template repository](https://gitlab.com/gitlab-org/gitlab-ci-yml).

> See [the Autodeploy documentation](https://docs.gitlab.com/ce/ci/autodeploy/index.html) for more information.

## Web Terminal

Working together with your container scheduler, GitLab happily spins up several
(dynamic) environments on request for your projects. Be that for review apps
or a staging or production environment.
Traditionally, getting direct access to these environments has been a little
painful. And that's a shame: it's very useful to quickly try something in a
live environment to debug a problem, or just to experiment.

With the web terminal, this has become extremely easy. Just visit the
environments page in your project and click on the terminal button.
GitLab will SSH into the instance for you and allow you to do anything
you would be able to do from your local instance.

![Web Terminal in GitLab 8.15](/images/8_15/terminal_gif.gif){: .shadow}

In the demonstration at [5:18](https://youtu.be/m0nYHPue5RU?t=318) we show you
give you a quick peek at the web terminal. We can't wait to see how you'll
use it to speed up your workflow.

> See the [administrator](https://docs.gitlab.com/ce/administration/integration/terminal.html) and [environments](https://docs.gitlab.com/ce/ci/environments.html#terminal-support) documentation on the web terminal

## Improved Bitbucket Importer

Importing from Bitbucket has become even more powerful. With GitLab 8.15 we'll
also import all pull requests as individual merge requests plus pull
request comments, milestones and the wiki from Bitbucket.
That makes the things we import from any Bitbucket project:

- Repository description
- Git repository
- Issues and their comments
- Pull Requests and their comments
- Milestones
- Wiki

When importing a project all references to pull requests and issues are
preserved and so is the access level (public/private).

[Read the docs on the Bitbucket importer](https://docs.gitlab.com/ce/workflow/importing/import_projects_from_bitbucket.html)

## Global Git Hooks

If you want to enforce rules and triggers based on Git pushes and their
contents, you have been able to use custom Git hooks in GitLab. But if you
want to standardize on these rules, you'd have to copy and paste them
to every new project.

With Global Git Hooks you can now create Git hooks that will be run
for each project on the GitLab instance. This should make it much easier
to set up rules that you want all incoming code to comply with.

Create the hooks in `hooks/<hook_name>.d/` directory or tell GitLab Shell where the directories are.

[See the documentation on Custom Hooks](https://docs.gitlab.com/ce/administration/custom_hooks.html)

## Chained Custom Git Hooks

If you have set up custom Git hooks, the order might matter: when an initial
hook fails, there is no point in moving forward. With Chained Custom Hooks
hooks will execute in lexical order, failing on the first failing script.

This means you can create hooks `1-hook.sh` and `2-hook.sh` and you'll know that
`1` will execute before `2`.

This gives a lot of power to your hooks and allows endless customization of
what happens when a commit is about to land in your GitLab project.

For more information, see the [custom git hooks documentation](https://docs.gitlab.com/ce/administration/custom_hooks.html#chained-hooks-support).

Thanks to both Elan Ruusamäe and Dirk Hörner for both helping to define Global Git Hooks and this feature, and providing the implementation!

## LDAP Group membership overrides (EE)

In GitLab EE, you can sync any LDAP group with any GitLab group and give
everyone automatically a certain permission. For instance, you
can give everyone in the LDAP group `developers` the `Developer`
permission level. New developers just have to be added to the LDAP
group and GitLab will take care of giving them access automatically.

With GitLab 8.15, this has become even more powerful. In addition to the
automatically synced permissions, you can now override this permission
per user. This should make it easier to manage complex permissions across
groups and projects.

![Override LDAP permissions in GitLab 8.15 EE](/images/8_15/ldap_overrides.gif){: .shadow}

## Slack Chatops

After bringing Chatops to GitLab with [our Mattermost integration](https://about.gitlab.com/2016/11/22/gitlab-8-14-released/#chat-commands-experimental),
we're now doing the same for everyone using Slack! This
means you can create, show and search for issues straight from Slack. Super
convenient to bridge that gap from a casual conversation to an actual issue.

In addition, you can actually deploy from and to any environment.
For instance, you can do

```
/awesome-website deploy from staging to production
```

And GitLab will deploy the latest commit from staging onto master.

![Slack Chatops in GitLab 8.15](/images/8_15/slack.png)

Configure Chatops for Slack in your project services. As always,
we're looking forward to see contributions to help expand the power of
chat integration with GitLab!

## One-click Mattermost configuration

Setting up the [awesome Mattermost integration](https://about.gitlab.com/2016/11/22/gitlab-8-14-released/#chat-commands-experimental) with GitLab has been made
much easier. It's a matter of a single click now, as you can see [in the video at 3:16](https://youtu.be/m0nYHPue5RU?t=196).

![Super easy Mattermost configuration in GitLab 8.15](/images/8_15/mattermost.png)

The Mattermost and Slack integrations allow you to do the same things:
create, show and search for issues and deploy to any environment.

> [Read the docs on the Mattermost Chatops integration](https://gitlab.com/help/project_services/mattermost_slash_commands.md)

## Diff in Notification Emails

When you get a notification email from a comment on a diff, GitLab will now
send along a bit of the diff, so you have the correct context immediately
available.

![Diffs in Notification emails in GitLab 8.15](/images/8_15/diff_emails.png)

## Interface improvements

Our amazing usability team has been working hard on making GitLab easier to use,
enhancing GitLab's personality and improving readability. This release contains
various changes that will make using GitLab more enjoyable!

### Fresh typefaces!

To improve readability and cross-OS/browser support in GitLab, we have
changed to using system fonts. These fonts are optimized for your platform
and should therefore provide a better experience, independent of where you're
viewing GitLab from.

If you want to get a feel of GitLab across platforms, [check out the original merge request](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7545).

### Slimmed down widths

We've reduced the max-width for issues and merge requests container in order to
provide a more readable line length. This is the first step for us to correct
the huge line lengths you see throughout GitLab.
Follow our [meta issue](https://gitlab.com/gitlab-org/gitlab-ce/issues/13680)
as we continue to improve GitLab's line length.

### Unique Labels

We've given labels a unique look in order to differentiate them from buttons.
We are continuing work on this to make our
[labels](https://gitlab.com/gitlab-org/gitlab-ce/issues/25518) and
[status badges](https://gitlab.com/gitlab-org/gitlab-ce/issues/25564)
even more consistent in further iterations.

![Unique Labels in GitLab 8.15](/images/8_15/labels.png)

### Improved Build Scrolling and Loading

Build scrolling and loading works and looks quite a bit better now:

![Improved Build Scrolling and Loading in GitLab 8.15](/images/8_15/build_scroll.gif)

### Smaller page size

Between system fonts and improvements to autocomplete, we've reduced the
average page size of any page in GitLab significantly. A given merge request
in the GitLab CE project went from 1800kb to now 718kb!

### Improved empty states

In order to improve our experience for users who are just getting started with
GitLab, we've added informative and fun empty states to many of our pages
across the application!
View our [meta issue](https://gitlab.com/gitlab-org/gitlab-ce/issues/15632) to
see where we've placed new empty states and feel free to suggest new ones!

![Even empty is beautiful in GitLab 8.15](/images/8_15/empty.png){: .shadow}

### Other changes and tweaks

- Improved accessibility by adding a focus state to dropdown options
- Added hover states to our primary navigation and tabs throughout the site.
- Improved hover, focus, and active states for buttons [!7797](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7797)
- Added hover states to collapsed items with the issues/mr's sidebar [!7777](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7777)

## Mathematics support for Markdown and AsciiDoc, using KaTeX

Comments and repository files can now contain beautifully-typeset mathematics, using the [KaTeX](https://khan.github.io/KaTeX/) library from Khan Academy.

To render inline mathematics, use dollar signs around inline code: ```$`a^2+b^2=c^2`$```

To render multiline mathematics, use the `math` language for the code block:

    ```math
    a^2+b^2=c^2
    ```

In addition to working for Markdown, this is also available for AsciiDoc documents. [Read the documentation on mathematics support.](https://docs.gitlab.com/ce/user/markdown.html#math)

![Beautifully rendered math in GitLab 8.15](/images/8_15/math.png)

Thanks to Michael Munch for this feature!

## Cleaner merge commit messages

Previously, merge commit messages included the title and description of the
merge request, and a reference to the merge request. This didn't read well when
using `git log` and similar tools, because merge request descriptions often
contain requests for review, screenshots, and other details incidental to the
code change.

Now, the default merge commit message is in the following format:

    Merge branch '$SOURCE_BRANCH' into '$TARGET_BRANCH'

    $TITLE

    Closes $CLOSING_ISSUE_REFERENCES # only present if the MR closes issues

    See merge request $MERGE_REQUEST_REFERENCE

The previous default message is available as an option when customizing the
merge commit message.

Thanks to Gabriel Gizotti!

## Shorthand cross-project references in GitLab Flavored Markdown

Previously, a reference to something in another project always included the
namespace, even if the project was in the same namespace.

Now, shorthand references are available. So from within the
`gitlab-org/gitlab-ce` project, you can refer to issue #1 in GitLab Workhorse
by writing `gitlab-workhorse#1` instead of `gitlab-org/gitlab-workhorse#1`,
saving precious keystrokes!

For more information, see the [special GitLab references](https://docs.gitlab.com/ce/user/markdown.html#special-gitlab-references) section of our Markdown documentation.

Thanks to Oswaldo Ferreira!

## Create an issue with unresolved discussion from a merge request

In 8.14, we [added the ability to block a merge when there are unresolved discussions](https://about.gitlab.com/2016/11/22/gitlab-8-14-released/#prevent-merge-until-review-is-done).

Now, we have added an option to [create a new issue from the unresolved discussions in a merge request](https://docs.gitlab.com/ce/user/project/merge_requests/merge_request_discussion_resolution.html#move-all-unresolved-discussions-in-a-merge-request-to-an-issue), and resolve those discussions at the same time! This is perfect for those cases where you need to merge something now, but don't want to forget about the code review comments.

Thanks to Bob van Landuyt!

## Manual Actions from the Pipeline Graph

Manual actions allow you to require manual interaction before moving
forward with a particular job in CI. Your entire pipeline can run
automatically, but the actual deploy to production will require a click.

You can do this straight from the pipeline graph. Just click on the play
button to execute that particular job.

![Manual actions on the pipeline graph](/images/8_15/manual_actions_graph.png)

## User Activities API

To quickly get an idea of when a user last interacted with GitLab,
we've added a special admin-only API to GitLab that allows you to get
the last activity timestamp of every user on the instance.

[Find the details in the docs](https://docs.gitlab.com/ee/api/users.html#get-user-activities-admin-only)

## Sort Project and Group members

You can now find people in projects and groups more easily by sorting them
by name, access level and date of joining.

![Easily find people in projects and groups in GitLab 8.15](/images/8_15/sort_members.png)

## API Changes

Every month we make many additions to our API. Here are the highlights
for GitLab 8.15:

- Allow some Project API GET endpoints to be requested anonymously
- Allow Repositories & Files API GET endpoints to be requested anonymously
- Allow some Tag API GET endpoints to be requested anonymously
- Add scopes for personal access tokens and OAuth tokens
- Add ability to cherry pick a commit (community contribution)
- Add ability to unshare a project from a group (community contribution)
- Add ability to set `should_remove_source_branch` on merge requests (community contribution)
- Add simple representation of group's projects (community contribution)
- Expose committer details for commits (community contribution)
- Expose merge status for branch API (community contribution)
- Expose personal snippets as /snippets (community contribution)
- Expose pipeline coverage

## Omnibus GitLab package changes

### PostgreSQL version upgrade

Starting last month with GitLab 8.14 omnibus-gitlab package, we are providing a
way to upgrade the PostgreSQL database version.

The current version of PostgreSQL we are packaging (9.2.18) is slowly
approaching its EOL. Due to the [PostgreSQL versioning policy](https://www.postgresql.org/support/versioning/),
upgrades between major releases require downtime and the use of the `pg_upgrade` tool.

For this purpose, we are packaging the newest available PostgreSQL version (9.6.1).
We are also introducing `gitlab-ctl pg-upgrade` tool which should make this
transition as painless as possible.
When upgrading to GitLab 8.15, this *action will not be run automatically*.
This will allow you to plan the database upgrade downtime.

After version 9.0 is released, we plan on setting the PostgreSQL version 9.6 as
default so please make sure that you plan your upgrade before that release.
We're expecting to ship GitLab 9.0 on or after February 22nd.

> [Read more about database upgrade in our docs](https://docs.gitlab.com/omnibus/settings/database.html#upgrade-packaged-postgresql-server)


> Ran into issues? Create an issue at the [omnibus-gitlab issue tracker](https://gitlab.com/gitlab-org/omnibus-gitlab/issues),
and reference it in the [upgrade problems meta issue.](https://gitlab.com/gitlab-org/omnibus-gitlab/issues/1783)

## Performance Improvements

GitLab CE:

* Retrieving commit counts has been improved for certain cases: [!7668](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7668)
* Polling intervals have been adjusted to reduce system load: [!7762](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7762)
* Refreshing authorized projects is done in a smarter way to reduce database load: [!7956](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7956)
* The most recent commit ID for a path is now cached: [!8098](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8098)

GitLab EE:

GitLab EE now ships with a command called `sidekiq-cluster`. This command can be used to start extra Sidekiq workers that process only a limited number of queues. This feature can be used to process queues that receive a lot of jobs, without it affecting other parts of Sidekiq. This was added in [922](https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/922).

This command is not yet used by Omnibus, our goal is to add this in 8.16.

## GitLab Runner 1.9

We are also releasing GitLab Runner 1.9 today. Some highlights:

- Add a retry mechanism to prevent failed clones in builds [!399](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/399)
- Add Kubernete Node Selector [!328](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/328)
- Push prebuilt images to dockerhub [!420](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/420)
- Use prebuilt containers with Kubernetes executor [!425](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/425)
- Add path and share cache settings for S3 cache [!423](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/423)
- Split prepare stage to be: prepare, git_clone, restore_cache, download_artifacts [!406](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/406)
- Introduce docker.Client timeouts [!411](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/411)
- Allow network-sourced variables to specify that they should be files [!413](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/413)
- Fix docker hanging for docker-engine 1.12.4 [!415](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/415)
- Add pprof HTTP endpoints to metrics server [!398](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/398)
- Add a multiple prometheus metrics: [!401](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/401)

To see the full list of all changes please read [the Runner's CHANGELOG file](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/v1.9.0/CHANGELOG.md).

## GitLab Mattermost 3.5.1

GitLab 8.15 includes [Mattermost 3.5.1](https://about.mattermost.com/), an open
source Slack-alternative providing workplace messaging for web, PC and phone
with archiving and search. Improvements this month include new [Xen Orchestra and Homebrew integrations, plus upgraded Desktop Apps for Windows, Mac and Linux](https://about.mattermost.com/mattermost-december-2016-update/).

This version includes [security updates](http://about.mattermost.com/security-updates/) and upgrade from earlier versions is recommended.

Mattermost 3.5.1 was included in GitLab 8.14.1, so anyone on GitLab 8.14.1 or
later should have the patch already.

## Other changes

This release has more improvements. Please check out
[the changelog] to see all the named changes.

[the changelog]: https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG.md

## Upgrade barometer

To upgrade to GitLab 8.15, downtime is required. Larger instances (>1000 users)
should expect about 15 minutes of downtime.

The specific migrations requiring downtime are described below.

- Columns with default values are added, this process may take some time depending on the number of rows in these tables
- Some indexes are added concurrently, which does not require downtime but may take some time to complete
- The environments table is cleaned up, and a new column is added with a generated default value (this could take some time depending on the number of environments)

### Note

We assume you are upgrading from the latest version. If not, then also consult the upgrade barometers of any intermediate versions you are skipping.
If you are upgrading from a GitLab version prior to 8.0 *and* you have CI enabled, you have to upgrade to GitLab 8.0 [first](https://about.gitlab.com/2015/09/22/gitlab-8-0-released/).

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](https://docs.gitlab.com/omnibus/update/README.html).

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
