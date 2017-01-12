---
title: "GitLab 8.10.5 released"
author: Rémy Coutable
author_twitter: rymai
categories: release
date: 2016-08-10
---

Today we are releasing version 8.10.5 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

Please read on for more details.

<!-- more -->

- **EE:** Used cached value of project count in `Elastic::RepositoriesSearch` to reduce DB load. ([!637])
- **CE/EE:** Add a data migration to fix some missing timestamps in the members table. ([!5670])
- **CE/EE:** Revert the "Defend against 'Host' header injection" change in the source NGINX templates. ([!5706])
- **CE/EE:** Cache project count for 5 minutes to reduce DB load. ([!5746]) & ([!5754])
- **Omnibus GitLab:** Pin mixlib-log to version 1.6.0 in order to keep the log open for writes during reconfigure. ([!914])


[!637]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/637

[!5670]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5670
[!5706]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5706
[!5746]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5746
[!5754]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5754

[!914]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/914

## Upgrade barometer

This version has one migration, but should not require any downtime.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

## Updating

To update, check out our [update page](https://about.gitlab.com/update/).

## Enterprise Edition

Interested in GitLab Enterprise Edition? Check out the [features exclusive to
EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](https://about.gitlab.com/pricing/).
No time to upgrade GitLab yourself? Subscribers receive upgrade and installation
services.
