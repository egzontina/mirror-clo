---
title: "GitLab 8.13.2 released"
author: Rémy Coutable
author_twitter: rymai
categories: release
---

Today we are releasing version 8.13.2 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version resolves a number of regressions and bugs in the [recent 8.13
release](/2016/10/22/gitlab-8-13-released).

Please read on for more details.

<!-- more -->

- **CE/EE:** Fix encoding issues on pipeline commits. ([!6832])
- **CE/EE:** Use Hash rocket syntax to fix cycle analytics under Ruby 2.1. ([!6977])
- **CE/EE:** Modify GitHub importer to be retryable. ([!7003])
- **CE/EE:** Fix refs dropdown selection with special characters. ([!7061])
- **CE/EE:** Fix horizontal padding for highlight blocks. ([!7062])
- **CE/EE:** Pass user instance to `Labels::FindOrCreateService` or `skip_authorization: true`. ([!7093])
- **CE/EE:** Fix builds dropdown overlapping bug. ([!7124])
- **CE/EE:** Fix applying labels for GitHub-imported MRs. ([!7139])
- **CE/EE:** Fix importing MR comments from GitHub. ([!7139])
- **CE/EE:** Fix project member access for group links. ([!7144])
- **CE/EE:** API: Fix booleans not recognized as such when using the `to_boolean` helper. ([!7149])
- **CE/EE:** Fix and improve `Sortable.highest_label_priority`. ([!7165])
- **CE/EE:** Fixed sticky merge request tabs when sidebar is pinned. ([!7167])
- **CE/EE:** Only remove right connector of first build of last stage. ([!7179])

- **EE:** Don't pass a current user to `Member#add_user` in LDAP group sync. ([!830])

- **Omnibus GitLab:** Move `mail_room` queue from `incoming_email` to `email_receiver`. ([!1060])

[!6832]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6832
[!6977]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6977
[!7003]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7003
[!7061]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7061
[!7062]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7062
[!7093]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7093
[!7124]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7124
[!7139]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7139
[!7139]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7139
[!7144]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7144
[!7149]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7149
[!7165]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7165
[!7167]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7167
[!7179]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7179

[!830]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/830

[!1060]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/1060

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
