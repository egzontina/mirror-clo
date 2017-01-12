---
title: "GitLab 8.14.2 released"
author: Alejandro Rodríguez
author_twitter: eReGeBe
categories: release
---

Today we are releasing version 8.14.2 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version resolves a number of regressions and bugs in the [recent 8.14
release](/2016/11/22/gitlab-8-14-released).

Please read on for more details.

<!-- more -->

- **CE/EE:** Rephrase some system notes to be compatible with new system note style ([!7692])
- **CE/EE:** Create tag after running pre-hooks and pass updated SHA to post-hooks ([!7700])
- **CE/EE:** Fixed commit time not rendering after initial page load ([!7704])
- **CE/EE:** Prevent error when submitting a merge request and pipeline is not defined ([!7707])
- **CE/EE:** Fix: Timeout creating and viewing merge request for binary file ([!7713])
- **CE/EE:** New system note design for commit discussion ([!7721])
- **CE/EE:** Refresh project authorizations using a Redis lease ([!7733])
- **CE/EE:** Fixed issue boards issue sorting when dragging issue into list ([!7734])
- **CE/EE:** Fix for builds with no start date throwing an error in cycle analytics events ([!7738])
- **CE/EE:** Clean up JiraService ([!7756])
- **CE/EE:** Update GitLab Workhorse to v1.0.1 ([!7759])
- **CE/EE:** Fix pipelines info being hidden in merge request widget ([!7808])
- **CE/EE:** Update Sidekiq-cron to fix compatibility issues with Sidekiq 4.2.1 ([!7815])
- **CE/EE:** Fix a transient spec failure ([!7825])
- **CE/EE:** Fixes access to the wiki code with git when repository feature disabled ([!7832])
- **CE/EE:** Revert bump in rufus-scheduler ([!7844])
- **CE/EE:** Make deleting with optimistic locking respect NULL ([!7867])
- **CE/EE:** Remove caching of events data ([!6578])
- **CE/EE:** Fix broken external links in help/index.html ([!7582])
- **CE/EE:** Evalute time_ago method instead of printing it ([!7634])
- **CE/EE:** Resolves updated and resolved status is not showing ([!7655])
- **CE/EE:** Fixed resolved discussion timeago not rendering ([!7656])
- **CE/EE:** Pick valid event objects for the events list ([!7689])


- **EE:** Port of rephrase-system-notes to EE ([!913])
- **EE:** Get rid of user activites table and replace it with redis ([!915])
- **EE:** Geo: Display Custom Avatars in secondary nodes ([!904])


- **Omnibus GitLab:** Revert default IPv6 configuration for NGINX ([!1133])

[!913]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/913
[!915]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/915
[!904]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/904
[!1133]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/1133
[!7692]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7692
[!7700]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7700
[!7704]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7704
[!7707]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7707
[!7713]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7713
[!7721]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7721
[!7733]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7733
[!7734]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7734
[!7738]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7738
[!7756]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7756
[!7759]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7759
[!7808]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7808
[!7815]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7815
[!7825]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7825
[!7832]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7832
[!7844]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7844
[!7867]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7867
[!6578]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6578
[!7582]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7582
[!7634]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7634
[!7655]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7655
[!7656]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7656
[!7689]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7689

## Upgrade barometer

This version has no migrations and should not require any downtime.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

## Updating

To update, check out our [update page](https://about.gitlab.com/update/).

## Enterprise Edition

Interested in GitLab Enterprise Edition? Check out the [features exclusive to
EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](https://about.gitlab.com/pricing/).
No time to upgrade GitLab yourself? Subscribers receive upgrade and installation
services.
