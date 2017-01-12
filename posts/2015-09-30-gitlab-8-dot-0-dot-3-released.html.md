---
title: "GitLab 8.0.3 Released"
date: 2015-09-30
author: GitLab
author_twitter: gitlab
---

Today we are releasing version 8.0.3 for Community Edition (CE) and Enterprise
Edition (EE).

It includes the following fixes:

- **CE/EE:** Fix URL shown in Slack notifications
- **CE/EE:** Fix bug where projects would appear to be stuck in the forked import state
- **CE/EE:** Fix Error 500 in creating merge requests with more than 1000 diffs

<!-- more -->

## Upgrade barometer

This version does not include any new migrations, and should not require any
downtime.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

## Updating

To update, check out our [update page](https://about.gitlab.com/update).

## Enterprise Edition

Interested in GitLab Enterprise Edition?
Check out the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/pricing).
No time to upgrade GitLab yourself?
Subscribers receive upgrade and installation services.
