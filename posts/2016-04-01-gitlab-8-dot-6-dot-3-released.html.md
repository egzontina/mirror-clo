---
title: "GitLab 8.6.3 Released"
date: 2016-04-01 16:00
author: GitLab
author_twitter: gitlab
---

Today we are releasing version 8.6.3 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version includes, once again many fixes and improvements.

Read on for all the details!

<!-- more -->

- **EE:** Fix other cases where git hooks would fail due to old commits. ([!310])
- **EE:** Exit ElasticIndexerWorker's job happily if record cannot be found. ([!311])
- **EE:** Fix "Reload with full diff" button not working. ([!313])
- **CE/EE:** Destroy related todos when an Issue/MR is deleted. ([!3376])
- **CE/EE:** Fix error 500 when target is nil on todo list. ([!3376])
- **CE/EE:** Fix copying uploads when moving issue to another project. ([!3382])
- **CE/EE:** Ensuring Merge Request API returns boolean values for work_in_progress. ([!3432])
- **CE/EE:** Fix raw/rendered diff producing different results on merge requests. ([!3450])
- **CE/EE:** Fix commit comment alignment. ([!3466])
- **CE/EE:** Update gitlab-shell version and doc to 2.6.12. ([!280])
- **CE/EE:** Mentions on confidential issues doesn't create todos for non-members. ([!3374])
- **CE/EE:** Allow temporary email as notification email. ([!3477])

[!280]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/280
[!310]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/310
[!311]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/311
[!313]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/313

[!3376]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3376
[!3376]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3376
[!3382]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3382
[!3432]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3432
[!3450]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3450
[!3466]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3466
[!3374]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3374
[!3477]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3477

## Upgrade barometer

This release includes two minor database migrations for CE. All the migrations
can be run without causing any downtime.

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
