---
title: "GitLab 8.11.5 released"
author: Rubén Dávila
author_twitter: rdavila
categories: release
---


Today we are releasing version 8.11.5 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version resolves a number of regressions and bugs in the [recent 8.11
release](/2016/08/22/gitlab-8-11-released).

Please read on for more details.

<!-- more -->

- **EE:** API: Restore backward-compatibility for POST /projects/:id/members when membership is locked. ([!715])
- **CE/EE:** Scope webhooks/services that will run for confidential issues. ([!1986])
- **CE/EE:** Fix confidential issues made public after import. ([!1992])
- **CE/EE:** Add the total number of issues in the JSON response in issue board lists. ([!5904])
- **CE/EE:** Changed `.commit-row-title` `line-height` to `1.35` from `1`. ([!5996])
- **CE/EE:** Optimize branch lookups and force a repository reload for Repository#find_branch. ([!6087])
- **CE/EE:** Added search for all lists on issue boards. ([!6101])
- **CE/EE:** Fix suggested colors options for new labels in the admin area. ([!6138])
- **CE/EE:** Remove gitorious from import_sources on ApplicationSetting model. ([!6180])
- **CE/EE:** Fix expiration date picker after update. ([!6184])
- **CE/EE:** Reduce intermittent spec failures by making VueJS resource interceptor decrement outstanding resource counts when HTTP response is received. ([!6224])

[!1986]: https://dev.gitlab.org/gitlab/gitlabhq/merge_requests/1986
[!1992]: https://dev.gitlab.org/gitlab/gitlabhq/merge_requests/1992

[!5904]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5904
[!5996]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5996
[!6101]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6101
[!6087]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6087
[!6138]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6138
[!6180]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6180
[!6184]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6184
[!6224]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6224

[!715]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/715

## Upgrade barometer

This version has some migrations, but should not require any downtime.

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
