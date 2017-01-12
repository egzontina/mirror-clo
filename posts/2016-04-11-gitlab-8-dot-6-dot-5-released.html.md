---
title: "GitLab 8.6.5 Released"
date: 2016-04-11 17:00
author: GitLab
author_twitter: gitlab
---

Today we are releasing version 8.6.5 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version includes an important security fix for Two-factor Authentication,
fixes for project importing, and a performance improvement in Git post-receive
handling.

Read on for all the details!

<!-- more -->

- **EE:** Allow OAuth SSL verification to be disabled when importing from GitHub
  ([!323])
- **CE/EE:** Prevent Two-factor Authentication spoofing
- **CE/EE:** Fix for importing projects from GitHub Enterprise ([!3529])
- **CE/EE:** Update project language after doing all other operations ([!3533])
- **CE/EE:** Check permissions when importing project members ([!3535])
- **CE/EE:** Unblocks user when active_directory is disabled and it can be found
  ([!3550])
- **CE/EE:** Only update main language if it is not already set ([!3556])
- **CE/EE:** Return status code 303 after a branch DELETE operation to avoid
  project deletion ([!3583])

[!323]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/323
[!3529]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3529
[!3533]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3533
[!3535]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3535
[!3550]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3550
[!3556]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3556
[!3583]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3583

## Two-factor Authentication spoofing

[Jobert Abma](https://twitter.com/jobertabma) of [HackerOne](https://hackerone.com/jobert)
alerted us to a [security vulnerability] related to the two-factor authentication
(2FA) method used in GitLab CE and EE.

It was possible for an attacker to bypass password authentication of users that
have 2FA enabled, and consequently sign in as a different user without knowing
their password, if he could guess the user's current six-digit 2FA validation
code.

It was also possible to enumerate users and check if they have 2FA enabled,
because GitLab responded with a different error for each case.

We've also [released new packages for 8.5, 8.4, and 8.3][backports] to include this
important fix.

[security vulnerability]: https://gitlab.com/gitlab-org/gitlab-ce/issues/14900
[backports]: /2016/04/11/gitlab-8-dot-5-dot-10-released/

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

Access to GitLab Enterprise Edition is included with a [subscription](https://about.gitlab.com/pricing/).
No time to upgrade GitLab yourself? Subscribers receive upgrade and installation
services
