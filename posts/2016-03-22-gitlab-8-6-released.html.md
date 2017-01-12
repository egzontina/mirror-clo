---
title: "GitLab 8.6 released with Deploy to Kubernetes and Subscribe to Label"
date: 2016-03-22
categories: release
author: Job van der Voort
author_twitter: Jobvo
image_title: /images/8_6/head.jpg
---

Never have there been more people contributing to GitLab. And you can see it.

Whether you're leading a large open source project, managing thousands of
private, interlinked projects, or even just use GitLab by yourself,
with GitLab 8.6 your life is going to get a whole lot easier.

Not only can you now effortlessly deploy to Kubernetes,
it's now _so much_ easier to only get the messages you need with
the ability to subscribe to labels. On top of that,
we made _many_ things faster and better looking.

This month's Most Valuable Person ([MVP](https://about.gitlab.com/mvp/)) is
Marcia Ramos for helping us [improving GitLab Pages documentation][gl-pages]
and being a great contributor to the GitLab community. Being an MVP doesn't
necessarily mean contributing code to GitLab!

Thanks Marcia!

[gl-pages]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/212

<!--more-->

## Deploy straight from GitLab CI to Kubernetes

GitLab has always been the place where your projects start their life,
where you collaborate in issues and diffs and even test your code.
Now, GitLab is also the place where you ship your code quickly and easily
to Kubernetes.

We want to make easy to deploy straight from GitLab CI in one step,
without any custom scripts.

Redspread is a company in the current Y Combinator batch (Winter 2016).
They noticed an incredible increase in Kubernetes usage among early stage
startups. Many startups in this YC batch and recent alumni are evaluating
or already using Kubernetes in production.

Redspread’s open source command line tool,
[Spread](https://github.com/redspread/spread),
allows command line deployments to
Kubernetes. It uses the current `kubectl` context to read
a project directory and
automatically create or update any Kubernetes objects. It made sense to
integrate Spread with GitLab CI, since GitLab CI focuses on automating
deployment.

To use Spread with GitLab CI:

1. Add the correct image to .gitlab-ci.yml:

```YAML
deploy:
  stage: deploy
  image: redspreadapps/gitlabci
  script:
  - null-script
```

2. Set the environment variables to what makes sense. [See the documentation of the environment variables](https://github.com/ethernetdan/spread/blob/gitlab-ci/images/gitlabci/README.md).

_Note: to use Spread with GitLab CI Variables, you will need [GitLab Runner 1.1](https://about.gitlab.com/2016/03/29/gitlab-runner-1-1-released/).

## Subscribe to a Label

If you don't want to miss issues that are important to you, simply
subscribe to a label! You'll get notified whenever the label gets added to
an issue, making sure you don't miss a thing.

![Subscribe to a label in GitLab 8.6](/images/8_6/subscribe-to-label.png)

If you work on a large or popular project, try subscribing only to the labels
that are relevant to you. You'll notice it'll be much easier to focus on what's
important.

## Confidential Issues

At GitLab [we're all about being open][open], but you can't share everything.
For sensitive subjects, you can now make a confidential issue in a project.
This issue will only be visible to the members of the project and the creator of
the issue, even if the project is public or internal.

This means people can now safely report security issues to your open source
projects. You can communicate with them right there and then, without having
to rely on external applications.

![Use confidential issue for sensitive matters in GitLab 8.6](/images/8_6/confidential-issue.png)

[open]: https://about.gitlab.com/2015/08/03/almost-everything-we-do-is-now-open/

## External Users

Internal projects allow you to practice [innersourcing],
sharing projects internally as if they're open source, but protecting them
as if they are private.

This is something we see more and more organisations adopt, but especially
larger organisations often have external parties working together with them.
These people also need access to GitLab, but not to the internal projects.

To prevent certain users from accessing internal projects, you can now mark
them as _External_. It's a simple check in the users' page that can be set
by any administrator.

In a future release, we'll be adding the ability to have this set automatically
based on LDAP membership.

> [Read about external users in our documentation](http://doc.gitlab.com/ce/permissions/permissions.html#external-users)

[innersourcing]: https://about.gitlab.com/2014/09/05/innersourcing-using-the-open-source-workflow-to-improve-collaboration-within-an-organization/

## Better Dropdowns

This seems like a minor update, but just try them!
The dropdowns all over GitLab have been improved. Especially the filters
for lists are now much more functional and easier to use.

You can quickly add multiple labels and even make new labels on the go.
This release contains hundreds of improvements to the interface, big and small,
we hope you appreciate them!

![Awesome dropdowns in GitLab 8.6](/images/8_6/create-label-from-dropdown.gif)

_Another improvement? Try Todos today!_

![Better Todos with GitLab 8.6](/images/8_6/fast-todos.gif)

## Delete Issues

Sometimes, simply closing an issue or merge request is not sufficient.
For those times, we are now making it possible to delete issues and merge
requests.

Only `owners` can delete issues by editing the issue or merge request and
clicking, you guessed it, `Delete`.

## Move Issues to other Projects

If your product consists of multiple GitLab projects,
issues can easily end up in the wrong place.
You can now easily move issues between projects!

![Move issues between projects in GitLab 8.6](/images/8_6/move-issue.png)

The original issue will be copied, closed and referenced,
making sure nothing or no one will be confused with the move.

## Commit Messages in JIRA

If you mention a JIRA issue in a commit,
GitLab will now not only reference the commit with a link,
but now also add the commit message in a comment in the JIRA issue.

We know many people are using JIRA and we're looking forward to more feedback
on how we can improve GitLab's integration with JIRA.

> [Read about GitLab's JIRA integration](http://doc.gitlab.com/ce/project_services/jira.html)

## Group Visibility Level

You can now set the visibility level of groups, just like you could always
do with projects. Groups now have a visibility level icon to show this.

The global restriction for visibility levels, which you can set as an administrator,
also applies to groups. That means that if you set it to `internal`,
the explore page will be empty for anonymous users.

The group level visibility solves
[this popular issue](https://gitlab.com/gitlab-org/gitlab-ce/issues/12658).

> [Read about the group visibility level](http://doc.gitlab.com/ce/public_access/public_access.html#visibility-of-groups)

## GitLab Mattermost 2.1

[Mattermost 2.1](http://www.mattermost.org/mattermost-2-1-android-windows-linux-and-mac-apps-plus-portuguese/)
ships in GitLab 8.6 with new Android, Windows, Linux and Mac apps with full
GitLab SSO support, plus Brazilian Portuguese translation and more.

Mattermost 2.1 contains a [security update](http://docs.mattermost.com/administration/changelog.html#security-update)
and earlier deployments should [upgrade to this version](http://doc.gitlab.com/omnibus/gitlab-mattermost/).

## Other changes

This release has been so full, we didn't have the space to highlight all!
We still want you to know about them, so here are some of them, in short:

- New keyboard shortcut: You can now press `e` to edit any issue / MR.
- YAML frontmatter is now rendered nicely in markdown files.
- No more default password! Set your password on first sign in. [Read more in the docs](http://doc.gitlab.com/ce/install/installation.html#initial-login).
- We now show test coverage in the builds view.
- Support for Golang subpackage fetching, straight from GitLab.
- Issues and Merge Requests now look better on mobile. Finally!
- Quickly create a new branch from an issue, with a dedicated button.
- [SAML customization](http://doc.gitlab.com/ee/integration/saml.html#customization).
- Easily (un)mark merge requests as WIP using a link. No more editing necessary!
- Better table of contents in Wikis!
- [GitLab Geo](http://doc.gitlab.com/ee/gitlab-geo/README.html) now syncs even
more things! We urge you to upgrade to 8.6 if you're interested in Geo.

### Performance improvements

When [we said][making-faster-blog] that [making GitLab faster][8-5-release]
was a priority, we weren't kidding.
Here is some of the work we've done to make GitLab 8.6 faster:

[making-faster-blog]: https://about.gitlab.com/2016/02/25/making-gitlab-faster/
[8-5-release]: https://about.gitlab.com/2016/02/22/gitlab-8-5-released/

- Search performance has been greatly improved for users using PostgreSQL
  _without_ using ElasticSearch. This requires the `pg_trgm` extension (see
  barometer).
- Performance of listing commits has been improved.
- Counting of tags and branches on the commits/branches/tags pages is now a bit
  faster and is cached.
- Performance of retrieving CI services of a project has been improved.
- Project avatars stored in Git repositories are now cached, cutting down request.
  timings for _all_ project pages for projects that don't use an avatar uploaded
  via the web UI. ([!3272](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3272))
- Diffs that are larger than 100 KB are no longer displayed, instead a "This
  diff is too large" message is displayed. This prevents Unicorn timeouts when
  viewing large diffs. ([!3185](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3185))
- The branch commit ahead/behind statistics are no longer pre-cached on every
  push. For projects with lots of branches (e.g. thousands) this can have a huge
  impact on the time it takes for the pre-caching process to complete.
  ([!3274](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3274))
- Indexes were added for `ci_runners.token`
  ([!3249](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3249)) and
  `git_hooks.project_id`. ([!271](https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/271))
- Performance of viewing individual issues is improved by caching certain Git operations.
- We enabled HTTP caching for requests that fetch the raw contents on a single
  file in a Git repository. Cache times range from 1 minute (for 'mutable'
  resources like `https://gitlab.com/gitlab-org/gitlab-ce/raw/master/VERSION`
  which use a branch name) to 1 hour (for immutable resources like
  `https://gitlab.com/gitlab-org/gitlab-ce/raw/17de30f412b5eddaa080006b6dd2aae2bd2d5647/VERSION`
  that use a commit SHA). In addition to this we configured NGINX in the Omnibus
  packages to use up to 1 GB of disk space for proxy caching. These two changes
  combined reduce the load on GitLab servers that get many requests of HTTP
  clients polling a single file in a public repo.
- In GitLab 8.4 we added a 'housekeeping button' to the project settings page.
  This button triggers a
  [git gc](https://www.kernel.org/pub/software/scm/git/docs/git-gc.html) run on
  the project. In GitLab 8.6 we have automated this button: every 10 pushes, but
  no more than once per hour, GitLab will run `git gc` on repositories. This
  should (slightly) improve Git disk use and performance.
- We split `LDAPSyncworker` and `LDAPGroupSync` worker. Performance will be
  greatly improved for large installations. LDAPSyncworker runs once per hour.
  In our benchmark runs, for 20,000 users and 10,000 groups, the sync takes 15
  minutes. This is in contrast to hours or, in extreme cases, 1-2 days for the
  old `LDAPSyncWorker` (which synced groups, too).

### Updates in the omnibus-gitlab package

As GitLab gets improved every release, so does the omnibus-gitlab package.
You can see the changes that package receives for every release in the
[omnibus-gitlab CHANGELOG](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/CHANGELOG.md).

In this release there are some important changes in the bundled software:

- Redis is updated to version 2.8.24
- PostgreSQL is updated to version 9.2.15
- Nginx proxy caching is enabled
- pg_trgm extension is automatically enabled
- Default Nginx http2 support can be disabled if necessary

---

This release has more improvements, including security fixes. Please check out [the changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG.md) to see all the named changes.

## Upgrade barometer

This release includes migrations that require downtime.

Especially for very large instances running PostgreSQL, this upgrade can
take some time. In our instance (with almost a million projects), the PostgreSQL
migrations took more than half an hour, which caused a TCP connection to be dropped.
Connecting using a Unix socket or using TCP keepalive should prevent this.
[This is what we did](https://gitlab.com/gitlab-com/operations/issues/135#note_4303804).

Smaller instances or those running MySQL should have no such issues, but still
require some downtime for migrations.

### Elasticsearch Requirements

We have added a requirement for the Elasticsearch integration with GitLab 8.6.
You now need to have the [Delete By Query Plugin](https://www.elastic.co/guide/en/elasticsearch/plugins/2.0/plugins-delete-by-query.html)
installed, in addition to Elasticsearch 2.0+.

> [Read about the Elasticsearch integration in our documentation](http://doc.gitlab.com/ee/integration/elasticsearch.html)

### Changes for Source installations with PostgreSQL

Starting with GitLab 8.6 PostgreSQL users are required to enable the "pg_trgm"
extension. On certain Linux distributions this will require the installation of
an extra package. Ubuntu, Fedora, and Debian all ship this extension in the
"postgresql-contrib" package. Once installed the extension must be enabled, this
must be done before upgrading to GitLab 8.6 to ensure that all database
migrations succeed. This extension can be enabled by running the following as a
PostgreSQL super user for every GitLab database:

    CREATE EXTENSION IF NOT EXISTS pg_trgm;

Users using GitLab's Omnibus packages do _not_ have to manually enable this
extension as this is done automatically.

To check if the extension is enabled you can run the following query:

    SELECT true AS enabled
    FROM pg_available_extensions
    WHERE name = 'pg_trgm'
    AND installed_version IS NOT NULL;

If the extension is enabled this will produce the following output:

     enabled
    ---------
     t
    (1 row)

MySQL users do not need to take any extra steps.

This release also includes a migration that will create a number of indexes that
rely on the above extension. Creating these indexes may take up to 30 minutes to
complete depending on the amount of data stored in your database. Users are
advised to ensure that any PostgreSQL connections stay active long enough for
this process to complete.

In the unlikely event of this migration failing (or completing partially) users
can run the following SQL commands in their database:

    CREATE INDEX CONCURRENTLY IF NOT EXISTS index_ci_runners_on_token_trigram ON ci_runners USING gin(token gin_trgm_ops);
    CREATE INDEX CONCURRENTLY IF NOT EXISTS index_ci_runners_on_description_trigram ON ci_runners USING gin(description gin_trgm_ops);
    CREATE INDEX CONCURRENTLY IF NOT EXISTS index_issues_on_title_trigram ON issues USING gin(title gin_trgm_ops);
    CREATE INDEX CONCURRENTLY IF NOT EXISTS index_issues_on_description_trigram ON issues USING gin(description gin_trgm_ops);
    CREATE INDEX CONCURRENTLY IF NOT EXISTS index_merge_requests_on_title_trigram ON merge_requests USING gin(title gin_trgm_ops);
    CREATE INDEX CONCURRENTLY IF NOT EXISTS index_merge_requests_on_description_trigram ON merge_requests USING gin(description gin_trgm_ops);
    CREATE INDEX CONCURRENTLY IF NOT EXISTS index_milestones_on_title_trigram ON milestones USING gin(title gin_trgm_ops);
    CREATE INDEX CONCURRENTLY IF NOT EXISTS index_milestones_on_description_trigram ON milestones USING gin(description gin_trgm_ops);
    CREATE INDEX CONCURRENTLY IF NOT EXISTS index_namespaces_on_name_trigram ON namespaces USING gin(name gin_trgm_ops);
    CREATE INDEX CONCURRENTLY IF NOT EXISTS index_namespaces_on_path_trigram ON namespaces USING gin(path gin_trgm_ops);
    CREATE INDEX CONCURRENTLY IF NOT EXISTS index_notes_on_note_trigram ON notes USING gin(note gin_trgm_ops);
    CREATE INDEX CONCURRENTLY IF NOT EXISTS index_projects_on_name_trigram ON projects USING gin(name gin_trgm_ops);
    CREATE INDEX CONCURRENTLY IF NOT EXISTS index_projects_on_path_trigram ON projects USING gin(path gin_trgm_ops);
    CREATE INDEX CONCURRENTLY IF NOT EXISTS index_projects_on_description_trigram ON projects USING gin(description gin_trgm_ops);
    CREATE INDEX CONCURRENTLY IF NOT EXISTS index_snippets_on_title_trigram ON snippets USING gin(title gin_trgm_ops);
    CREATE INDEX CONCURRENTLY IF NOT EXISTS index_snippets_on_file_name_trigram ON snippets USING gin(file_name gin_trgm_ops);
    CREATE INDEX CONCURRENTLY IF NOT EXISTS index_users_on_username_trigram ON users USING gin(username gin_trgm_ops);
    CREATE INDEX CONCURRENTLY IF NOT EXISTS index_users_on_name_trigram ON users USING gin(name gin_trgm_ops);
    CREATE INDEX CONCURRENTLY IF NOT EXISTS index_users_on_email_trigram ON users USING gin(email gin_trgm_ops);
    INSERT INTO schema_migrations VALUES ('20160226114608');

These commands ensure all indexes are in place and mark the migration as having
finished successfully (so Rails doesn't end up trying to run it again).

### Deprecation of download_url in Builds API

We removed `download_url` from the [Builds API](http://doc.gitlab.com/ce/api/builds.html).
Instead we provide [an API for downloading artifacts of builds](http://doc.gitlab.com/ce/api/builds.html#get-build-artifacts).

---

*Note*: We assume you are upgrading from the latest version. If not, then also consult the upgrade barometers of any intermediate versions you are skipping.
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

EE only features and features such as LDAP group support can be found in GitLab Enterprise Edition.
For a complete overview please have a look at the [feature list of GitLab EE]( https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a
[subscription]( https://about.gitlab.com/pricing/).
No time to upgrade GitLab yourself?
A subscription also entitles you to our upgrade and installation services.

- - -

## Join our webcast about 8.6!

In our next webcast on Thursday, March 24th, we'll take a look at the new features in GitLab 8.6.
Our special guest is Douwe Maan, Development Lead here at GitLab.

- Date: Thursday, March 24, 2016
- Time: 5pm (17:00) UTC; 12pm EST; 9am PST
- [Register here][webcast]

Can't make it? Register anyway, and we'll send you a link to watch later.

[webcast]: http://page.gitlab.com/mar242016-release-webcast.html
