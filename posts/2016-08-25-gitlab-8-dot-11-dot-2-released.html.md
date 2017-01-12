---
title: "GitLab 8.11.2 released"
author: Rubén Dávila
author_twitter: rdavila
categories: release
---


Today we are releasing version 8.11.2 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version resolves a number of regressions and bugs in the [recent 8.11
release](/2016/08/22/gitlab-8-11-released).

If you're wondering what happened to 8.11.1, good eye! That version was pulled due to a packaging error.

Please read on for more details.

<!-- more -->

- **CE/EE:** Document protected branches new behavior. ([!5934])
- **CE/EE:** Fix typo in gitlab-workhorse header. ([!5891])
- **CE/EE:** Documentation for Issue Boards. ([!5713])
- **CE/EE:** Fix file links on project page Files view. ([!5933])
- **CE/EE:** Also check if Akismet is enabled, before showing the `Submit as spam` button. ([!5948])
- **CE/EE:** Fix incorrect "stopped impersonation" log message. ([!5949])
- **CE/EE:** Fix project namespace links. ([!5912])
- **CE/EE:** Fixed enter key in search input not working. ([!5888])
- **CE/EE:** Bump SimpleCov merge timeout to 365 days. ([!5932])
- **CE/EE:** Remove tab stop from issuable form added by description templates. ([!5929])
- **CE/EE:** Add Ruby 2.3 upgrade notes. ([!5940])
- **CE/EE:** Use gitlab-workhorse 0.7.11. ([!5983])
- **CE/EE:** Does not halt the GitHub import process when an error occurs. ([!5763])
- **CE/EE:** last_push_event widget considers fork events on the main project. ([!5978])

- **Omnibus GitLab:** Fix mail_room URL for Redis. ([!954])
- **Omnibus GitLab:** Fixed a regression where the default container registry and mattermost nginx proxy headers were not being set. ([!958])

[!5934]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5934
[!5891]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5891
[!5713]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5713
[!5933]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5933
[!5948]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5948
[!5949]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5949
[!5912]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5912
[!5888]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5888
[!5932]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5932
[!5929]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5929
[!5940]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5940
[!5983]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5983
[!5763]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5763
[!5978]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5978

[!954]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/954
[!958]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/958

## Upgrade barometer

This version has one migration, but should not require any downtime.

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
