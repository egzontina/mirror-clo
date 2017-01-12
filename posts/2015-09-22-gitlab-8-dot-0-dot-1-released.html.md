---
title: "GitLab 8.0.1 released"
date: 2015-09-22
author: GitLab
author_twitter: gitlab
---

Hot on the heels of today's [big 8.0 release](/2015/09/22/gitlab-8-0-released/),
we are releasing version 8.0.1 for Community Edition (CE), Enterprise Edition
(EE), and Continuous Integration (CI).

It includes the following fixes:

- **CE/EE/CI**: Improve CI migration procedure and documentation
- **EE**: Correct gem dependency versions
- **EE**: Re-add the "Help Text" feature that was inadvertently removed
- **Omnibus**: Revert "Do not buffer with nginx git http requests"

<!-- more -->

***Update*** *(2015-09-22 22:00 UTC)*: Omnibus packages for this release have
been updated to resolve the [No resource, method, or local variable named
`ci_service`](https://gitlab.com/gitlab-org/gitlab-ce/issues/2670) error some of
our users saw during the upgrade process. Fixed packages have a `.1` Omnibus
patch version (e.g., `8.0.1-ee.1` and `8.0.1-ce.1`). If you've already upgraded
to GitLab 8.0.1 without issue, you can safely ignore this update.

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

Interested in GitLab Enterprise Edition?
Check out the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/pricing).
No time to upgrade GitLab yourself?
Subscribers receive upgrade and installation services.
