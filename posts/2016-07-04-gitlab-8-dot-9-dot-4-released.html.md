---
title: "GitLab 8.9.4, 8.8.7, and 8.7.9 released"
author: Robert Speicher
author_twitter: rspeicher
categories: release, security
---

Today we are releasing versions 8.9.4, 8.8.7, and 8.7.9 for GitLab Community
Edition (CE) and Enterprise Edition (EE).

All versions contain two security fixes, and 8.9.4 additionally contains fixes
for another batch of regressions. We recommend that all GitLab installations be
upgraded to one of these versions.

Please read on for more details.

<!-- more -->

- **CE/EE:** Fix privilege escalation issue with OAuth external users.
- **CE/EE:** Ensure references to private repos aren't shown to logged-out users.
- **CE/EE:** Updated breakpoint for sidebar pinning. ([!5019])
- **CE/EE:** Expiry date on pinned nav cookie. ([!5009])
- **CE/EE:** Fix wrong line in changelog. ([!5008])
- **CE/EE:** Handle external issues in IssueReferenceFilter. ([!4988])
- **CE/EE:** Fix restore warning message. ([!4980])
- **CE/EE:** Do not show build retry link when build is active. ([!4967])
- **CE/EE:** Fixed commit avatar alignment. ([!4933])
- **CE/EE:** Fixed URL on label button when filtering. ([!4897])
- **CE/EE:** File Browser navigation fixes. ([!4891])
- **CE/EE:** Resolve "Sub nav isn't showing on file view". ([!4890])
- **CE/EE:** Fixed search field blur not removing focus. ([!4704])
- **EE:** Improve how File Lock feature works with nested items. ([!497])

[!5019]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5019
[!5009]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5009
[!5008]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5008
[!4988]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4988
[!4980]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4980
[!4967]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4967
[!4933]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4933
[!4897]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4897
[!4891]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4891
[!4890]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4890
[!4704]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4704
[!497]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/497

## Information disclosure via references

Certain GitLab Flavored Markdown references could expose the existence of a
private project to logged-out users. See [the issue][18033] for more details.

[18033]: https://gitlab.com/gitlab-org/gitlab-ce/issues/18033

Thanks to Ron Arts for responsibly disclosing this issue to us.

## Privilege escalation for external users via OAuth

If an external user logged in via an OAuth provider that was not in the
`external_providers` configuration setting, they would erroneously be set to
internal. See [the issue][19312] for more details.

[19312]: https://gitlab.com/gitlab-org/gitlab-ce/issues/19312

Thanks to Niels Keurentjes for responsibly disclosing this issue to us.

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
