---
title: "GitLab 7.13 released with a Customizable Project Dashboard and even better Approvals"
date: 2015-07-22
categories: release
author: GitLab
author_twitter: gitlab
image_title: /images/7_13/ny.jpg
---

It's July and time for GitLab 7.13!
It's been a warm month for most of us but it hasn't slowed us down luckily.
[We raised a seed round](https://about.gitlab.com/2015/07/09/1.5M-raised-in-seed-funding-for-gitlab-to-accelerate-growth-and-expand-operations/) and we [introduced a new logo](https://about.gitlab.com/2015/07/03/our-new-logo/)!

<blockquote class="twitter-tweet" lang="en"><p lang="en" dir="ltr">The new <a href="https://twitter.com/gitlab">@gitlab</a> logo looks pretty awesome :)</p>&mdash; Lev Lazinskiy (@levlaz) <a href="https://twitter.com/levlaz/status/623117535618199552">July 20, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Today, we're happy to bring you a customizable Project Dashboard, better merge request approvals, a number of GitLab CI improvements (Docker support!) and more in this month's GitLab release.

This month's Most Valuable Person ([MVP](https://about.gitlab.com/mvp/)) is Stan Hu. He contributed support for commenting on side-by-side diffs.
This is the third time this year that Stan Hu is MVP, a GitLab hat-trick (three times MVP in the same major release!).
Thanks Stan, we're happy to see you score more great features!

<!--more-->

## Customizable Project Dashboard

We've gotten a lot of requests to make the README the default page of
projects in GitLab. At the same time, many of our contributors didn't like
this idea. They just wanted to see what is happening, not the same README.

We kept redesigning it, looking for a great middle ground.
This time, we made it look good and are giving you the choice of what to see.

Want to see the README first? You can!

![Readme on Project Dashboard](/images/7_13/dash_readme.png)

Rather see the activity in a project? Go ahead!

![Activity on Project Dashboard](/images/7_13/dash_activity.png)

Change it in the settings, alongside the choice for either seeing the starred
projects or all projects on the home page.

![Project Dashboard configuration](/images/7_13/dash_settings.png)


## Comment on Side-by-Side diffs

You can now place comments on side-by-side diffs.

![Comments on side-by-side diff](/images/7_13/side_comment.png)

## Improved Merge Request Approvals (GitLab EE)

With GitLab 7.12, we introduce Merge Request Approvals, allowing you to
set a number of required approvals before a Merge Request can be merged.

This month, we're expanding the Approvals with the ability to set the
specific people that will have to approve a merge request. We've made it
flexible enough that you can have any combination of specific approvers and
unspecific approvers (Mindy and any one else, for instance).

![Approvers in a Merge Request](/images/7_13/approvers_mr.png)

If you want, you can set the default approvers for a project:

![Setting default suggested approvers for a project](/images/7_13/approvers_settings.png)

## Docker support for GitLab CI

This is a really cool new feature.
When configuring your project for GitLab CI, using the new
`.gitlab-ci.yml` file, you can now make use of Docker Images and Services.

This means that all you need to run ruby test suite is the following
`.gitlab-ci.yml` file:

```
image: ruby:2.2
services:
  - postgres:9.3
before_install:
  - bundle install

test:
  script:
  - bundle exec rake spec
```

The Image is the name of any repository present in a local Docker Engine or
any repository that can be found at [Docker Hub](https://registry.hub.docker.com/).

A Service is just another image that is run and linked to your build.
This image can run any application, but the most common use case is to
run a database container such as PostgreSQL.
So instead of having to install PostgreSQl with every build, you can simply
reuse your existing Services image, making your build less
complex and much faster.

For more information about the image and Docker Hub please read the [Docker Fundamentals](https://docs.docker.com/introduction/understanding-docker/).

Read more about this at [Using Docker Images](http://doc.gitlab.com/ci/docker/using_docker_images.html).
See [Using Docker Build](http://doc.gitlab.com/ci/docker/using_docker_build.html) for more information on Docker features.

## allow_failure option for jobs (GitLab CI)

If you want to ignore the status of a specific job when computing the status
of the build for a certain commit, you can now specify this with the
`allow_failure` option in the build script.

It's easy to use in your `.gitlab-ci.yml` file:

```
rspec:
  script: bundle exec rspec
  allow_failure: true
```

## Cancel all Builds (GitLab CI)

If a single commit starts many jobs in your GitLab CI project and you want
to cancel it, previously you'd have to cancel all builds by hand.
Now there is a single button that cancels all builds immediately.

![Quickly cancel all builds](/images/7_13/ci_cancel.png)


## Flexible Build Types (GitLab CI)

We wanted to add flexibility to the configuration of build scripts.
Rather than having predefined build types, you can now group your builds
however you'd like it, with flexible build types.

This allows you to accurately define the behavior and order of builds in
`.gitlab-ci.yml`:

```
types:
  - build
  - test
  - deploy

rspec:
  type: test
  script: bundle exec rspec
```

The script above, for instance, will execute all jobs with the type `build` first, followed by `test` and lastly `deploy`.
The next builds are executed only if all previous succeeds.
And, to speed-up building, all jobs for one type will run in parallel
automatically.

This is the first step towards flexible and powerful build pipelines in
GitLab CI with support for multiple stages.

You can read more information about this feature in [the .gitlab-ci.yml documentation](http://doc.gitlab.com/ci/yaml/README.html).

## Runners without Tags (GitLab CI)

GitLab CI builds and runners can be tagged.
This allows you to do things like running different builds on different platforms. At GitLab we use this to build our packages.

GitLab CI 7.12 and earlier would send tagged builds to runners without tags.
Now, runners without tags will only pick up builds that don't have tags
assigned.

This is a breaking change coming from GitLab CI 7.12. If some of your builds
stop running after you upgrade to 7.13, make sure that your runners have tags
and builds assigned.

## Better Omnibus Documentation

We spend a lot of time writing documentation. Some projects that started small,
like [Omnibus-GitLab](https://gitlab.com/gitlab-org/omnibus-gitlab), end up
becoming major projects with very large documentation. In this specific case,
it could use some restructuring and indexing.

All [Omnibus package documentation](http://doc.gitlab.com/omnibus) can now be
found on our documentation site, [doc.GitLab.com](http://doc.gitlab.com/).

## Other changes

This release has more improvements, including security fixes. Please check out [the CE Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG), [the EE Changelog](https://gitlab.com/gitlab-org/gitlab-ee/blob/master/CHANGELOG-EE) or [the CI Changelog](https://gitlab.com/gitlab-org/gitlab-ci/blob/master/CHANGELOG) to see the all named changes.


## Upgrade barometer

This release upgrade will require downtime.

Coming from 7.12 the database migrations in GitLab and GitLab CI will be fast but they cannot be performed online.

### Update: Custom git hooks no longer trigger for web edits

Due to changes in GitLab, custom git hooks no longer trigger for
commits made through the web UI. They do trigger as normal with pushes
to GitLab.

We're looking into a workaround for the problem and are planning to release
a patch for 7.13 that resolves this issue. Follow [this issue on GitLab.com](https://gitlab.com/gitlab-org/gitlab-ce/issues/1974#note_1845415)
for updates.

### Update: Ruby (MRI) 2.0.x no longer supported

As of this release, we have dropped support for the 2.0.x versions of Ruby (MRI).
We support Ruby (MRI) 2.1.x and recommend using 2.1.6.

### Important notice for GitLab CI installations

GitLab CI now uses symmetric encryption to share 'secure variables'
(provided by your users) in the SQL database.
Symmetric encryption needs a secret key, which GitLab CI will generate for you
when you install / upgrade to 7.13.

The key is called `db_key_base` and can be found in /etc/gitlab/gitlab-secrets.json
(in Omnibus packages) or config/secrets.yml (in installations from source).
If you lose this secret key during a backup restore
or a server migration, your users will lose their 'secure variables'.

Don't store the secret key in the same place as your database backups.
If you do, somebody who steals your backup also gets your users' secure variables.

If you use configuration management (Chef, Puppet etc.) you should
store the secret key securely in your configuration management system.
This way, your CI server uses the correct DB secret key after a server rebuild.


### Changed default location of database socket for Omnibus packages

By default, PostgreSQL places the unix socket file inside of the `/tmp` directory.
Prior to 7.13, GitLab installed using omnibus-gitlab packages would use PostgreSQL default socket location to connect to the database.
This has caused issues when installing GitLab using omnibus-gitlab packages if there is an existing PostgreSQL database.

Given the goal of omnibus-gitlab package to be self contained and not influenced by existing software we've moved the socket location to `/var/opt/gitlab/postgresql`.

If you had previously set `db_host` setting in `/etc/gitlab/gitlab.rb` explicitly for `gitlab_rails` or `gitlab_ci`, be aware that this will possibly require a change. For example, if you had

```ruby
gitlab_rails['db_host'] = '/tmp'
```

this will need to change to

```ruby
gitlab_rails['db_host'] = '/var/opt/gitlab/postgresql'
```

If you didn't change the db_host setting the migration will be completely automatic.
- - -

## Installation

If you are setting up a new GitLab installation please see the
[download GitLab page](https://www.gitlab.com/installation/).

## Updating

Check out our [update page](https://about.gitlab.com/update/).


## Enterprise Edition

The mentioned EE only features and things like LDAP group support can be found in GitLab Enterprise Edition.
For a complete overview please have a look at the [feature list of GitLab EE](http://www.gitlab.com/gitlab-ee/).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/pricing/).
No time to upgrade GitLab yourself?
A subscription also entitles you to our upgrade and installation services.

- - -
