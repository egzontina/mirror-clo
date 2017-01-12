---
title: "GitLab 8.5.1 Released"
date: 2016-02-24
author: GitLab
author_twitter: gitlab
filename: 2016-02-24-gitlab-8-dot-5-dot-1-released.markdown
---

Today we are releasing version 8.5.1 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version includes several fixes for merge requests, todos, as well as many
UI fixes and improvements.

Read on for all the details!

<!-- more -->

- **EE:** Fix adding pages domain for a project in a group ([!211])
- **CE/EE:** Fix group projects styles ([!2714])
- **CE/EE:** Show Crowd login tab when sign in is disabled and Crowd is enabled ([!2749])
- **CE/EE:** Fix a set of small UI glitches in project, profile, and wiki pages ([!2758])
- **CE/EE:** Restrict permissions on public/uploads ([!2764])
- **CE/EE:** Fix the merge request side-by-side view after loading diff results ([!2880])
- **CE/EE:** Fix the look of tooltip for the "Revert" button ([!2910])
- **CE/EE:** Add when the Builds & Runners API changes got introduced ([!2912])
- **CE/EE:** Fix error 500 on some merged merge requests ([!2917])
- **CE/EE:** Fix an issue causing the content of the issuable sidebar to disappear ([!2919])
- **CE/EE:** Fix error 500 when trying to mark an already done todo as "done" ([!2926])
- **CE/EE:** Fix an issue where MRs weren't sortable ([!2935])
- **CE/EE:** Issues can now be dragged & dropped into empty milestone lists. This is also possible with MRs ([!2935])
- **CE/EE:** Changed padding & background color for highlighted notes ([!2937])
- **CE/EE:** Re-add the newrelic_rpm gem which was removed without any deprecation or warning ([!2943])
- **CE/EE:** Update sentry-raven gem to 0.15.6 ([!2947])
- **Omnibus GitLab:** Push Raspbian repository for RPI2 to packagecloud ([!655])
- **Omnibus GitLab:** Update GitLab pages daemon to v0.2.0 ([!656])
- **Omnibus GitLab:** Unset env variables that could interfere with `gitlab-rake` and `gitlab-rails` commands ([!658])

[!211]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/211
[!2714]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2714
[!2749]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2749
[!2758]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2758
[!2764]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2764
[!2880]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2880
[!2910]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2910
[!2912]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2912
[!2917]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2917
[!2919]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2919
[!2926]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2926
[!2935]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2935
[!2937]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2937
[!2943]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2943
[!2947]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2947
[!655]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/655
[!656]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/656
[!658]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/658

## Re-introduction of the `newrelic_rpm` gem

This release re-introduces the `newrelic_rpm` which was [removed without any
deprecation notice or warning](https://gitlab.com/gitlab-org/gitlab-ce/issues/12860).
We are really sorry about that. Our goal in the long term is to replace the
proprietary NewRelic solution with InfluxDB (MIT License), and Grafana (Apache
2.0 License). We are already using this alternative on GitLab.com and are very
happy with it. That being said, it still
[needs proper documentation](https://gitlab.com/gitlab-org/omnibus-gitlab/issues/1008#note_3825813)
and [built-in dashboards](https://gitlab.com/gitlab-org/omnibus-gitlab/issues/1008#note_3526963)
to be a drop-in replacement for NewRelic.

## Upgrade barometer

This version does not include any new migrations, and should not require any
downtime.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

## Updating

To update, check out our [update page](https://about.gitlab.com/update).

## Enterprise Edition

Interested in GitLab Enterprise Edition? Check out the [features exclusive to
EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself? Subscribers receive upgrade and installation
services.
