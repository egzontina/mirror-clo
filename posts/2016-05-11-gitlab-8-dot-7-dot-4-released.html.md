---
title: "GitLab 8.7.4 Released"
comments: true
author: GitLab
author_twitter: gitlab
date: 2016-05-11 12:00
---

Today we are releasing version 8.7.4 for GitLab Community Edition (CE) and
Enterprise Edition (EE). This release includes two security fixes and as such we
**strongly recommend** that all affected users upgrade their GitLab
installations as soon as possible.

It includes the following fixes:

- **EE:** Delete `ProjectImportData` record only if Project is not a mirror
  ([!370])
- **EE:** Fixed typo in GitLab Geo license check alert ([!379])
- **CE/EE:** Links for Redmine issue references are generated correctly again
  ([!4048])
- **CE/EE:** Fix setting trusted proxies ([!3970])
- **CE/EE:** Fix Bitbucket importer bug when throwing exceptions ([!3941])
- **CE/EE:** Use sign out path only if not empty ([!3989])
- **CE/EE:** Running `rake gitlab:db:drop_tables` now drops tables with cascade
  ([!4020])
- **CE/EE:** Running `rake gitlab:db:drop_tables` uses `IF EXISTS` as a
  precaution ([!4100])

It also includes the following security fixes:

- **CE/EE:** Use a case-insensitive comparison in sanitizing URI schemes
  ([#17299])
- **EE:** Fix LDAP access level spillover bug ([#552])

<!-- more -->

## XSS vulnerability via faulty URI scheme sanitization

The URI scheme of user-supplied links was not being properly sanitized. See
[the issue][#17299] for more details.

Thanks to [Anirudh Anand](https://hackerone.com/a0xnirudh) of [0daylabs] for
responsibly disclosing this issue to us.

## GitLab Enterprise LDAP Group Sync

GitLab Enterprise Edition versions 8.7.0 through 8.7.3 contain an LDAP
group sync bug that can lead to GitLab users being added to GitLab groups they
do not belong to. We do not know if it is possible for a malicious GitLab user
to reliably exploit this bug. Regardless of exploitability, when this bug
strikes it makes unwanted changes to your project access controls.

Versions of GitLab EE prior to 8.7.0 are not affected by this bug. All versions
of GitLab CE are not affected by this bug. If you are not using LDAP group
synchronization in GitLab EE, you are not affected by this bug.

We recommend all users of GitLab EE 8.7.0 through 8.7.3 upgrade to 8.7.4 as soon
as possible.

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

[!370]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/370
[!379]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/379
[!4048]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4048
[!3970]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3970
[!3941]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3941
[!3989]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3989
[!4020]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4020
[!4100]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4100
[#552]: https://gitlab.com/gitlab-org/gitlab-ee/issues/552
[#17299]: https://gitlab.com/gitlab-org/gitlab-ce/issues/17299
[0daylabs]: https://0daylabs.com
