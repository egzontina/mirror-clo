---
title: "GitLab 8.6.4, 8.5.9, 8.4.7, and 8.3.6 Released"
date: 2016-04-04 12:00
author: GitLab
author_twitter: gitlab
---

Today we are releasing versions 8.6.4, 8.5.9, 8.4.7, and 8.3.6 for GitLab
Community Edition (CE) and Enterprise Edition (EE).

These versions include a minor security fix.

Read on for all the details!

<!-- more -->

- **CE/EE:** Don't attempt to fetch any tags from a forked repo. ([!3504])

[!3504]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3504

## Minor security issue with tags and forks

Prior to these versions, it was possible for the Git tags from a fork project to
appear in the source project, if a merge request was opened on the source
project from the fork project, and then new tags were pushed to the forked
project. Tags that already existed in the source project would not be
overwritten.

> **Update:** _(2016-04-05 22:45 UTC)_
>
> As promised, we have included this security fix for the previous four GitLab
> monthly releases, and have released new packages for each.

## Upgrade barometer

These versions do not include any new migrations, and should not require any
downtime.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

## Updating

To update, check out our [update page](https://about.gitlab.com/update).

## Enterprise Edition

Interested in GitLab Enterprise Edition? Check out the [features exclusive to
EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](https://about.gitlab.com/pricing/).
No time to upgrade GitLab yourself? Subscribers receive upgrade and installation
services.
