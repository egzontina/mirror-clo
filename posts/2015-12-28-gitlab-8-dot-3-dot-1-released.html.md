---
title: "GitLab 8.3.1 Released"
date: 2015-12-28
author: GitLab
author_twitter: gitlab
---

Today we are releasing version 8.3.1 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

It includes the following fixes:

- **CE/EE:** Fix Error 500 when global milestones have slashes ([#2182])
- **CE/EE:** Fix Error 500 when doing a search in dashboard before visiting any
  project ([#2110])
- **CE/EE:** Fix LDAP identity and user retrieval when special characters are used ([#2176])
- **CE/EE:** Move Sidekiq-cron configuration to gitlab.yml ([#2087], [#78])
- **CE/EE:** Prevent a possible XSS attack in reference filters ([#2209])
- **EE:** "Group Statistics" renamed to "Contribution Analytics" ([#96])

[#2087]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2087
[#2110]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2110
[#2176]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2176
[#2182]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2182
[#2209]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2209
[#78]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/78
[#96]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/96

<!-- more -->

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
