---
layout: post
title: "GitLab 8.9 released with File Locking, Environments, Priority Labels and more!"
categories: release
author: Job van der Voort
author_twitter: Jobvo
image_title: /images/8_9/windmills.jpg
---

Whether you work on code or media,
work thousands of miles away from your organization's HQ,
or work on a project with ten thousand issues,
GitLab 8.9 will help you get stuff done faster.

With GitLab 8.9 you will be able to work better on complex projects together
with file locking, priority labels and new workflow tools, like
a custom notification level and the ability to
restrict merging until the build passes.
We're also continuing to improve GitLab's built-in continuous integration.
You can now specify environments, have artifacts expire and quickly get started
with templates.

This month's Most Valuable Person ([MVP](https://about.gitlab.com/mvp/)) is
Rui Santos, for building the new feature that restricts merging until your build
passes. It's a great feature that we're sure many people are going to use.
Thanks Rui!

Since GitLab 8.8.0 we've had 1761 commits with 1947 files changed,
see what has changed exactly, below.

<!--more-->

## File Locking (new Product)

When you're working on files that Git can't merge for you,
working with multiple people on the same file can be a risk.
Conflicts when merging the non-text file
(which inevitably happens when two people work on the same file at the same
time), are hard to overcome and will require a lot of manual work to resolve.

To work around this, we've added the ability to lock files in GitLab.
File Locking prevents everyone, except you, from modifying a specific file or
entire directory.
It's also a good way of communicating to your collaborators that you
are working on this file.

### Example: Game assets

For example, you're working on a game. Many people are involved with building
the complex levels. With file locking, you can lock the level you want to work
on by clicking lock in the interface:

![Lock a file in GitLab 8.9](/images/8_9/lock_file.png)

Your colleagues will see that you are working on this file.
Except for you, no one else is able to push changes that modify this file.

![A locked file in GitLab 8.9](/images/8_9/locked_file.png)

Once you're done making changes and you've merged them, you can remove your lock
in the same way as you've placed it.

Find a list of all locked files under repository:

![Locked files in GitLab 8.9](/images/8_9/locked_files.png)

### Availability

File locking is available as a [paid option](/pricing) for Enterprise Edition
and for free on GitLab.com.
We welcome further suggestions to expanding this feature.

> Read more in the [File lock documentation][lock-doc].

[lock-doc]: http://docs.gitlab.com/ee/user/project/file_lock.html

## Environments and Deployments in CI

You can already deploy from GitLab to your various environments,
whether it is test, staging or production.
With GitLab CI you can set up pipelines with one or more jobs that
deploy for you.

With GitLab 8.9 you can now define environments in your project's
CI configuration file (`.gitlab-ci.yml`).
This allows you to track deployments to these environments and quickly
understand things like "what's running in staging?"

Defining an environment is as simple as adding the `environment` variable
to your `.gitlab-ci.yml`:

```
deploy to production:
  stage: deploy
  script: git push production HEAD:master
  environment: production
```

You can then see exactly what is live on which environment:

![Environments in GitLab 8.9](/images/8_9/environments.png)

> Read more in the documentation on [environments in GitLab CI][cienv].

[cienv]: http://docs.gitlab.com/ce/ci/yaml/README.html#sts=environment

## Priority Labels

It can be hard to prioritize issues and merge requests, especially larger
projects can have a hard time sorting through hundreds, thousands of issues.

Adding priorities to issues could help with that, but we felt that there had
to be a better way that involved less manual work. Our solution is prioritized
labels.

Prioritized labels are like any other label, but sorted by priority.
This allows you to sort issues and merge requests by priority. Those with
the highest priority label, will appear on top.

![Priority Labels in GitLab 8.9](/images/8_9/plabels2.png)

For instance, the highest priority label for GitLab is `P1`. If I sort by
priority, I will see that issues with `P1` appear on top, followed by `P2`, etc.
In most cases, `security` issues are very important. By making the `security`
label highly prioritized, I can rest assure that my colleagues will start
working on those issues before any other issue in this milestone.

![Priority Labels in GitLab 8.9](/images/8_9/plabels3.png)

If you prefer a more traditional priority system, you're free to add labels
such as `priority: 1`, `priority: 2`.

Right now, priority sorting is based the highest priority label only.

> Read more in the documentation about [Labels].

[labels]: http://docs.gitlab.com/ce/user/project/labels.html

## Custom Notification Level

It's amazing to see how people use GitLab. Some people only review code,
others closely monitor everything that happens on the issue tracker,
yet other people only want to see what's new.

To make it easier to only get notified on what's important to you,
we've added a new notification level: custom.

<img src="/images/8_9/custom_not_1.png" alt="Custom notification level in GitLab 8.9" style="max-height: 350px;" />

The custom notification level works just like a participating level.
This means anywhere you participate or get mentioned, you receive a
notification. On top of that, you now have the ability to also receive
select notifications for things that are important to you.

<img src="/images/8_9/custom_not2.png" alt="Custom notification level in GitLab 8.9" style="max-height: 350px;" />

So if you just want notifications for new merge requests, you can now easily
set that up.

> Read more in the documentation about [Notifications].

[notifications]: http://docs.gitlab.com/ce/workflow/notifications.html

## Request Access to a Project

Rather than having to contact the owners through some other means,
you can now request access to a project straight from GitLab.
Find the button on the project home page:

![Request access to a project in GitLab 8.9](/images/8_9/req_access.png)

You'll get a notification when someone requests access and see the request
appear in the members sections of your project.

![Request access to a project in GitLab 8.9](/images/8_9/access_request.png)

> Read more in the documentation on [requesting access to a project][project] or
a [group].

[project]: http://docs.gitlab.com/ce/workflow/add-user/add-user.html#request-access-to-a-project
[group]: http://docs.gitlab.com/ce/workflow/groups.html#request-access-to-a-group

## .gitlab-ci.yml Templates

Continuous integration, built into GitLab, works by a `.gitlab-ci.yml` file,
where you define your tests, builds and deployments. Getting started with
creating this file can be hard, so we've created several templates to make
this easier.

To start with a template `.gitlab-ci.yml`, simply create a new file and
call it `.gitlab-ci.yml`. You'll see a dropdown appear where you can choose
from several templates.

![.gitlab-ci.yml templates in GitLab 8.9](/images/8_9/ci_template.png)

If you want to contribute your own templates, you can do so in the [`.gitlab-ci.yml` repository][yml-repo].

Want to give GitLab CI a roll? You can use it completely for free on GitLab.com
or on your own server.

[yml-repo]: https://gitlab.com/gitlab-org/gitlab-ci-yml

## New Navigation

We've revamped the navigation of GitLab. [We wrote before about this][nav-blog],
but have made further changes.

![Updated navigation in GitLab 8.9](/images/8_9/look3.png)

The main navigation within projects is now on the top bar. Global navigation,
to pages specific to you, such as your issues and groups is in the new sidebar,
hiding automatically.

![Updated navigation in GitLab 8.9](/images/8_9/look4.gif)

[nav-blog]: https://about.gitlab.com/2016/06/06/navigation-redesign/

## Universal 2nd Factor Support

GitLab now fully supports the Universal 2nd Factor (U2F)
authentication standard. This means you can use a device like the U2F security
keys by Yubico, known as YubiKeys as your 2nd factor when signing into GitLab.

Read more about our support for U2F in our [our blog post about it](https://about.gitlab.com/2016/06/22/gitlab-adds-support-for-u2f)
and the documentation on [Two-factor Authentication][2fa] in GitLab.

[2fa]: http://docs.gitlab.com/ce/profile/two_factor_authentication.html

## Import / Export Projects

If you're moving between GitLab instances or just want a backup of your
most important data, you can now Import and Export entire projects.

![Export entire projects with GitLab 8.9](/images/8_9/export1.png)

Visit the project settings page to export your project. Importing a project
can be done from the new project page.

![Import entire projects with GitLab 8.9](/images/8_9/import.png)

> Read more in the [documentation][import-export].

[import-export]: http://docs.gitlab.com/ce/user/project/settings/import_export.html

## Restrict Merging until Build Passes

You can already merge a merge request automatically after the CI builds have
passed successfully. Thanks to Rui Santos, you can now
even prevent people from merging a merge request unless the build is 'green'.

![Only merge if the build passes in GitLab 8.9](/images/8_9/merge_if_build_passes.png)

This prevents people from circumventing your tests, guards your code from
sloppy contributions and encourages everyone to maintain a solid test suite.

## GitLab Geo (new Product)

GitLab Geo allows you to have one or multiple mirrored instance of GitLab
running in another location. That allows your remote team to have quick
cloning and pulling of repositories, while still having everyone, globally
in sync.

[We released Geo in Alpha][geo-alpha] with GitLab 8.5 and have been
testing it intensely internally and with customers since. One customer
reported that git clone times dropped from 10 minutes to 30 seconds
on average for their teams.

### Availability

GitLab Geo is available for purchase from [our pricing page] or through [our sales team].

### Limitations

GitLab Geo isn't supported for disaster recovery purposes yet.
We've released a guide with manual steps in the unfortunate case that you'd
have to use it for this purpose, but we recommend against using it for that.

GitLab Geo only supports PostgreSQL at the moment. MySQL is not supported.

### Getting Started

To get started with GitLab Geo, [read our documentation on it][geo-docs].

[geo-alpha]: https://about.gitlab.com/2016/02/22/gitlab-8-5-released/
[our pricing page]: https://about.gitlab.com/pricing
[our sales team]: sales@gitlab.com
[geo-docs]: http://docs.gitlab.com/ee/gitlab-geo/README.html#sts=GitLab Geo

## Other changes

This release has more improvements, including security fixes. Please check out
[the Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG.md)
to see all the named changes. See below for some further highlights of changes.

### Better Highlighting

GitLab 8.9 incorporates the first [Rouge](https://github.com/jneen/rouge) release since September (!) with over
20 new languages supported, plus support for newer features of Swift, Ruby,
Python, and C/C++, as well as some critical bug fixes for Apache, JavaScript,
Objective-C, and Groovy.
R and Apache users will also see a marked improvement in lexing quality.
[See the full changelog here](https://github.com/jneen/rouge/blob/master/CHANGELOG.md#version-1110-2016-06-06
clap)

### Award Emoji in Comments

Besides issues and merge requests, you can now also vote on individual comments.
Whether you want to react to someone without distorting the flow of the
conversation or want to conduct a quick poll, you can now do it quickly,
everywhere.

> Read more in the [award emoji documentation][emoji].

[emoji]: http://docs.gitlab.com/ce/workflow/award_emoji.html

### Manually add Todos

Every issue and merge request can now be marked as 'Todo' or 'Done'. This means
you don't have to go back to the lists of Todos to mark one off and can even add
items quickly to your Todos. Super useful!

![Manually add Todos in GitLab 8.9](/images/8_9/add_todo.png)

![Mark as done in GitLab 8.9](/images/8_9/mark_done.png)

> Read more in the [Todos documentation][todos].

[todos]: http://docs.gitlab.com/ce/workflow/todos.html

### Bulk-assign labels

With label priorities and future features (such as [issue boards](https://gitlab.com/gitlab-org/gitlab-ce/issues/2306168)), labels are
becoming more and more important in GitLab.
To make working with issues a bit easier,
we've added the ability to bulk-assign labels.

### Expire Artifacts

If you're using artifacts in GitLab's built-in CI, you might be building up
quite a catalogue of old data. You can now have artifacts expire by adding
a `expire_in` line to your `.gitlab-ci.yml` file. The artifacts will expire
after the duration that you specify.

```
job:
  artifacts:
    expire_in: 1 week
```

You can use natural language to set the expiry time:

- 3 mins 4 sec
- 2 hrs 20 min
- 2h20min
- 6 mos 1 day
- 47 yrs 6 mos and 4d
- 3 weeks and 2 days

_**Note:** this feature requires Runner 1.3, released at the same time as
GitLab 8.9_

> Read more in the [artifacts documentation][artifacts].

[artifacts]: http://docs.gitlab.com/ce/ci/yaml/README.html#artifactsexpire_in

### When keyword for Artifacts

You can now only have artifacts be made available on failure, success or always.

```
job:
  artifacts:
    when: on_failure
```

The default behavior is the same as before, only creating artifacts on success.

_**Note:** this feature requires Runner 1.3, released at the same time as
GitLab 8.9_

> Read more in the [artifacts documentation][artwhen].

[artwhen]: http://docs.gitlab.com/ce/ci/yaml/README.html#artifactswhen

### Support for Docker Registry Manifest V1

GitLab 8.9 adds support for Manifest V1 generated by older versions
of Docker (before 1.10).

### Smarter allocation for Shared Runners

Shared Runners now prioritize projects without any other shared Runners
assigned to them, before allocating more shared Runners to a single demanding
project.

### GitLab Mattermost 3.1

[Mattermost 3.1](http://www.mattermost.org/mattermost-3-1-apple-watch-notification-upgrades-shortcuts-compact-view-openshift-and-more/) ships in GitLab 8.9 with multi-team accounts, Japanese language translation, Apple Watch & upgraded notifications, keyboard shortcuts & channel switcher, new full width and compact view display options, new emoji, plus [security updates](https://about.mattermost.com/security-updates/) and [many more improvements.](http://docs.mattermost.com/administration/changelog.html)

**The upgrade requires manual steps!**
Before upgrading, make sure to read [documentation for upgrades from versions prior to 8.9](http://docs.gitlab.com/omnibus/gitlab-mattermost/#upgrading-gitlab-mattermost-from-versions-prior-to-8.9)

### Managing custom SSL certificates with omnibus-gitlab package

If you run your own CA or you have self-signed certificates, you need to tell omnibus-gitlab explicitly to trust them.
This is required for web-hooks, system-hooks and anything that requires a trusted connection.
Accomplishing this task was possible with older versions of the package, however you had to repeat it at every upgrade.
Now it is possible to add all your custom certificates into a single place and after reconfiguring the package,
GitLab will be able to verify the certificate authenticity.
For more information, see the [custom SSL certificate documentation](http://docs.gitlab.com/omnibus/common_installation_problems/README.html#using-self-signed-certificate-or-custom-certificate-authorities).

## Performance Improvements

Performance is a great priority for us. We're working hard on making sure
GitLab can handle the loads of very large instances (like GitLab.com with hundreds
of thousands of active users) easily.

With GitLab 8.9 we've made many improvements, below are some of the highlights.

### Increased Memory Limits

We increased the default memory limits from 300-350MB to 450-600MB per worker.
Previously, our workers were being killed every 6 seconds. This was increasing
the load of the whole system, as every 6 seconds a new worker was spawned that
had to create new connections to the database and cache the data that is used
often. As a result of this change we saw a drop in HTTP queuing time from ~2
seconds down to ~100ms on average. As a side effect we also noticed that the
system load of our worker and database nodes went down to half. Memory usage on
the workers does not change too much, but worker processes now live for 20
minutes on average.

![Increased memory limits in GitLab 8.9 brought down HTTP queue timings](/images/8_9/http-queue-timings.png)

See how this affected the worker load (for GitLab.com):

![Decreased worker load for GitLab 8.9](/images/8_9/worker-load.png)

### Better Handling of Mirroring

We've changed how we schedule mirroring in Sidekiq.
See the difference in queries being pushed into the database:

![Lower amount of queries](/images/8_9/pg-from-sidekiq.png)

### API Endpoint for Sidekiq Metrics

This API endpoint allows you to retrieve some information about the current state of Sidekiq, its jobs, queues, and processes.

> [Read more in our docs](http://docs.gitlab.com/ce/api/sidekiq_metrics.html)

### Other performance improvements

- Lower PG auto-vacuum/analyze thresholds 10x: On large GitLab servers this should amortize the costs of autovacuuming and auto-analyzing better
- Only use JS libraries where needed
- Upgrade to [jQuery 2](https://blog.jquery.com/2013/04/18/jquery-2-0-released/)
- Large amount of changes to performance monitoring, [see here](https://gitlab.com/gitlab-com/www-gitlab-com/merge_requests/2187#note_12598695)
- The column `users.state` is now indexed
- The number of queries needed to render username references in Markdown has been reduced
- The builds counter for projects is now cached
- The assigned issues and merge requests counters are now cached
- The number of queries needed to render issue references in Markdown has been reduced
- Rendering labels in the issue/merge requests sidebar now only needs 1 query instead of 2
- The number of pending/done TODOs is now cached
- The presence of an external issue tracker is now cached per project, reducing the number of queries needed to figure out if a project uses an external issue tracker
- The number of queries needed by the issues API has been reduced
- The number of queries needed to extract issue references has been reduced
- Rendering external links now uses a more efficient way of querying elements to process
- Project dashboards now use the appropriate methods for getting branch/tag counts, these methods cache their output to reduce load on the Git repository/storage system
- The `keys.fingerprint` column is now indexed and any duplicate keys are removed automatically. This speeds up looking up keys using a fingerprint
- Project dashboards now run fewer Git operations
- The list of issue/merge requests participants is now memoized so repeated calls in the same request don't end up doing the same work over and over
- Rendering relative links has been optimised so it uses fewer (and more efficient) Git operations

## Upgrade barometer

Downtime notice: while technically this release allows one
to upgrade without downtime, one may get errors if new comments or award emoji
are created/assigned during the upgrade.

*__Note__: We assume you are upgrading from the latest version. If not, then also consult the upgrade barometers of any intermediate versions you are skipping.
If you are upgrading from a GitLab version prior to 8.0 and you have CI enabled, you have to upgrade to GitLab 8.0 [first](https://about.gitlab.com/2015/09/22/gitlab-8-0-released/).*

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
For a complete overview please have a look at the [feature list of GitLab EE]( https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a
[subscription]( https://about.gitlab.com/pricing/).
No time to upgrade GitLab yourself?
A subscription also entitles you to our upgrade and installation services.

- - -
