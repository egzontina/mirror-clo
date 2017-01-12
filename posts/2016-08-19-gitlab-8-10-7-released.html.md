---
title: "GitLab 8.10.7, 8.9.8, and 8.8.9 released"
author: Robert Speicher
author_twitter: rspeicher
categories: release, security
---

Today we are releasing versions 8.10.7, 8.9.8, and 8.8.9 for GitLab Community
Edition (CE) and Enterprise Edition (EE).

These versions include a security fix in two GitLab dependencies and are a
recommended upgrade for all installations.

Please read on for more details.

<!-- more -->

- **CE/EE:** Upgrade Doorkeeper to 4.2.0. ([!5881])
- **CE/EE:** Upgrade Hamlit to 2.6.1. ([!5873])

[!5873]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5873
[!5881]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5881

## Upgrade Doorkeeper to 4.2.0

Doorkeeper 4.2.0 was recently released to address
[CVE-2016-6582](http://seclists.org/oss-sec/2016/q3/332) and we've updated the
gem accordingly.

## Upgrade Hamlit to 2.6.1

The Hamlit library was vulnerable to the same [CVE-2016-6316][cve] issue that
recently prompted an update for Rails. See [the issue][21017] for more details.

GitLab versions prior to 8.10 are not using Hamlit and do not require this
fix.

We'd like to thank [Dylan Katz](https://dylankatz.com/) for responsibly
disclosing this issue to us, and to Hamlit author [Takashi Kokubun][k0kubun] for
quickly releasing a fix after we traced the cause back to the gem.

[cve]: https://groups.google.com/d/msg/ruby-security-ann/8B2iV2tPRSE/JkjCJkSoCgAJ
[21017]: https://gitlab.com/gitlab-org/gitlab-ce/issues/21017
[k0kubun]: https://github.com/k0kubun

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
