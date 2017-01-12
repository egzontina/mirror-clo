---
title: "GitLab 8.9.5 released"
author: Robert Speicher
author_twitter: rspeicher
categories: release
---

Today we are releasing version 8.9.5 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

Please read on for more details.

<!-- more -->

- **EE:** Fix of quoted text in lock tooltip. ([!518])
- **CE/EE:** Add more debug info to import/export and memory killer. ([!5108])
- **CE/EE:** Fixed avatar alignment in new MR view. ([!5095])
- **CE/EE:** Fix diff comments not showing up in activity feed. ([!5069])
- **CE/EE:** Add index on both Award Emoji user and name. ([!5061])
- **CE/EE:** Downgrade to Redis 3.2.2 due to massive memory leak with Sidekiq. ([!5056])
- **CE/EE:** Re-enable import button when import process fails due to namespace already being taken. ([!5053])
- **CE/EE:** Fix snippets comments not being displayed. ([!5045])
- **CE/EE:** Fix emoji paths in relative root configurations. ([!5027])
- **CE/EE:** Fix issues importing events in Import/Export. ([!4987])
- **CE/EE:** Fixed 'use shortcuts' button on docs. ([!4979])
- **CE/EE:** Admin should be able to turn shared runners into specific ones. ([!4961])
- **CE/EE:** Update RedCloth to 4.3.2 for CVE-2012-6684. ([!4929])
- **CE/EE:** Improve the request / withdraw access button. ([!4860])

[!518]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/518
[!5108]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5108
[!5095]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5095
[!5086]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5086
[!5069]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5069
[!5061]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5061
[!5056]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5056
[!5053]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5053
[!5045]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5045
[!5028]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5028
[!5027]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5027
[!4987]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4987
[!4979]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4979
[!4961]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4961
[!4929]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4929
[!4860]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4860

## Upgrade barometer

This version has one migration, but should not require any downtime.

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
