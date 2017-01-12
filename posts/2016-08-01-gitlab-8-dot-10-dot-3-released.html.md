---
title: "GitLab 8.10.3 released"
author: Rémy Coutable
author_twitter: rymai
categories: release
---

Today we are releasing version 8.10.3 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version resolves a number of regressions and bugs in the [recent 8.10
release](/2016/07/22/gitlab-8-10-released/).

Please read on for more details.

<!-- more -->

- **EE:** Fix regression in Git Annex permission check. ([!599])
- **EE:** [Elastic] Fix commit search for some URLs. ([!605])
- **CE/EE:** Fix Import/Export issue importing milestones and labels not associated properly. ([!5426])
- **CE/EE:** Fix timing problems running imports on production. ([!5523])
- **CE/EE:** Add a log message when a project is scheduled for destruction for debugging. ([!5540])
- **CE/EE:** Fix hooks missing on imported GitLab projects. ([!5549])
- **CE/EE:** Properly abort a merge when merge conflicts occur. ([!5569])
- **CE/EE:** Fix importer for GitHub Pull Requests when a branch was removed. ([!5573])
- **CE/EE:** Ignore invalid IPs in `X-Forwarded-For` when trusted proxies are configured. ([!5584])
- **CE/EE:** Trim extra displayed carriage returns in diffs and files with CRLFs. ([!5588])


[!599]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/599
[!605]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/605

[!5426]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5426
[!5523]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5523
[!5540]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5540
[!5549]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5549
[!5569]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5569
[!5573]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5573
[!5584]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5584
[!5588]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5588

## Upgrade barometer

This version has no migrations and should not require any downtime.

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
