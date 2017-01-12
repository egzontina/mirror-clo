---
title: "GitLab 8.10.4 released"
author: Rémy Coutable
author_twitter: rymai
categories: release
date: 2016-08-05 09:00:00
---

Today we are releasing version 8.10.4 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version resolves a number of regressions and bugs in the [recent 8.10
release](/2016/07/22/gitlab-8-10-released/).

Please read on for more details.

<!-- more -->

- **EE:** Fix available users in userselect dropdown when there is more than one userselect on the page. ([!604])
- **EE:** Fix updating skipped approvers in search list on removal. ([!604])
- **CE/EE:** Don't close referenced upstream issues from a forked project. ([#20527])
- **CE/EE:** Fix issue with dropdowns `enter` key not working correctly. ([!5544])
- **CE/EE:** Fix Import/Export project import not working in HA mode. ([!5618])
- **CE/EE:** Fix Import/Export error checking versions. ([!5638])
- **Omnibus GitLab:** Revert Host and X-Forwarded-Host headers in NGINX. ([!902])
- **Omnibus GitLab:** Better handle the SSL certs whitelisted files when the directory has been symlinked. ([!907])
- **Omnibus GitLab:** Fix issue where Mattermost log file is created by the root user. ([!908])

[!604]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/604

[#20527]: https://gitlab.com/gitlab-org/gitlab-ce/issues/20527
[!5544]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5544
[!5618]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5618
[!5638]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5638

[!902]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/902
[!907]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/907
[!908]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/908

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
