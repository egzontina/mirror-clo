---
layout: post
title: "GitLab 8.13.5, 8.12.9, and 8.11.11 Released"
date: 2016-11-09 10:30
author: Brian Neel
author_twitter: b0bby_tables
---

Today we are releasing versions 8.13.5, 8.12.9, and 8.11.11 for GitLab
Community Edition (CE) and Enterprise Edition (EE).

These versions contain several security fixes, including a fix for a
persistent cross-site scripting vulnerability and fixes for several
information disclosure vulnerabilities. In addition, version 8.13.5 resolves a
number of regressions and bugs. We recommend that all GitLab installations be
upgraded to one of these versions.

If you're wondering what happened to 8.13.4, good eye! That version introduced
a CI issue that we had to fix in 8.13.5.

Please read on for more details.

<!-- more -->

## 8.13.5, 8.12.9, and 8.11.11 Security Fixes

### Persistent Cross-site Scripting Vulnerability in Autolink Feature

[Mohamed Ebrahem] via [HackerOne] reported a Cross-site Scripting (XSS)
vulnerability in the autolinking feature of our description fields. Autolinking
is used to automatically turn words or phrases into their HTML equivalent links.
The autolinking code did not properly filter dangerous URL protocols and was
therefore vulnerable to persistent script injection. Please see [#23153] for more details.

[Mohamed Ebrahem]: https://www.facebook.com/PSX0S404
[HackerOne]: https://hackerone.com/
[#23153]: https://gitlab.com/gitlab-org/gitlab-ce/issues/23153

## 8.13.5 Security Fixes

The following security issues were fixed ONLY in 8.13.5:

### Private Issue Disclosure from Group Page of Public Repositories

Gustav Bylund reported an information disclosure vulnerability that allowed
confidential issues inside public repositories to be viewed by anyone viewing
the group page. Please see [#22481] for more details.

[#22481]: https://gitlab.com/gitlab-org/gitlab-ce/issues/22481

### Private Merge Request Disclosure in Related Merge Requests Feature

Patrick Fiedler reported an issue where private merge requests in public
projects could be disclosed by creating related merge requests in the same
project. Please see [#23548] for more details.

[#23548]: https://gitlab.com/gitlab-org/gitlab-ce/issues/23548

### Disabled Public Repositories Could Still Be Cloned

An internal code review disclosed that when a public repository is disabled or
restricted to team members only it could still be cloned by the public. Please
see [#23788] for more details.

[#23788]: https://gitlab.com/gitlab-org/gitlab-ce/issues/23788

### Team-Only Merge Requests and Issues Still Visible in Public Activity Feed

An internal code review disclosed that when a public repository has merge
requests and issues disabled for non-team members these merge requests and
issues were still visible in the public activity feed. Please see [#23403] for
more details.

[#23403]: https://gitlab.com/gitlab-org/gitlab-ce/issues/23403

## Regressions fixed in 8.13.5

The following regressions were fixed in 8.13.5:

- **CE/EE:** Fix showing pipeline status for a given commit from correct branch. ([!7034])
- **CE/EE:** Only skip group when it's actually a group in the "Share with group" select. ([!7262])
- **CE/EE:** Introduce round-robin project creation to spread load over multiple shards. ([!7266])
- **CE/EE:** Ensure merge request's "remove branch" accessors return booleans. ([!7267])
- **CE/EE:** Fix lightweight tags not processed correctly by GitTagPushService. ([!6532])
- **CE/EE:** Allow owners to fetch source code in CI builds. ([!6943])
- **CE/EE:** Return conflict error in label API when title is taken by group label. ([!7014])
- **CE/EE:** Reduce the overhead to calculate number of open/closed issues and merge requests within the group or project. ([!7123])
- **CE/EE:** Fix builds tab visibility. ([!7178])
- **CE/EE:** Fix project features default values. ([!7181])

- **EE:** Weight dropdown in issue filter form does not stay selected. ([!826])

[!7034]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7034
[!7262]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7262
[!7266]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7266
[!7267]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7267
[!6532]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6532
[!6943]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6943
[!7014]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7014
[!7123]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7123
[!7178]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7178
[!7181]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7181

[!826]: https://gitlab.com/gitlab-org/gitlabee/merge_requests/826

## Upgrade barometer

These versions **do** include new migrations, and will require brief downtime.

## Updating

To update, check out our [update page](https://about.gitlab.com/update).

## Enterprise Edition

Interested in GitLab Enterprise Edition? Check out the [features exclusive to
EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a
[subscription](https://about.gitlab.com/pricing/). No time to upgrade GitLab
yourself? Subscribers receive upgrade and installation services.
