---
title: "GitLab 8.6.2 Released"
date: 2016-03-30 16:00
author: GitLab
author_twitter: gitlab
---

Today we are releasing version 8.6.2 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version includes many fixes and improvements.

Read on for all the details!

<!-- more -->

- **EE:** Fix old commits triggering git hooks on new branches branched off another branch. ([!281])
- **EE:** Fix issue with deleted user in audit event. ([!284])
- **EE:** Mark pending todos as done when approving a merge request. ([!292])
- **EE:** GitLab Geo: Display Attachments from Primary node. ([!302])
- **CE/EE:** Fix dropdown alignment. ([!3298])
- **CE/EE:** Fix issuable sidebar overlaps on tablet. ([!3299])
- **CE/EE:** Make dropdowns pixel perfect. ([!3337])
- **CE/EE:** Fix order of steps to prevent PostgreSQL errors when running migration. ([!3355])
- **CE/EE:** Fix bold text in issuable sidebar. ([!3358])
- **CE/EE:** Fix error with anonymous token in applications settings. ([!3362])
- **CE/EE:** Fix the milestone 'upcoming' filter. ([!3364]) & ([!3368])
- **CE/EE:** Fix comments on confidential issues showing up in activity feed to non-members. ([!3375])
- **CE/EE:** Fix `NoMethodError` when visiting CI root path at `/ci`. ([!3377])
- **CE/EE:** Add a tooltip to new branch button in issue page. ([!3380])
- **CE/EE:** Fix an issue hiding the password form when signed-in with a linked account. ([!3381])
- **CE/EE:** Add links to CI setup documentation from project settings and builds pages. ([!3384])
- **CE/EE:** Fix an issue with width of project select dropdown. ([!3386])
- **CE/EE:** Remove redundant `require`s from Banzai files. ([!3391])
- **CE/EE:** Fix error 500 with cancel button on issuable edit form. ([!3392]) & ([!3417])
- **CE/EE:** Fix background when editing a highlighted note. ([!3423])
- **CE/EE:** Remove tabstop from the WIP toggle links. ([!3426])
- **CE/EE:** Ensure private project snippets are not viewable by unauthorized people.
- **CE/EE:** Gracefully handle notes on deleted commits in merge requests. ([!3402])
- **CE/EE:** Fixed issue with notification settings not saving. ([!3452])
- **Omnibus GitLab:** Updated chef version to 12.6. ([!704])
- **Omnibus GitLab:** Use `:before` from Chef 12.6 to enable extension before migration or database seed. ([!705])

[!281]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/281
[!284]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/284
[!292]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/292
[!302]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/302

[!3298]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3298
[!3299]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3299
[!3337]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3337
[!3355]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3355
[!3358]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3358
[!3362]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3362
[!3364]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3364
[!3368]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3368
[!3375]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3375
[!3377]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3377
[!3380]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3380
[!3381]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3381
[!3384]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3384
[!3386]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3386
[!3392]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3392
[!3391]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3391
[!3417]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3417
[!3423]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3423
[!3426]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3426
[!3402]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3402
[!3452]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3452

[!704]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/704
[!705]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/705

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
