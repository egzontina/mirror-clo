---
title: "GitLab 8.12.4 released"
author: Rubén Dávila
author_twitter: rdavila
categories: release, security
---

Today we are releasing version 8.12.4 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version contains two security fixes for GitLab, plus fixes for minor regressions and bugs in the [recent 8.12
release](/2016/09/22/gitlab-8-12-released).

Please read on for more details.

<!-- more -->

- **EE:** Indexer works with smaller batches of repositories to not exceed NOFILE limit. ([!774])

- **CE/EE:** Fix tooltip text when Copy to cliboard is clicked. ([!6294])
- **CE/EE:** Fix build sidebar build details padding. ([!6506])
- **CE/EE:** Changed compare dropdowns to dropdowns with search input. ([!6550])
- **CE/EE:** Fix race condition on LFS Token. ([!6592])
- **CE/EE:** Fix bug when trying to cache closed issues from external issue trackers. ([!6619])
- **CE/EE:** Fix lint-doc error. ([!6623])
- **CE/EE:** Skip wiki creation when GitHub project has wiki enabled. ([!6665])
- **CE/EE:** Fix issues importing services via Import/Export. ([!6667])
- **CE/EE:** Restrict failed login attempts for users with 2FA. ([!6668])
- **CE/EE:** Fix project deletion when feature visibility is set to private. ([!6688])

[!774]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/774

[!6294]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6294
[!6506]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6506
[!6550]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6550
[!6592]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6592
[!6619]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6619
[!6623]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6623
[!6665]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6665
[!6667]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6667
[!6668]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6668
[!6688]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6688


## Further improvements for security of Import/Export projects.

Prevented access to foreign entities using the Import/Export functionality. This could be achieved altering the foreign key IDs in the project JSON of an exported GitLab project file. The foreign keys are now always being ignored at the time of importing a project. See [#20821] for more information.

[#20821]: https://gitlab.com/gitlab-org/gitlab-ce/issues/20821

## Exported projects were world-readable in the filesystem

Exported projects are no longer world-readable in the GitLab server filesystem as permissions are set to owner access only. See [#22757] for more information.

[#22757]: https://gitlab.com/gitlab-org/gitlab-ce/issues/22757

## Prevent a 2FA brute force attack

Incorrect two-factor authentication (2FA) code submissions were not incrementing
the number of failed login attempts as intended, leading to a possible brute
force attack on accounts with 2FA enabled. See [#19799] for more information.

Thanks to [Pete Yaworski](https://twitter.com/yaworsk) for responsibly
disclosing this issue via [HackerOne](https://hackerone.com/gitlab).

[#19799]: https://gitlab.com/gitlab-org/gitlab-ce/issues/19799

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
