---
title: "GitLab 8.6.1 Released"
date: 2016-03-23 15:00
author: GitLab
author_twitter: gitlab
---

Today we are releasing version 8.6.1 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version includes many fixes and improvements.

Read on for all the details!

<!-- more -->

- **EE:** Only rename the `light_logo` column in the `appearances` table if it is not there yet. ([!290])
- **EE:** Fix diffs in text part of email-on-push messages. ([!293])
- **EE:** Fix an issue with methods not accessible in some controllers. ([!295])
- **EE:** Ensure `Projects::ApproversController` inherits from `Projects::ApplicationController`. ([!296])
- **CE/EE:** Add option to reload the schema before restoring a database backup. ([!2807])
- **CE/EE:** Display navigation controls on mobile. ([!3214])
- **CE/EE:** Fix a bug where participants would not work correctly on merge requests. ([!3329])
- **CE/EE:** Fix sorting issues by votes on the groups issues page results in SQL errors. ([!3333])
- **CE/EE:** Restrict notifications for confidential issues. ([!3334])
- **CE/EE:** Do not allow to move issue if it has not been persisted. ([!3340])
- **CE/EE:** Add a confirmation step before deleting an issuable. ([!3341])
- **CE/EE:** Fix an issue with the sign-in button overflowing on mobile. ([!3342])
- **CE/EE:** Auto-collapses the navigation sidebar when resizing. ([!3343])
- **CE/EE:** Fix build dependencies, when the dependency is a string. ([!3344])
- **CE/EE:** Show error messages when trying to create a label in dropdown menu. ([!3345])
- **CE/EE:** Fix an issue with assign milestone not loading milestone list. ([!3346])
- **CE/EE:** Fix an issue causing the Dashboard > Milestones page to be blank. ([!3348])
- **Omnibus GitLab:** Fix artifacts path key in `gitlab.yml.erb` ([!694])

[!290]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/290
[!293]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/293
[!295]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/295
[!296]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/296

[!2807]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2807
[!3214]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3214
[!3329]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3329
[!3333]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3333
[!3334]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3334
[!3340]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3340
[!3341]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3341
[!3342]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3342
[!3343]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3343
[!3344]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3344
[!3345]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3345
[!3346]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3346
[!3348]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3348

[!694]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/694

## Upgrade barometer

This version does not include any new migrations, and should not require
any downtime.

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
services.
