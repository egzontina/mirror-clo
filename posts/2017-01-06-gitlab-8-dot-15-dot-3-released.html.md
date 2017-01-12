---
title: "GitLab 8.15.3 released"
author: Douglas Barbosa Alexandre
author_twitter: dbalexandre
categories: release
---

Today we are releasing version 8.15.3 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version resolves a number of regressions and bugs in the [recent 8.15
release](/2016/12/22/gitlab-8-15-released).

This version includes a migration which will **rename projects** that became
inaccessible in version 8.15 due to reserved names. We would have preferred
to do this in the monthly release rather than a patch release, but weighed
against inaccessible projects we believe it's a reasonable tradeoff.

<!-- more -->

- **CE/EE:** Rename projects with reserved path names ([!8234])
- **CE/EE:** Whitelist next project names: assets, profile, public ([!8470])
- **CE/EE:** Fix 500 error when visit group from admin area if group name contains dot ([!8342])
- **CE/EE:** Fix GFM dropdown not showing at beginning of new lines ([!8338])
- **CE/EE:** Fix error 500 renaming group. ([!8201])
- **CE/EE:** Pipeline stylesheets changes ([!8224])
- **CE/EE:** Fix cross-project references copy to include the project reference ([!8232])
- **CE/EE:** Revert MattermostNotificationService and SlackNotificationService ([!8240])
- **CE/EE:** Use stable icon for Mattermost integration ([!8252])
- **CE/EE:** Resolve "Labels are not consistent on all pages" ([!8256])
- **CE/EE:** Fix 500 errors when creating a user with identity via API ([!8442])
- **CE/EE:** Remove bottom border from Issuable titles ([!8278])
- **CE/EE:** Fix project hooks params ([!8425])
- **CE/EE:** Gitlab::LDAP::Person uses LDAP attributes configuration ([!8418])
- **CE/EE:** LDAP attributes needs default values ([!8465])
- **CE/EE:** Removes invalid HTML and unneeded CSS to prevent shaking in the pipelines tab ([!8411])
- **CE/EE:** API: extern_uid is a string ([!8404])
- **CE/EE:** Increases pipeline graph drowdown width in order to prevent strange position ([!8399])
- **CE/EE:** Copy, don't move uploaded avatar files ([!8396])
- **CE/EE:** Add API route slack slash commands ([!8362])
- **CE/EE:** Fixed regression of note-headline-light where it was always placed on 2 lines ([!8348])
- **CE/EE:** Fix left border in session tabs ([!8346])
- **CE/EE:** Fix unclear closing issue behaviour on Merge Request show page ([!8345])
- **CE/EE:** Fix grammar error in text about mentioned issues ([!8337])
- **CE/EE:** Only limit container width on issues & MRs within fixed-width container ([!8330])
- **CE/EE:** Cache project authorizations even when user has access to zero projects ([!8327])
- **EE:** Only fetch repo once on secondary after push ([!1015])
- **EE:** Disable LDAP permission override in project members edit list ([!1018])

[!8234]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8234
[!8470]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8470
[!8342]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8342
[!8338]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8338
[!8201]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8201
[!8224]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8224
[!8232]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8232
[!8465]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8465
[!8240]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8240
[!8442]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8442
[!8252]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8252
[!8256]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8256
[!8278]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8278
[!8425]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8425
[!8418]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8418
[!8411]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8411
[!8404]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8404
[!8399]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8399
[!8396]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8396
[!8362]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8362
[!8348]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8348
[!8346]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8346
[!8345]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8345
[!8337]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8337
[!8330]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8330
[!8327]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8327
[!1015]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/1015
[!1018]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/1018

## Upgrade barometer

This version includes a post-deploy migration and should not require
any downtime.

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
