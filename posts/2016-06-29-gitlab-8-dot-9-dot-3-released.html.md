---
title: "GitLab 8.9.3 released"
author: Robert Speicher
author_twitter: rspeicher
categories: release
---

Today we are releasing version 8.9.3 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version resolves a number of regressions and bugs in the [recent 8.9
release](/2016/06/22/gitlab-8-9-released/).

Please read on for more details.

<!-- more -->

- **EE:** Roll back Grack::Auth to fix Git HTTP SPNEGO. ([!504])
- **EE:** Fix MR creation on fork of deleted project. ([!503])
- **EE:** Fix `attr_encrypted` in EE. ([!502])
- **CE/EE:** Fix encrypted data backwards compatibility after upgrading `attr_encrypted` gem. ([!4963])
- **CE/EE:** Fix rendering of commit notes. ([!4953])
- **CE/EE:** Resolve "Pin should show up at 1280px min". ([!4947])
- **CE/EE:** Switched mobile button icons to ellipsis and angle. ([!4944])
- **CE/EE:** Correctly returns Todo ID after creating Todo. ([!4941])
- **CE/EE:** Better debugging for memory killer middleware. ([!4936])
- **CE/EE:** Remove duplicate new page button from edit wiki. ([!4904])
- **CE/EE:** Use `clock_gettime` for all performance timestamps. ([!4899])
- **CE/EE:** Use update_columns to bypass all the dirty code on active_record. ([!4985])
- **CE/EE:** Reduce overhead and optimize ProjectTeam#max_member_access performance. ([!4973])
- **CE/EE:** Fixes missing avatar on system notes. ([!4954])
- **CE/EE:** Removed fade when filtering results. ([!4932])
- **CE/EE:** Fixed avatar alignment in new MR view. ([!4901])

[!504]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/504
[!503]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/503
[!502]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/502
[!4971]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4971
[!4963]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4963
[!4953]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4953
[!4947]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4947
[!4944]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4944
[!4941]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4941
[!4936]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4936
[!4904]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4904
[!4899]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4899
[!4985]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4985
[!4973]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4973
[!4954]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4954
[!4932]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4932
[!4901]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4901

## Upgrade barometer

This version does not include any migrations, and should not require any
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

Access to GitLab Enterprise Edition is included with a [subscription](https://about.gitlab.com/subscription).
No time to upgrade GitLab yourself? Subscribers receive upgrade and installation
services.
