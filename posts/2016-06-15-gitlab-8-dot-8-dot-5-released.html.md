---
title: "GitLab 8.8.5 released"
author: Stan Hu
author_twitter: stanhu
---

Today we are releasing the versions 8.8.5, 8.7.7, 8.6.9, 8.5.13, 8.4.11,
8.3.10 and 8.2.6 for GitLab Community Edition (CE) and Enterprise Edition
(EE).

These versions contain a number of security fixes, and we recommend that all
GitLab installations be upgraded to one of these versions.

Please read on for more details.

<!-- more -->

8.8.5 includes the following fixes:

- **CE/EE:** Import GitHub repositories respecting the API rate limit ([!4166])
- **CE/EE:** Fix todos page throwing errors when you have a project pending deletion ([!4300])
- **CE/EE:** Disable Webhooks before proceeding with the GitHub import ([!4470])
- **CE/EE:** Fix importer for GitHub comments on diff ([!4488])
- **CE/EE:** Adjust the SAML control flow to allow LDAP identities to be added to an existing SAML user ([!4498])
- **CE/EE:** Fix incremental trace upload API when using multi-byte UTF-8 chars in trace ([!4541])

[!4166]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4166
[!4300]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4300
[!4470]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4470
[!4488]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4488
[!4498]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4498
[!4541]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4541

In addition, 8.8.5, 8.7.7, 8.6.9, 8.5.13, 8.4.11, 8.3.10 and 8.2.6 include the following
security fixes:

## Unauthorized access to project build traces

It was possible for users to view build traces, possibly exposing sensitive
information to other users. See [the issue][18188] for more details.

[18188]: https://gitlab.com/gitlab-org/gitlab-ce/issues/18188

Thanks to Madhu Akula for responsibly disclosing this issue to us.

## Cross-site scripting (XSS) vulnerability in Wiki pages

It was possible for an attacker to inject malicious JavaScript code in a
Wiki page. See [the issue][17298] for more details

Thanks to [Jobert Abma][jobert-twitter] of [HackerOne][jobert] for
responsibly disclosing this issue to us.

[17298]: https://gitlab.com/gitlab-org/gitlab-ce/issues/17298
[jobert-twitter]: https://twitter.com/jobertabma
[jobert]: https://hackerone.com/jobert

## Unauthorized access to notes in confidential issues

Notes in confidential issues could be viewed in JSON form by unauthorized users.
See [the issue][18535] for more details.

[18535]: https://gitlab.com/gitlab-org/gitlab-ce/issues/18535

## Upgrade barometer

This version does not include any migrations, and should not require any
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

Access to GitLab Enterprise Edition is included with a [subscription](https://about.gitlab.com/subscription).
No time to upgrade GitLab yourself? Subscribers receive upgrade and installation
services.
