---
title: "GitLab 7.10.5 released"
date: 2015-05-27
author: Job van der Voort
author_twitter: Jobvo
---

In GitLab 7.11 we have [introduced](https://about.gitlab.com/2015/05/22/gitlab-7-11-released/)
the requirement of a license key for users of GitLab Enterprise Edition.

This can cause a moment of downtime when upgrading, as you will need to upload
the license key before being able to push to the GitLab instance.

With this patch release we're adding a license upload functionality that allows
you to upload your license in GitLab 7.10.5, preventing downtime when upgrading
to GitLab 7.11 Enterprise Edition.

This patch release also includes a fix for GitLab Annex and patches a MySQL
vulnerability in GitLab CI.

If you are not using GitLab Enterprise Edition,
you can skip this patch and go straight to [GitLab 7.11](https://about.gitlab.com/2015/05/22/gitlab-7-11-released/).

<!-- more -->

## Upgrade barometer

This is a minor update, without any migrations.
No downtime is necessary.

## Updating

To update, check out our [update page](https://about.gitlab.com/update).

As Enterprise Edition user, if you want to update to 7.10.5 rather than straight to 7.11,
download and install the Omnibus package
[at the old download location, here.](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/install/packages.md).
For installations from source, use [this guide](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/update/patch_versions.md).

## Enterprise Edition

Interested in GitLab Enterprise Edition?
For an overview of feature exclusive to GitLab Enterprise Edition please have a look at the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/pricing).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.
