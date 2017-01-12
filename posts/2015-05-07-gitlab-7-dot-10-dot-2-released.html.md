---
title: "GitLab 7.10.2 released"
date: 2015-05-07
author: Job van der Voort
author_twitter: Jobvo
---

Please note that we have discovered an issue in the migrations in this patch
release. The tag migration will fail on certain duplicate tags in the database.

**Do not upgrade to 7.10.2 at this time.**

If you have already updated to 7.10.2 and everything is working fine,
there is no need to worry. You can keep using GitLab normally.

---

We've released GitLab 7.10.2 CE, EE and CI.

It includes the following fixes, that apply to both CE and EE:

- A bug when using the Gitorious importer
- A bug that prevented adding group members through the admin screen
- Broken links on the merge request page leading to CI services
- A 500 error when trying to search in the wiki
- A 500 error when trying to add new tags to a project
- A bug where commit data would not appear in some subdirectories due to escaped slashes
- A bug where branches with escaped characters in their names would not always work
in the compare view

<!-- more -->

## Upgrade barometer

There is a migration that loops through all tags.
This can take a while for larger installations.

The upgrade can be performed online.

Theoretically, there is a small chance that if a tag is created during
the [migration](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/db/migrate/20150425164649_add_taggings_counter_cache_to_tags.acts_as_taggable_on_engine.rb)
of that specific tag, the tag counter gets a value that is
slightly higher or lower than its actual value. We do not believe this
is reason to schedule downtime and recommend performing the upgrade online.

## Updating

To update, check out our [update page](https://about.gitlab.com/update).

## Enterprise Edition

Omnibus packages for GitLab Enterprise Edition 7.10.2 are available for subscribers [here](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/install/packages.md). For installations from source, use [this guide](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/update/patch_versions.md).

Interested in GitLab Enterprise Edition?
For an overview of feature exclusive to GitLab Enterprise Edition please have a look at the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.
