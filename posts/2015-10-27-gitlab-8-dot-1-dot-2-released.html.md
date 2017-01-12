---
title: "GitLab 8.1.2 Released"
date: 2015-10-27
author: GitLab
author_twitter: gitlab
---

Today we are releasing version 8.1.2 for Community Edition (CE) and Enterprise
Edition (EE).

It includes the following changes:

- **CE/EE:** Require CI jobs to be named
- **CE/EE:** Prevent a 500 error when editing CI services
- **CE/EE:** Correct styling for runner status badge
- **CE/EE:** Fix "Edit Readme" link on project home page
- **CE/EE:** Fix cloning wiki repositories over HTTP
- **CE/EE:** Fix `.gitlab-ci.yml` lint rendering
- **CE/EE:** Allow users in the "Developer" role to manage builds
- **CE/EE:** Fix link to specific runner on the CI build page
- **CE/EE:** Fix Redis version check on Debian
- **CE/EE:** Add migration to automatically remove the satellites directory
- **CE/EE:** Add missing database index for project paths
- **EE:** Prevent a 500 error related to the JIRA external issue tracker service
- **Omnibus**: Fix sysctl code in `gitlab-ctl reconfigure`

<!-- more -->

***Note:*** We planned to release 8.1.1 yesterday but discovered a missing
database index that briefly brought down GitLab.com after we deployed the
release. We're releasing 8.1.2, which includes all of the changes intended for
8.1.1, and adds the missing database index.

This release also addresses a minor security issue introduced in 8.0 that
disclosed the names of CI runners that the user may not have had permission to
view.

## Upgrade barometer

When we [released GitLab 8.0 last month], we promised to automatically remove
the satellites directory in 8.1. This seems to have slipped our minds, but we're
now including a migration to automatically perform the promised cleanup in this
patch release.

Due to this migration, an upgrade to GitLab 8.1.2 may cause your GitLab service
to be offline for longer than a standard patch upgrade. The amount of time
depends on the size of the installation and, by extension, the number of
remaining satellite directories.

If you'd prefer to *manually* remove the satellites directory and avoid waiting
for a potentially lengthy migration to complete, you can use one of the commands
below for either Omnibus installations, or installations from source:

```bash
# Omnibus
sudo gitlab-rails runner "require 'fileutils'; FileUtils.rm_rf(Gitlab.config.satellites.path)"

# Source
cd /home/git/gitlab
sudo -u git -H bundle exec rails runner -e production "require 'fileutils'; FileUtils.rm_rf(Gitlab.config.satellites.path)"
```

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

[released GitLab 8.0 last month]: https://about.gitlab.com/2015/09/22/gitlab-8-0-released/

## Updating

To update, check out our [update page](https://about.gitlab.com/update).

## Enterprise Edition

Interested in GitLab Enterprise Edition?
Check out the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/pricing).
No time to upgrade GitLab yourself?
Subscribers receive upgrade and installation services.
