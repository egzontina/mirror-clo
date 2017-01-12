---
layout: post
title: "GitLab 8.14.5, 8.13.10, and 8.12.13 Released"
date: 2016-12-14 19:00
author: GitLab
author_twitter: gitlab
categories: security
---

Today we are releasing versions 8.14.5, 8.13.10, and 8.12.13 for GitLab Community
Edition (CE) and Enterprise Edition (EE).

These versions contain important security fixes, and we recommend that all
affected GitLab installations be upgraded to one of these versions.

Please read on for more details.

<!-- more -->

## Security fixes in 8.14.5, 8.13.10 and 8.12.13

- **CE/EE:** Fix missing Note access checks in by moving Note#search to updated NoteFinder ([#23867])
- **CE/EE:** Filter `incoming_email_token` and `runners_token` parameters ([#25687])

## Security fixes in 8.14.5 and 8.13.10

- **CE/EE:** Issue#visible_to_user moved to IssuesFinder ([#24637])

### Other fixes in 8.14.5, 8.12.13 and 8.13.10

- **CE/EE:** API: Memoize the current_user so that the sudo can work properly. ([!8017])

### Other fixes in 8.14.5

- **Omnibus GitLab**: Add attribute client_output_buffer_limit_slave for redis ([!1147])

- **CE/EE:** Remove 'Leave Project' and 'Leave Group' from settings dropdowns ([!7600])
- **CE/EE:** Fix display hook error message ([!7775])
- **CE/EE:** Shows group members in the project members list ([!7899])
- **CE/EE:** Correct autocomplete for values with special characters ([!7910])
- **CE/EE:** Remove wrong '.builds-feature' class from the MR settings fieldset ([!7930])
- **CE/EE:** Avoid escaping relative links in Markdown twice ([!7940])
- **CE/EE:** Allow branch names with dots on API endpoint ([!7963])
- **CE/EE:** Fixed timeago re-rendering every element ([!7969])
- **CE/EE:** Use a single query in Projects::ProjectMembersController to fetch members ([!7997])
- **CE/EE:** Displays milestone remaining days only when it's present ([!7998])
- **CE/EE:** Fix Crontab typo for PruneOldEventsWorker to run 4x/day instead of 60x/hour ([!8051])
- **CE/EE:** Encode when migrating ProcessCommitWorker jobs ([!8064])
- **CE/EE:** Updates the docs to require GitLab Shell 4.0.3 ([!8050])

- **EE:** Fix milestone total weight is missing on the milestone page ([!944])
- **EE:** Remove wrong '.builds-feature' class from the MR settings fieldset ([!947])
- **EE:** Group members in project members view ([!958])

[!1147]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/1147
[!7600]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7600
[!7775]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7775
[!7899]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7899
[!7910]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7910
[!7930]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7930
[!7940]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7940
[!7963]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7963
[!7969]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7969
[!7997]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7997
[!7998]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7998
[!8051]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8051
[!8017]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8017
[!8064]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8064
[!8050]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8050
[!944]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/944
[!947]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/947
[!958]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/958
[#23867]: https://gitlab.com/gitlab-org/gitlab-ce/issues/23867
[#25687]: https://gitlab.com/gitlab-org/gitlab-ce/issues/25687
[#24637]: https://gitlab.com/gitlab-org/gitlab-ce/issues/24637

## Upgrade barometer

These versions do include a single migration, and will require brief
downtime of typically less than one minute.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

## Updating

To update, check out our [update page](https://about.gitlab.com/update).

## Enterprise Edition

Interested in GitLab Enterprise Edition? Check out the [features exclusive to
EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a
[subscription](https://about.gitlab.com/pricing/). No time to upgrade GitLab
yourself? Subscribers receive upgrade and installation services.
