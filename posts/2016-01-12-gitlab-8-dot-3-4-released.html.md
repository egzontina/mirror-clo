---
title: "GitLab 8.3.4 Released"
date: 2016-01-12
author: Jacob Vosmaer
author_twitter: jacobvosmaer
---

[GitLab 8.3.3](/2016/01/11/gitlab-8-dot-3-dot-3-released/) depends on
gitlab-workhorse 0.5.3 which has an [API routing
bug](https://gitlab.com/gitlab-org/gitlab-workhorse/issues/14). We have
just released GitLab 8.3.4 and gitlab-workhorse 0.5.4 to fix the routing
bug.

<!-- more -->

If you are running GitLab 8.3.3 you should upgrade to 8.3.4. If you are
still using an earlier version of GitLab then you should skip version
8.3.3.

## Upgrade barometer

This version does not include any new migrations, and should not require
any downtime.

Please be aware that by default the Omnibus packages will stop, run
migrations, and start again, no matter how “big” or “small” the upgrade
is. This behavior can be changed by adding a
[`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

### Update gitlab-workhorse

This version requires gitlab-workhorse version 0.5.4. Omnibus
installations will automatically have the latest version; installations
from source should follow the [update
guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/8-3-stable/doc/update/8.2-to-8.3.md#5-update-gitlab-workhorse)
to ensure the required version is used.

## Updating

To update, check out our [update page](https://about.gitlab.com/update).

## Enterprise Edition

Interested in GitLab Enterprise Edition? Check out the [features
exclusive to EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a
[subscription](http://www.gitlab.com/subscription/). No time to upgrade
GitLab yourself? Subscribers receive upgrade and installation services.
