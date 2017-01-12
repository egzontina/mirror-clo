---
title: "GitLab 8.15.2 released"
author: Robert Speicher
author_twitter: rspeicher
categories: release
---

Today we are releasing version 8.15.2 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version resolves a number of regressions and bugs in the [recent 8.15
release](/2016/12/22/gitlab-8-15-released).

Please read on for more details.

<!-- more -->

---

- **CE/EE:** Fix merge request list timestamp alignment. ([!8271])
- **CE/EE:** Fix discussion overlap text in regular screens. ([!8273])
- **CE/EE:** Fix timeout when MR contains large files marked as binary by `.gitattributes`.
- **CE/EE:** Fix mini-pipeline-graph dropdown animation and stage position in Chrome, Firefox and Safari. ([!8282])
- **CE/EE:** Fix line breaking in nodes of the pipeline graph in Firefox. ([!8292])
- **CE/EE:** Fix confidential warning text alignment. ([!8203])
- **CE/EE:** Hide Scroll Top button for failed build page. ([!8295])
- **CE/EE:** Rename "autodeploy" to "auto deploy".
- **CE/EE:** Disable PostgreSQL statement timeouts when removing unneeded services. ([!8322])
- **CE/EE:** Fix finding the latest pipeline. ([!8301])
- **CE/EE:** Fixed GFM autocomplete error when no data exists.
- **CE/EE:** Added ability to put emojis into repository name. ([!7420])
- **CE/EE:** Fixed resolve discussion note button color.
- **EE:** Add hover states for collapsed Issue/Merge Request sidebar for Time tracking Icon
- **EE:** Fix ElasticSearch search for non-default branches ([!999])
- **Omnibus GitLab** Add a delay option for pg-upgrade ([!1164])

[!8271]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8271
[!8273]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8273
[!8282]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8282
[!8292]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8292
[!8203]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8203
[!8295]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8295
[!8322]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8322
[!8301]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/8301
[!7420]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7420
[!999]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/999
[!1164]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/1164

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
