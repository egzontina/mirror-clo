---
title: "GitLab 8.15.1 released"
author: Douglas Barbosa Alexandre
author_twitter: dbalexandre
categories: release
---

Today we are releasing version 8.15.1 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version resolves a number of regressions and bugs in the [recent 8.15
release](/2016/12/22/gitlab-8-15-released).

Please read on for more details.

<!-- more -->

- **CE/EE:** Fix viewing "build failed" TODOs. ([!8262])
- **CE/EE:** Do not show retried builds in pipeline stage dropdown. ([!8260])
- **CE/EE:** Don't render inline math when dollar signs are inside markup. ([!8259])
- **CE/EE:** Do not override incoming Webhook channel for Slack/Mattermost. ([!8270])
- **CE/EE:** Fix Mattermost command creation by specifying username. ([!8257])
- **CE/EE:** Improve autodeploy documentation. ([!8242])
- **CE/EE:** Add more images to issue creation from unresolved discussions. ([!8279])
- **CE/EE:** Stops GFM special characters interfering with markdown tags. ([!8265])
- **CE/EE:** Fix dropdown content non appearing in MR view. ([!8255])
- **CE/EE:** Fix `state_event` parameter to reopen an issue. ([!8246])
- **CE/EE:** Resolve "Titles are bigger than usual". ([!8235])
- **CE/EE:** Adds background color for disabled state to merge when succeeds dropdown. ([!8222])
- **CE/EE:** Add Slack documentation. ([!8269])
- **CE/EE:** Fix format of Slack when result is `nil`. ([!8248])
- **CE/EE:** Fix error 500 on slash commands. ([!8285])
- **CE/EE:** Improve ProcessCommitWorker for large push payloads. ([!8267])
- **CE/EE:** Monkey-patch StrongParameters for ::UploadedFile". ([!8299])
- **EE:** Fix 500 error while navigating to the `pages_domains` 'show' page.. ([!993])

[!8299]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8299
[!8262]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8262
[!8260]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8260
[!8259]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8259
[!8257]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8257
[!8242]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8242
[!8279]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8279
[!8265]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8265
[!8255]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8255
[!8246]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8246
[!8235]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8235
[!8222]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8222
[!8294]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8294
[!8269]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8269
[!8248]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8248
[!8285]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8285
[!8267]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8267
[!8270]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8270
[!993]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/993

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
