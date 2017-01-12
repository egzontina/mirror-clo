---
layout: post
title: "GitLab 8.14.4, 8.13.9, and 8.12.12 Released"
date: 2016-12-08 19:00
author: GitLab
author_twitter: gitlab
categories: security
---

Today we are releasing versions 8.14.4, 8.13.9, and 8.12.12 for GitLab Community
Edition (CE) and Enterprise Edition (EE).

These versions contain important security fixes, and we **strongly
recommend** that all affected GitLab installations be upgraded to one of these
versions **immediately**.

Please read on for more details.

<!-- more -->

## Security fixes in 8.14.4, 8.13.9 and 8.12.12

- **CE/EE:** Replace MR access checks with use of `MergeRequestsFinder` ([#23867])

## Security fixes in 8.14.4

- **CE/EE:** Destroy a user's session when they delete their account. ([#25015])
- **CE/EE:** Filter authentication tokens from Sentry output.
- **CE/EE:** XSS when `LegacyDiffNote` is created on a merge request diff containing HTML ([#25249])
- Thanks to Kristiyan Bogdanov via HackerOne.

## Other fixes in 8.14.4

- **CE/EE:** Fix pipeline author for Slack and use pipeline id for pipeline link ([!7506])
- **CE/EE:** Resolve "Highlighting lines is broken" ([!7090])
- **CE/EE:** Fix pipelines tabs ([!7709])
- **CE/EE:** Fix compatibility with Internet Explorer 11 for merge requests ([!7525])
- **CE/EE:** Authorize users into imported GitLab project ([!7936])
- **CE/EE:** Remove caching of Repository#has_visible_content? ([!7947])
- **CE/EE:** Bump gitlab-shell version to 4.0.3 ([!7953])


- **EE:** Prevent remote mirrors from failing when project is in pending_delete ([!938])

[#23867]: https://gitlab.com/gitlab-org/gitlab-ce/issues/23867
[#25015]: https://gitlab.com/gitlab-org/gitlab-ce/issues/25015
[#25249]: https://gitlab.com/gitlab-org/gitlab-ce/issues/25249

[!7506]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7506
[!7090]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7090
[!7709]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7709
[!7525]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7525
[!7936]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7936
[!7947]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7947
[!7953]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7953
[!938]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/938

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
