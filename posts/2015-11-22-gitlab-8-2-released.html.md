---
title: "GitLab 8.2 released with Award Emoji and Repository Mirroring"
date: 2015-11-22
author: Job van der Voort
author_twitter: Jobvo
image_title: /images/8_2/header2.jpg
---

Back home from our Summit in Amsterdam, we're at full force again and have a
whole lot of awesome new features for GitLab 8.2!

This time we added more emoji power to GitLab and made it much easier to release
versioned software with Releases and Global Milestones. On top of that,
the CI train is rolling full steam ahead with artifacts and caching available
right now!
If you're using GitLab Enterprise, you also get Repository Mirroring, a great
feature if you want to make your intensively-used repositories more easily
reachable all over the planet.

This month's Most Valuable Person ([MVP](https://about.gitlab.com/mvp/)) is Cristian Bica for
allowing users to select the files view as default project view.
Thanks Cristian!

<!--more-->

## Git LFS

We’re excited to announce we’ve added support for Git LFS in GitLab.com, GitLab CE, and GitLab EE. To learn more about this new feature, take a look at our [highlight blog post](https://about.gitlab.com/2015/11/23/announcing-git-lfs-support-in-gitlab/).

## Award Emoji

As a remote worker, you get fewer opportunities for high-fives and thumbs-ups. In order to make virtual celebrations easier, you can now vote on
issues and merge requests using emoji!

![Add award emoji to issues and merge requests in GitLab 8.2](/images/8_2/emoji.png)

This makes it much easier to give and receive feedback, without a long comment thread.
For example, we will start using issues as a replacement for our
[feedback forum](http://feedback.gitlab.com).

## Releases

When creating versioned software, Git tags are ideal. It is not uncommon that you
want to include some extra files and release notes, which are not natively
supported by Git.

With releases you can now add a Markdown-formatted message to any Git tag
and attach any number of files to it.

![Add notes and attachments to a git tag to create a release](/images/8_2/releases.png)

Simply press the edit button next to tags.

## Global Milestones

In GitLab you were already able to create milestones that cover multiple
projects. By giving a milestone the same name across projects, you can view the
grouped issues and merge requests on the dashboard and in groups.

With Global Milestones in GitLab 8.2, we made it possible to immediately create
milestones in multiple projects in a group. This makes it easier to track activity and
progress across groups and projects.

![With Global Milestones, quickly add a milestone to all projects in a group](/images/8_2/global_milestones.png)

## Repository Mirroring (EE only)

If you want to maintain a mirror of a repository in a GitLab instance,
you can now let GitLab handle the mirroring for you automatically in [GitLab
Enterprise Edition](https://about.gitlab.com/pricing/).

![Mirror any repository automatically in GitLab 8.2 EE](/images/8_2/mirroring.png)

There are several use cases for repository mirroring. If you are globally distributed and want
to have a repository available for quick cloning, you can use repository mirroring
to always have an up-to-date, fast mirror of a remote repository.

![Mirror any repository automatically in GitLab 8.2 EE](/images/8_2/mirroring2.png)

Alternatively, if you want to have a public mirror of your project, for instance
on GitLab.com, you can now do so effortlessly.

## Build Artifacts

You were always able to work with the output from your CI builds,
as long as you up/downloaded it somewhere. That's a bit of a hassle, why not
put it on GitLab's server?

With Build Artifacts in GitLab 8.2 you can do this now. By defining `artifacts`
in your `.gitlab-ci.yml`, you can specify which files will get uploaded and
attached to the build on success.

```
artifacts:
  paths:
  - binaries/
  - .config
```

Do you simply want to have all files that are not tracked by Git? You can
with one single setting:

```
artifacts:
  untracked: true
```

This will upload anything from Runner that is not tracked by Git! Then simply
download them from the build:

![Download the build artifact in GitLab 8.2 straight from your builds](/images/8_2/artifacts.png)

To use build artifacts, make sure to upgrade your Runners to 0.7 or higher.
Have a look at
[the artifact documentation for more information](http://doc.gitlab.com/ce/ci/yaml/README.html#artifacts).

In future releases, we aim to introduce artifact expiration, passing artifacts between
builds, and the ability to quickly get an overview of your artifacts.

## CI Runner Caching

When doing CI builds, many builds make use of the same dependencies. Because
Runners start fresh with every run, this means that they spend a lot of time
installing the same things over and over.

With caching now available for builds, this is no longer necessary. You can
specify a list of files and directories that will be cached between builds

For instance, to cache all files in `binaries` and `.config`:

```
rspec:
  script: test
  cache:
    paths:
    - binaries/
    - .config
```

As with Build Artifacts, you can also cache all files that are not tracked by
Git:

```
rspec:
  script: test
  cache:
    untracked: true
```

We hope this will give your Runners some much-needed time off.

For more options, view [the documentation on build caching](http://doc.gitlab.com/ce/ci/yaml/README.html#cache).

## Copy to Clipboard buttons

Want to get a commit SHA or the cross-project reference for an issue or
merge request? Simply click the copy-to-clipboard button to have it ready
for pasting!

![Copy to clipboard with GitLab 8.2](/images/8_2/copy.jpg)

## Search through Commit Messages

When you search, GitLab now also searches through commit messages for you!

![Search through commits with GitLab 8.2](/images/8_2/commit_search.jpg)

## CI Runner improvements

With the release of GitLab 8.2, we're also releasing the new Runner, version 0.7.

The biggest improvement in GitLab Runner 0.7.0 is that the Docker executor now uses
separate containers for: git clone, running builds (as specified in .gitlab-ci.yml),
and a separate container for uploading artifacts.
This means you can use images without git installed
(a limitation of previous releases).

Runners now also come with built-in support for TLS self-signed certificates.

## CI & Shared Runners now on by default

We want everyone to be able to use CI with zero effort or configuration.
That's why we've enabled CI and shared runners by default for all new projects.

This means that all you need to do to start using CI is push your `.gitlab-ci.yml`
and your current shared runners will start working on it!

This is also the case for GitLab.com, where we have a number of shared runners
available for everyone to use.

## Other changes

This release has more improvements, including security fixes. Please check out
[the Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG)
to see the all named changes.

## Upgrade barometer

### Custom Nginx? Update needed!

If you are not using the Omnibus packages and their built-in Nginx settings,
you will have to update your Nginx/Apache settings when upgrading to 8.2.

### Slow-ish migrations

This version contains a (potentially) slow migration that loops through all
records in the 'services' table (project services) to update JIRA settings to a new format.
This took about 5 minutes on our largest server.

### Shared file storage

There is a new config setting for 'shared file storage' in `gitlab.yml` / `gitlab.rb`.
If you run GitLab with NFS or something similar,
you need to make sure this directory is on an NFS share.

### Upgrading from 7.x or before?

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

The mentioned EE-only features and things like Repository Mirroring can be found in GitLab Enterprise Edition.
For a complete overview please have a look at the [feature list of GitLab EE](http://www.gitlab.com/gitlab-ee/).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/pricing/).
No time to upgrade GitLab yourself?
A subscription also entitles you to our upgrade and installation services.

- - -
