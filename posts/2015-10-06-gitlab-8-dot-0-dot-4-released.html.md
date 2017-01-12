---
title: "GitLab 8.0.4 Released"
date: 2015-10-06
author: GitLab
author_twitter: gitlab
---

Today we are releasing version 8.0.4 for Community Edition (CE) and Enterprise
Edition (EE).

It includes the following fixes:

- **CE/EE**: Fix Message-ID header to be RFC 2111-compliant to prevent e-mails being dropped
- **CE/EE**: Fix referrals for :back and relative URL installs
- **CE/EE**: Fix anchors to comments in diffs
- **CE/EE**: Remove CI token from build traces
- **CE/EE**: Fix "Assign All" button on Runner admin page
- **EE**: Fix multi-project setup for Jenkins

<!-- more -->

**Omnibus-gitlab packages note:** Before announcing this release, inital set of packages that was built contained an error.
We've noticed this and yanked the packages(version 8.0.4-ce.0). Sadly, the packages were publicly available before this blogpost was live so if you installed/upgraded your GitLab in the timeframe(approx 12:00PM-12:45PM CET on Oct. 06, 2015.) where the broken packages were available, you will run into a `SyntaxError` during installation.
Run `sudo apt-get update` to get the correct version of the package (8.0.4-ce.1) and install the package again with `sudo apt-get install gitlab-ce` (or `gitlab-ee`).

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
