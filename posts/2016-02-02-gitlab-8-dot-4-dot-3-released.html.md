---
title: "GitLab 8.4.3 Released"
date: 2016-02-02
author: GitLab
author_twitter: gitlab
filename: 2016-01-28-gitlab-8-dot-4-dot-2-released.markdown
---

Today we are releasing version 8.4.3 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This patch release includes fixes for and improvements to Elasticsearch
indexing, more fixes for syntax highlighting in diffs, and a few other minor
fixes.

Read on for all the details!

<!-- more -->

- **CE/EE:** Increase lfs_objects size column to 8-byte integer to allow files larger
  than 2.1GB ([!2644])
- **CE/EE:** Correctly highlight MR diff when MR has merge conflicts ([!2632])
- **CE/EE:** Fix highlighting in blame view ([!2630])
- **CE/EE:** Update sentry-raven gem to prevent "Not a git repository" console output
  when running certain commands ([!2636])
- **CE/EE:** Add instrumentation to additional Gitlab::Git and Rugged methods for
  performance monitoring ([!2664])
- **CE/EE:** Allow autosize textareas to also be manually resized ([!2653])
- **EE:** Elasticsearch: fix partial blob indexing on push ([!149])
- **EE:** Elasticsearch: added advanced indexer for repositories ([!154])
- **EE:** Fix "Mirror User" dropdown ([!158])
- **Omnibus GitLab** Update openssl to 1.0.1r ([!621])

[!149]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/149
[!154]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/154
[!158]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/158
[!2630]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2630
[!2632]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2632
[!2636]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2636
[!2641]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2641
[!2644]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2644
[!2653]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2653
[!2664]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2664
[!621]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/621

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

Interested in GitLab Enterprise Edition? Check out the [features exclusive to
EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself? Subscribers receive upgrade and installation
services.
