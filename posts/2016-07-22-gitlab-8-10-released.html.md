---
title: "GitLab 8.10 released with Wildcard Branch Protection and Manual Actions for CI"
categories: release
author: Job van der Voort
author_twitter: Jobvo
image_title: /images/8_10/bg.jpg
date: 2016-07-22 17:00
twitter_image: '/images/tweets/gitlab-8-10-released.png'
---

GitLab enables you to go faster from idea to production.
With every GitLab release we want to improve this and with 8.10,
GitLab is _yet again_ faster than ever.


With GitLab 8.10, reviewing code and making sure it gets merged
is easier and snappier than ever with many improvements to diffs and protected
branches. And when it's time to deploy, you can now do a manual check before
deploying with a single click, with manual actions.

This month's Most Valuable Person ([MVP](https://about.gitlab.com/mvp/)) is
Winnie! Winnie has been incredibly helpful [fixing bugs][winnie-wins] in GitLab and even
triaging issues on GitLab.com.
Thanks ***Winnie***!

[winnie-wins]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests?author_id=14714&scope=all&sort=id_desc&state=merged

<!--more-->

## Wildcard Branch Protection

To make sure your branches don't get deleted or accidentally pushed to,
[you can protect them][protected-branches]. This even allows you to prevent
people with lower permission levels to push or merge to these branches,
which is very convenient for production and release branches.

With Gitlab 8.10 you can now protect any branch automatically, based on a
wildcard. This makes it much easier to protect a large amount of branches.

![Wildcard Branch Protection in GitLab 8.10](/images/8_10/wc1.png)

For example, if you protect `release-*`, any branch whose name starts
with `release-` automatically becomes protected. At GitLab we use this feature
to automatically protect all our stable releases by protecting `*-stable`.

![Wildcard Branch Protection in GitLab 8.10](/images/8_10/wc2.png)

[protected-branches]: http://docs.gitlab.com/ce/user/project/protected_branches.html

## Merge into Protected Branches

Using protected branches is a great way to ensure only the right people
can push to important branches. By default, only `Master` permission and higher
is able to push or merge anything into a protected branch.

Previously, we added the ability to allow `Developer` users to also push to
these branches. With GitLab 8.10 you can now disallow pushing, yet explicitly
allow merges by `Developer` users.

![Allow developers to merge to protected branches in GitLab 8.10](/images/8_10/dev_merge.png)

**Concretely this means that `Developer` users can merge a merge request but not
directly push**. So your branches are protected from direct pushes, yet developers
don't need elevated permissions or wait for someone with a higher permission to
press merge (this is only possible to the web interface,
not from the command line).

Combine this feature with approvals (EE only) to enforce code review by multiple
people, while still giving developers the power to merge at their discretion.

> [See our documentation on protected branches](http://docs.gitlab.com/ce/user/project/protected_branches.html)

## Improved Diffs

Whether you create or review code and content, you are spending a lot of time
looking at diffs, so they should work really well. With GitLab 8.10 diffs will
render faster and have even learned a few new tricks.

### Better Side-by-Side Diffs

We've improved side-by-side diffs so that they now accurately show you the
changes side-by-side.

![Better side-by-side diffs in GitLab 8.10](/images/8_10/side1.png)

### Inline Diffs

When you have specific inline changes, we'll now show the exact changes that
were made, rather than just the entire line:

![Inline diffs in GitLab 8.10](/images/8_10/inline1.png)

### Collapsable Diffs

Diffs can now be collapsed by clicking on the filename, allowing you
to review file-by-file.

![Collapsable diffs in GitLab 8.10](/images/8_10/cdiff.png)

Very large diffs ([> 10kb][10kb]) will automatically be collapsed and can be expanded on
demand. This should go a long way into improving working with large diffs with
many files.

[10kb]: https://gitlab.com/gitlab-org/gitlab_git/merge_requests/101#note_13100125

## Manual Actions to Trigger Pipeline Jobs

You've already got your
[CI/CD pipeline](http://docs.gitlab.com/ce/ci/pipelines.html) configured to
continuously deploy changes, right? Well maybe you're not ready to have it
automatically deploy to production. You might automatically deploy to staging,
but you want to do manual QA before deploying to production.

Now you can define
how to deploy to production and using `when: manual`, a new action will appear
in the web UI so that you or your release manager can trigger that part of the
pipeline manually. You can define any kind of job in your pipeline to be
performed at a later time, when a user chooses.

![Manual Actions with Pipelines in GitLab 8.10](/images/8_10/ci_manual1.png)

The actions also show up in the environments, making it easy to promote from
staging to production:

![Manual Actions with Pipelines in GitLab 8.10](/images/8_10/ci_manual2.png)

> [Read our docs on getting started with GitLab CI](http://docs.gitlab.com/ce/ci/quick_start/README.html)
> [Documentation on Environments and Deployments in GitLab CI](http://docs.gitlab.com/ce/ci/environments.html)

## Blockquote Fence Syntax

If you want to quote multiple lines in markdown, you no longer have to
prepend every sentence with `>`, rather you can use the new fence syntax
in GitLab:

```
>>>
This will all become a quote.

Independent of the amount of line breaks.

Yay!
>>>
```

> [Read how to use GitLab Flavored Markdown](http://docs.gitlab.com/ce/markdown/markdown.html#gitlab-flavored-markdown-gfm)

## Multiple Repository Mount Points

You now have the option to distribute storage load over multiple mount points.
Simply define the alternative mount points in your `gitlab.rb` file:

```
git_data_dirs({
  "default" => "/var/opt/gitlab/git-data",
  "alternative" => "/mnt/nas/git-data"
})
```

In the GitLab admin you are able to configure under which mount point
new repositories will be stored.

> [Read the documentation on multiple mount points](http://docs.gitlab.com/ce/administration/repository_storages.html)

## Bulk Subscribe to Issues

You can now bulk subscribe and unsubscribe to issues, making it easier to start
following new activity in a project you just joined or to quiet some of the
email noise.

![Bulk subscribe to issues in GitLab 8.10](/images/8_10/bulk_sub.gif)

## Custom Notification Level for Groups

In GitLab 8.9 [we added a custom notification to projects][custom-not], allowing
you to only get notified on what's important to you.

With GitLab 8.10 you can now also set this on a group level, setting this for
all projects except the project that you have overridden with other notification
settings.

[custom-not]: https://about.gitlab.com/2016/06/22/gitlab-8-9-released/#custom-notification-level

## Ticket-based Kerberos authentication (Enterprise Edition)

Before GitLab 8.10 users had to submit their Kerberos username and password on the GitLab sign-in page to authenticate with Kerberos. In GitLab 8.10 Enterprise Edition it is possible for Kerberos users to sign in with one click without ever submitting their password to GitLab, via the new 'Kerberos Spnego' button on the sign-in page.

We have added an OmniAuth provider for Kerberos SPNEGO authentication which reuses code originally [contributed by CERN in GitLab 7.14](https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/6) that enabled ticket-based 'git clone'. If the web browser of the user 'understands' Kerberos and the user has a valid Kerberos ticket on their local machine then the browser can negotiate access to GitLab during sign-in without ever asking the user for a password.

Read the [Kerberos documentation](http://docs.gitlab.com/ee/integration/kerberos.html) to learn how to enable ticket-based Kerberos integration on your GitLab Enterprise Edition server. We will remove support for password-based Kerberos sign-ins in a future release so if you are currently using GitLab with password-based Kerberos sign-ins we recommend that you switch to ticket-based sign-ins.

## Syntax Highlighting

Syntax highlighting has been massively improved with GitLab 8.10.
We've updated [rouge] from 1.11.1 to 2.0.5 and in doing that have added
[new lexers and bugfixes][changelog-rouge]. That means syntax highlighting
for Docker, F#, IDL, and improved highlighting for praat,
JavaScript, Java, C#, Shell, Liquid, Tulip, Markdown, Ruby, Python and YAML!

You can now also override language guessing with a `.gitattributes` entry.

> [See the documentation for details][override-docs].

[changelog-rouge]: https://github.com/jneen/rouge/blob/master/CHANGELOG.md
[override-docs]: http://docs.gitlab.com/ce/user/project/highlighting.html
[rouge]: https://github.com/jneen/rouge

## Disable Access Request

[The ability to request access to a project][access-request] can now be disabled
for a group or project.

By default it's turned on.

[access-request]: https://about.gitlab.com/2016/06/22/gitlab-8-9-released/#request-access-to-a-project

## Better Slack integration

GitLab can notify you on Slack when certain events happen.
For instance, when someone posts a comment, when a merge request is created
or when a build fails.

We've improved the Slack service so you can configure per event to which
Slack channel GitLab should report.

![Improved Slack integration with GitLab 8.10](/images/8_10/slack.png)

> [Read how to setup the Slack service in GitLab](http://docs.gitlab.com/ce/project_services/slack.html)

## Updated Emoji!

We've updated to the 2016 library of [gemojione](https://github.com/jonathanwiesel/gemojione),
adding many new and updated emoji!

![New Emoji in GitLab 8.10!](/images/8_10/new_emoji.png)

## Domain Blacklist

You can now block certain domains from signing up by adding them to the
domain blacklist. Find the settings in the admin.

> [Read how to blacklist domains in our docs](http://docs.gitlab.com/ce/user/admin_area/settings/sign_up_restrictions.html#blacklist-email-domains)

## Toggle Git Access Protocols

You can now configure Git access controls: enabling or disabling SSH, HTTP or
both.

> [Read how to toggle protocols in our docs](http://docs.gitlab.com/ce/user/admin_area/settings/visibility_and_access_controls.html#enabled-git-access-protocols)

## Inline Videos now supported!

GitLab will now render inline videos in comments and descriptions of
issues and merge requests.

> [How to use GitLab Flavored Markdown](http://docs.gitlab.com/ce/markdown/markdown.html#gitlab-flavored-markdown-gfm)

## Build Warnings

When your CI pipeline passes, but there were some warnings since you
[allow some jobs to fail](http://docs.gitlab.com/ce/ci/yaml/README.html#allow_failure),
GitLab will now tell you in the related merge request:

![Build warnings in GitLab 8.10](/images/8_10/warnings.png)

## Usage Ping (EE only)

To help us better engage with our customers, 8.10 EE periodically attempts to
send license usage back to GitLab, Inc. You can
disable this functionality by unchecking a setting in the application settings
page, which will also show you the _exact_ payload that we're sending.

![License Usage Report](/images/8_10/license_report.png)

## Performance Improvements

GitLab is only getting better every single month, and performance is no
exception. This month we've significantly increased performance for issue
rendering and diff rendering:

![Faster issues in GitLab 8.10](/images/8_10/perf1.png)

![Faster diffs in GitLab 8.10](/images/8_10/perf2.png)

And have made a large amount of further changes, some highlights below with
links to their merge requests.

### Backend

* [HAML has been replaced with Hamlit to reduce memory usage and rendering timings of views](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3666)
* [Certain Git operations are now cached when finding CI pipelines](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4984)
* [Various Git operations on project dashboards are now cached, reducing the time spent in Git whenever the caches exist](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4996)
* [Git operations related to viewing trees of files are only executed when necessary](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4997)
* [The various Markdown reference parsers now re-use SQL queries when used multiple times in the same request, reducing the total number of executed SQL queries](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5020)
* [The column `projects.pushes_since_gc` is only updated at most once per minute, reducing the number of writes to the `projects` table](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5083)
* [Checking if an avatar is present no longer hits the underlying storage engine, reducing the time it takes to check if an avatar is present](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5093)
* [Checking if a user has access to a single project has been optimised](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5102)
* [The queries used to get merge request closing/merging events are now cached per request](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5151)
* [The presence of an external wiki is now cached on database level](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5305)
* [Performance of automatically generating links in Markdown has been improved](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5311)
* [Checking whether to show a system note has been optimized](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5070)
* [The maximum access badge for each author of a comment is now cached to prevent multiple lookups for the same author](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4982)

### Frontend

* [Rendering of diffs has been improved by only rendering certain UI elements when necessary](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4776)
* [Page specific JS loading has been implemented in a better way, reducing the amount of JS to load per page](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4883)
* [Cropper.js has been separated from the main JavaScript file and only load Cropper.js when necessary](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4978)
* [The projects dropdown now only sends the data it needs, reducing the time it takes to load the data](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5113)
* [Discussion notes are not rendered when the diff tab is requested using Ajax](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5130)
* [The code used to check which issues are closed by a merge request is only called when necessary](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5140)

### Monitoring

* [Sidekiq latency is now tracked](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4871)
* [Redis cache hits and misses are now tracked](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4993)
* [The Markdown syntax highlighting filter is instrumented](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5038)

## Runner v1.4

From now on, runner releases will be synchronized with monthly GitLab releases.
Changes in this release (links to merge requests):

* [Use Sentry in GitLab Runner to monitor critical errors](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/217)
* [Improve logging](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/218)
* [Extend support for caching and artifacts for other executors](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/224)
* [Add support for cloning VirtualBox VM snapshots](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/111)
* [Improve support for Docker Machine](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/233)
* [Improve build abort](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/232)

## GitLab Mattermost 3.2

[Mattermost 3.2](https://www.mattermost.org/mattermost-3-2-german-custom-emoji-improved-threaded-messaging-search-windows-and-mac-apps-plus-more/) ships in GitLab 8.10 with German language translation, custom emoji, improved threaded messages, widescreen search, new Exchange and XMPP integrations, plus many more new benefits.

This version also includes [security updates](http://about.mattermost.com/security-updates/) and upgrade from earlier versions is recommended.

## Other changes

This release has more improvements, including security fixes. Please check out [the changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG.md) to see all the named changes.

## Upgrade barometer

To upgrade to GitLab 8.10, about 15 to 30 minutes downtime is required.
Several database columns are renamed and migrations are done for changes in the
code. To prevent faulty data, GitLab will need to be offline during this time.

### Update your NGINX configuration

The default NGINX configuration now overwrites the 'Host' and 'X-Forwarded-Host'
headers. This adds defense in depth against header injection attacks.
For installations from source this means you need to update your NGINX
configuration for GitLab. For Omnibus installations this will happen
automatically, unless you configured your own 'Host' and 'X-Forwarded-Host'
values in `gitlab.rb`.

### Git Hooks renamed to Push Rules and Deprecated API

We renamed Git Hooks to Push Rules and have deprecated the git hooks API,
it will be removed with GitLab 9.0. We recommend you switch to using the
[new push_rules API][push-rules] as soon as possible.

> [Read about Push Rules in our docs](http://docs.gitlab.com/ee/push_rules/push_rules.html#sts=Push Rules)

[push-rules]: http://docs.gitlab.com/ee/api/projects.html#sts=Push Rules (EE only)

### Default behavior

*Note* We assume you are upgrading from the latest version. If not, then also consult the upgrade barometers of any intermediate versions you are skipping.
If you are upgrading from a GitLab version prior to 8.0 *and* you have CI enabled, you have to upgrade to GitLab 8.0 [first](https://about.gitlab.com/2015/09/22/gitlab-8-0-released/).

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

GitLab Enterprise Edition includes advanced features such as LDAP Group support,
merge request approvals, Geo and File locking.
For a complete overview please have a look at the [feature list of GitLab EE]( https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a
[subscription]( https://about.gitlab.com/pricing/).
No time to upgrade GitLab yourself?
A subscription also entitles you to our upgrade and installation services.

- - -
