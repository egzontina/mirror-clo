---
title: "GitLab 8.10.6, 8.9.7, and 8.8.8 released"
author: Robert Speicher
author_twitter: rspeicher
categories: release, security
---

Today we are releasing versions 8.10.6, 8.9.7, and 8.8.8 for GitLab Community
Edition (CE) and Enterprise Edition (EE).

Version 8.10.6 contains a security fix for GitLab, plus fixes for minor
regressions. All versions include a security update for Rails. We recommend that
all GitLab installations be upgraded to one of these versions.

Please read on for more details.

<!-- more -->

- **CE/EE:** Upgrade Rails to 4.2.7.1. ([!5781])
- **CE/EE:** Fix privilege escalation via project export.
- **CE/EE:** Restore "Largest repository" sort option on Admin > Projects page. ([!5797])
- **CE/EE:** Require administrator privileges to perform a project import.
- **EE:** Fix race condition with UpdateMirrorWorker Lease. ([!641])

[!5781]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5781
[!5797]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5797
[!641]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/641

## Privilege escalation via project export

Due to incorrect attribute whitelisting, it was possible for a project export to
contain the full User attributes of project members, including their API tokens.
See [the issue][20974] for more details.

***Update (2016-08-17 22:00 UTC):*** We have temporarily made importing a GitLab
project export require administrator access while we further audit the security
of the import/export feature as a whole.

Thanks to [Jobert Abma](https://twitter.com/jobertabma) of
[HackerOne](https://hackerone.com/jobert) for responsibly disclosing this issue
to us.

[20974]: https://gitlab.com/gitlab-org/gitlab-ce/issues/20974

## Rails security update

Rails [recently released version 4.2.7.1][rails-update] to address two security
vulnerabilities, so we've updated the version included in GitLab.

[rails-update]: http://weblog.rubyonrails.org/2016/8/11/Rails-5-0-0-1-4-2-7-2-and-3-2-22-3-have-been-released/

## Upgrade barometer

These versions do not include any migrations, and should not require any
downtime.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

## Updating

To update, check out our [update page](https://about.gitlab.com/update).

## Sign up for security notices

Want to be alerted to new security patches as soon as they're available? Sign up
for our [Security Newsletter](https://about.gitlab.com/contact/).

## Enterprise Edition

Interested in GitLab Enterprise Edition? Check out the [features exclusive to
EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](https://about.gitlab.com/subscription).
No time to upgrade GitLab yourself? Subscribers receive upgrade and installation
services.
