---
title: "GitLab 8.8.2 released"
author: GitLab
author_twitter: gitlab
---

Today we are releasing version 8.8.2 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

It includes the following fixes:

- **EE:** [Elastic] Search through the filenames. ([!409])
- **EE:** Fix repository mirror updates for new imports stuck in "started" state. ([!416])
- **CE/EE:** Added remove due date button. ([!4209])
- **CE/EE:** Fix Error 500 when accessing application settings due to nil disabled OAuth sign-in sources. ([!4242])
- **CE/EE:** Fix Error 500 in CI charts by gracefully handling commits with no durations. ([!4245])
- **CE/EE:** Fix table UI on CI builds page. ([!4249])
- **CE/EE:** Fix backups if Docker Registry is disabled. ([!4263])
- **CE/EE:** Fixed issue with "Merge Immediately" button color. ([!4211])
- **CE/EE:** Fixed issue with Enter key selecting wrong option in dropdown. ([!4210])
- **CE/EE:** When creating a .gitignore file a dropdown with templates will be provided. ([!4075])
- **CE/EE:** Fix concurrent request when updating build log in browser. ([!4183])

[!409]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/409
[!416]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/416
[!4209]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4209
[!4242]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4242
[!4245]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4245
[!4249]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4249
[!4263]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4263
[!4211]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4211
[!4210]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4210
[!4075]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4075
[!4183]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4183

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

Access to GitLab Enterprise Edition is included with a [subscription](https://about.gitlab.com/subscription).
No time to upgrade GitLab yourself? Subscribers receive upgrade and installation
services.
