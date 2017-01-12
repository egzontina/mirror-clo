---
title: "GitLab 8.10.1 released"
author: Rémy Coutable
author_twitter: rymai
categories: release
---


Today we are releasing version 8.10.1 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version resolves a number of regressions and bugs in the [recent 8.10
release](/2016/07/22/gitlab-8-10-released/).

Please read on for more details.

<!-- more -->

- **CE/EE:** Refactor repository storages documentation. ([!5428])
- **CE/EE:** Gracefully handle case when keep-around references are corrupted or exist already. ([!5430])
- **CE/EE:** Add detailed info on storage path mountpoints. ([!5437])
- **CE/EE:** Fix Error 500 when creating Wiki pages with hyphens or spaces. ([!5444])
- **CE/EE:** Fix bug where replies to commit notes displayed in the MR discussion tab wouldn't show up on the commit page. ([!5446])
- **CE/EE:** Ignore invalid trusted proxies in `X-Forwarded-For` header. ([!5454])
- **CE/EE:** Add links to the real `markdown.md` file for all GFM examples. ([!5458])
- **Omnibus GitLab:** Fix custom HTTP/HTTPS external ports. ([!887])

[!5428]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5428
[!5430]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5430
[!5437]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5437
[!5444]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5444
[!5446]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5446
[!5454]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5454
[!5458]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5458

[!887]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/887

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
