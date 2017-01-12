---
title: "GitLab 8.5.3 Released"
date: 2016-03-03 17:00
author: GitLab
author_twitter: gitlab
filename: 2016-03-03-gitlab-8-dot-5-dot-3-released.markdown
---

We are releasing version 8.5.3 for GitLab Community Edition (CE) and
Enterprise Edition (EE).
This follows the release of version 8.5.2 earlier today, we try to release fixes as early and often as possible and this is the first time we have two patch releases on the same day.

This version includes one important fix for GitLab Enterprise Edition when
Elasticsearch is enabled, as well as two minor fixes.

Read on for all the details!

<!-- more -->

- **EE:** Prevent LDAP from downgrading a group's last owner ([!216])
- **EE:** Update `gitlab-elastic-search` gem to `0.0.11` ([!234])
- **CE/EE:** Flush repository caches before renaming projects ([!2974])

[!216]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/216
[!234]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/234

[!2974]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2974

## `gitlab-elastic-search` gem update

This patch release updates the `gitlab-elastic-search` gem to `0.0.11`. If you
are using Elasticsearch, this will fix an issue where no CI builds where created
for new merge requests.

## Upgrade barometer

This version does not include any new migrations, and should not require
any downtime.

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
