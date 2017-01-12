---
title: "GitLab 8.7 released with Due Date for Issues and Remote Mirrors"
date: 2016-04-22
categories: release
author: Job van der Voort
author_twitter: Jobvo
image_title: /images/8_7/ny.jpg
---

We want GitLab to be the place where your projects go from idea all the way to
production. You shouldn't have to rely on other tools to build something
great together.
We believe GitLab is able to power any step in this process and with
GitLab 8.7, we've made every step better.

GitLab 8.7 improves Issues, makes diffs better to work with, brings better
commenting, has 100% more cherries and can now even push to remote repositories
by its own volition[^1].

This month's [MVP] is [Connor Shea][connor]. Connor has been an incredibly
responsive and productive member of the community, working on anything from new
features to performance issues up to this very release post.

We also want to thank [Ershad Ahmad][ershad] for his enthusiastic support in the
community, both in the forums and on Twitter. Thanks Ershad and Connor!

[^1]: _GitLab 8.7 doesn't actually have a mind of its own._

<!--more-->

[mvp]: /mvp "GitLab Hall of Fame"
[connor]: https://gitlab.com/u/connorshea
[ershad]: https://gitlab.com/u/ershad

## Remote Mirrors (EE only)

You could already automatically mirror an external repository to your GitLab
instance. With GitLab 8.7 you can now do the inverse and have GitLab push
updates to a remote repository: a mirror on a remote repository ([!249]). It's
like you can have your cake and eat it too.

This means you can use GitLab to build your projects, while still maintaining
an active mirror in another place. You could even run a GitLab instance locally
and mirror it to GitLab.com or any other git hosting service.

To start mirroring to a remote repository, find the Mirror Repository settings
in your project and fill out the required URL and GitLab with automatically sync
the remote every hour.

![Remote Mirror in GitLab 8.7](/images/8_7/remote_mirror.png)

[!249]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/249

## Multiple Label Filter

You might already be labelling your issues and merge requests. You might even
[be subscribed] to a label. If that's the case, you were probably sad to
discover GitLab couldn't filter by multiple labels at once. Well, now you can!

Select any number of labels to filter only for issues or merge requests that
contain all selected labels. Meaning, if I search for `feature proposal` and
`customer`, I'm now able to find only feature proposals by customers ([!3438]).

![Multiple label filter in GitLab 8.7](/images/8_7/label.png)

[be subscribed]: /2016/04/13/feature-highlight-subscribe-to-label
[!3438]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3438

## LICENSE templates

If you have an open source project, you should have a license in place for it.
Typically, projects include a text file named `LICENSE` in the root of their
repository. GitLab now provides license templates, so you can quickly move on
with building the rest of the project ([!3660]).

To add a license, add a new file named `LICENSE` to an existing project. GitLab
will show a dropdown with licenses to choose from. With certain licenses, your
name will even be pre-filled.

![LICENSE templates](/images/8_7/license.png)

Open source licenses benefit everyone. For authors, they specify any conditions
of reuse or modification of their code. For people who use the code, they
clarify what people can and cannot do with it. It may sound restrictive but
there are several variations of licenses, so it really depends on the author's
preference. That's why we provide several of the most popular licenses. We
welcome merge requests for additional templates. These licenses allow the open
source community to carry on with the free use and sharing of software.

[!3660]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3660

## Due Date for Issues

It's easy for things to get lost in the shuffle of multiple priorities and
several stakeholders. This challenge compounds in collaborative projects since
people often depend on each other.  To help keep things on track, we've added
the ability to set a due date for individual issues ([!3614]).

![Due date for issues in GitLab 8.7](/images/8_7/due_date.png)

With the addition of due dates for issues, there are now two ways to keep your
projects on track. However, due dates and milestones have a couple important
distinctions. Due dates are only for individual issues. They are most useful
when you want to drive your team to a target completion date.

![Due date for issues in GitLab 8.7](/images/8_7/due_date2.png)

Milestones, on the other hand, apply to your entire project. Milestones are
great for organizing issues and merge requests into a cohesive group and to
track progress on a collection of issues, using the [milestone view].

[milestone view]: https://gitlab.com/gitlab-org/gitlab-ce/milestones/23
[!3614]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3614

## Cherry Pick

You can now cherry-pick any commit into any branch, right within GitLab.
Cherry picking allows you to take a single commit and bring it to any other
branch. It's especially useful if you work with multiple, concurrent branches,
like the release branches of GitLab (`8-6-stable`, `8-7-stable`) and you want
to bring a certain change set over from one to the other.

To cherry pick a commit, simply click on the `Cherry Pick` button, whenever
it presents itself. You can find it in Merge Requests and Commits:

![Cherry-pick any commit into any branch in GitLab 8.7](/images/8_7/cherry_pick_button.png)

Choose a branch to pick the commit into and optionally create a merge request
for it.

![Cherry-pick any commit into any branch in GitLab 8.7 and create a merge request straight away](/images/8_7/cherry_pick_modal.png)

Cherry Pick was contributed by [P.S.V.R](https://gitlab.com/u/pmq20). Thanks!

> [Documentation link](http://doc.gitlab.com/ce/workflow/cherry_pick_changes.html)

## Better Diffs

Diffs never looked better than in GitLab 8.7 and now are much more
copy friendly, no longer copying line numbers or the `+` and `-` symbols!

![Better diffs in GitLab 8.7](/images/8_7/diffs.png)

## Tooltip in your timezone

Although some of you may correctly be using the one true timezone (UTC), it was
confusing to many others that times in GitLab were reported in a different
timezone than their own.

That's a thing of the past! All times are now reported in your own timezone.

![GitLab 8.7 uses your local timezone](/images/8_7/timezone.png)

## Improved GitHub Importer

The GitHub importer now also imports milestones and labels, and preserves
references to pull requests and issues!

> [Documentation link](http://doc.gitlab.com/ce/workflow/importing/import_projects_from_github.html)

## Other changes

### Location-aware Search

Search is getting better and better with GitLab. With GitLab 8.7 we've added
location-aware search. Meaning you can either search within the project:

![Location Aware Search in GitLab 8.7](/images/8_7/search1.png)

Or remove the scope of the project and quickly search through the server:

![Location Aware Search in GitLab 8.7](/images/8_7/search2.png)

In either case you always have the quick navigation options available when
searching:

![Location Aware Search in GitLab 8.7](/images/8_7/search3.png)

### Smarter, Better Commenting

We've revised the input for comments! It doesn't just look much better,
it's also smarter. If you start to mention someone, autocomplete
will prioritize names based on the context of the issue, diff or merge request
(several other dropdown boxes have that same ability now).

### Shortcuts!

Press `e` to edit the issue or merge request you're viewing, and press the up
arrow key to quickly edit your last comment. In any case, make sure you're not
focusing in the comments area when pressing those keys.

### More Default Dashboards

Did you know you can change the page you see when you sign in to GitLab?
We've now made it possible to also make that page Groups or even Todos ([!3379]),
thanks to the contribution of [Elias W.][elias]! That means you can set the
Dashboard to be:

- Projects (default)
- Starred Projects
- Activity of Projects
- Activity of Starred Projects
- Groups (new)
- Todos (new)

[elias]: https://gitlab.com/u/eliasw
[!3379]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3379

### Build status notifications

You'll now get browser notifications from running builds in the current project.
No more staring at the builds view!

### Raw build trace output

You can now get the raw build trace of your builds.

### CI: job-level environment variables

You can now define environment variables on a job level in `.gitlab-ci.yml`.

Job-level variables take precedence over global YAML variables, so it is now
possible to override global YAML variables in the definition of a CI job.

> [Documentation link](http://doc.gitlab.com/ce/ci/yaml/README.html#job-variables)

### Improvements to logging when behind a reverse proxy

- You can now add your proxy server to the list of trusted servers, so its IP is
  not logged as the client IP. The default trusted servers were also updated so
  that IPs on the private network are not trusted by default. [!3524](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3524)
- The NGINX included in the Omnibus package is now compiled with the `real_ip`
  module, and can be configured to use a  list of  trusted proxies for
  determining client IP in its logs. [!709](https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/709)

### Authentication-related changes

- SAML can identify external groups based on configuration and set members of
  these groups as external users. [!3530](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3530)
- Omniauth providers can be marked as external, allowing all users of these
  providers, even existing ones, to be marked as external users.
  [!3657](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3657)

## Performance-related changes

* Timestamps for metrics have been made more accurate to prevent InfluxDB from
  overwriting points. Depending on the amount of traffic this may lead to
  significantly more data being stored.
* Extra instrumentation was added for various bits of code.
* Rails cache timings are now tracked.
* Markdown rendering performance has been improved, leading to a 3x performance
  boost in the most ideal cases, though this highly depends on the type of data
  being rendered.
* Emoji autocomplete performance has been improved.
* The referenced merge requests and related branches of an issue are now loaded
  asynchronously. This reduces the loading time of issue pages.
* Re-enable GZIP compression of assets in production.
* Load the emoji spritesheet only when necessary.

## GitLab Mattermost 2.2

[Mattermost 2.2](http://www.mattermost.org/mattermost-2-2-threaded-messages-and-more/)
ships in GitLab 8.7 with threaded messages, French translation, new themes, new
Trello and IRC support, plus many more new benefits.

This version also includes a [security update] and [upgrade from earlier versions] is recommended.

[security update]: http://docs.mattermost.com/administration/changelog.html#security-update
[upgrade from earlier versions]: http://doc.gitlab.com/omnibus/gitlab-mattermost

## Other changes

This release has more improvements, including [security fixes from previous
patches](/2016/04/20/gitlab-8-6-7-released/). Please check out [the
changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG.md) to see
all the named changes.

## Upgrade barometer

This release requires up to 30 minutes downtime.

A migration affecting projects with import data requires downtime as it
manipulates and encrypts user data stored for projects that were previously
imported from other Git repositories. Unless you have a large number of
imported projects, this migration should last only a few seconds.

This release contains other migrations that might make the total upgrade time
longer. For GitLab.com (>800k projects) the complete upgrade was completed within
30 minutes.

***Note:*** This assumes you are upgrading from the latest version. If not,
please also consult the upgrade barometers of any intermediate versions you are
skipping. If you are upgrading from a GitLab version prior to 8.0 *and* you have
CI enabled, you have to [upgrade to GitLab 8.0 first](/2015/09/22/gitlab-8-0-released/).

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations` file](http://doc.gitlab.com/omnibus/update/README.html).

- - -

## Installation

If you are setting up a new GitLab installation please see the
[download GitLab page](/installation/).

## Updating

Check out our [update page](/update/).

## Enterprise Edition

The mentioned EE only features and things like LDAP group support can be found in GitLab Enterprise Edition.
For a complete overview please have a look at the [feature list of GitLab EE](/features/#enterprise).

Access to GitLab Enterprise Edition is included with a
[subscription](/pricing/).
No time to upgrade GitLab yourself?
A subscription also entitles you to our upgrade and installation services.

- - -
