---
title: "GitLab 8.2.3 Released"
date: 2015-12-10
author: GitLab
author_twitter: gitlab
---

Today we are releasing version 8.2.3 for Community Edition (CE) and Enterprise
Edition (EE).

It includes the following fixes:

- **CE/EE:** Fix application settings cache not expiring after changes
  ([#1972]).
- **CE/EE:** Prevent 500 error when creating global milestones with Unicode
  characters ([#1983]).
- **CE/EE:** Update documentation for "Guest" permissions ([#1952]).
- **CE/EE:** Properly convert Emoji-only comments into Award Emojis ([#1936]).
- **CE/EE:** Webhook payload has an added, modified and removed properties for
  each commit ([#1988]).
- **CE/EE:** Prevent 500 error when creating a merge request that removes a
  submodule ([#1989]).
- **CE/EE:** Enable "paranoid mode" for Devise logins to prevent user
  enumeration ([#2044]).
- **CE/EE:** Prevent a possible remote code execution (RCE) in `.gitlab-ci.yml`
  parsing (see below for more details).

[#1936]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/1936
[#1952]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/1952
[#1972]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/1972
[#1983]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/1983
[#1988]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/1988
[#1989]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/1989
[#2044]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2044

<!-- more -->

## Remote code execution prevention

We found a vulnerability in GitLab where arbitrary Ruby objects could be
instantiated with arbitrary data, because of an unsafe YAML load. This is the
same problem that was found in Rails almost three years ago and was heavily
publicized at that time.

The vulnerability can be turned into remote code execution when an object can be
instantiated that evaluates one of its data attributes as Ruby code. At the time
when the issue was found in Rails, Rails contained a number of classes that
could be abused in this way, making it a RCE vulnerability.

In the version of Rails used in GitLab, these classes no longer meet the
criteria, and we have been unable to find any other classes that do, which is
why we currently consider this low-risk. However, someone with enough
perseverance could likely find another class that can be abused in this way, so
we recommend everyone to upgrade as soon as possible.

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
