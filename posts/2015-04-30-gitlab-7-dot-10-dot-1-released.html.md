---
title: "GitLab 7.10.1 Released"
date: 2015-04-30
categories: release
author: Job van der Voort
author_twitter: Jobvo
---

We've just released GitLab 7.10.1 (CE, EE and CI).

This patch release removes `GroupMembers` that have `nil` as group from the database, for both
GitLab CE and EE.

<!-- more -->

## Upgrade barometer

There is a small migration in the patch that'll only take a few milliseconds to run.
This patch can be performed online if you're coming from 7.10.

## Upgrading

See our [upgrade page](https://about.gitlab.com/update/).

## Enterprise Edition

Omnibus packages for GitLab Enterprise Edition 7.10.1 are available for subscribers [here](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/install/packages.md). For installations from source, use [this guide](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/update/patch_versions.md).

Interested in GitLab Enterprise Edition?
For an overview of feature exclusive to GitLab Enterprise Edition please have a look at the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.
