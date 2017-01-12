---
title: "GitLab 8.10.2 released"
author: Rémy Coutable
author_twitter: rymai
categories: release
---

Today we are releasing version 8.10.2 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version resolves a number of regressions and bugs in the [recent 8.10
release](/2016/07/22/gitlab-8-10-released/).

Please read on for more details.

<!-- more -->

- **EE:** Fix pagination on search result page when ES search is enabled. ([!592])
- **EE:** Decouple an ES index update from `RepositoryUpdateMirrorWorker`. ([!593])
- **EE:** Fix broken `user_allowed?` check in Git Annex push. ([!597])
- **CE/EE:** User can now search branches by name. ([!5144])
- **CE/EE:** Page is now properly rendered after committing the first file and creating the first branch. ([!5399])
- **CE/EE:** Add branch or tag icon to ref in builds page. ([!5434])
- **CE/EE:** Fix backup restore. ([!5459])
- **CE/EE:** Use project ID in repository cache to prevent stale data from persisting across projects. ([!5460])
- **CE/EE:** Fix issue with autocomplete search not working with enter key. ([!5466])
- **CE/EE:** Add iid to MR API response. ([!5468])
- **CE/EE:** Disable MySQL foreign key checks before dropping all tables. ([!5472])
- **CE/EE:** Ensure relative paths for video are rewritten as we do for images. ([!5474])
- **CE/EE:** Ensure current user can retry a build before showing the 'Retry' button. ([!5476])
- **CE/EE:** Add ENV variable to skip repository storages validations. ([!5478])
- **CE/EE:** Added `*.js.es6 gitlab-language=javascript` to `.gitattributes`. ([!5486])
- **CE/EE:** Don't show comment button in gutter of diffs on MR discussion tab. ([!5493])
- **CE/EE:** Rescue Rugged::OSError (lock exists) when creating references. ([!5497])
- **CE/EE:** Fix expand all diffs button in compare view. ([!5500])
- **CE/EE:** Show release notes in tags list. ([!5503])
- **CE/EE:** Fix a bug where forking a project from a repository storage to another would fail. ([!5509])
- **CE/EE:** Fix missing schema update for `20160722221922`. ([!5512])
- **CE/EE:** Update `gitlab-shell` version to 3.2.1 in the 8.9->8.10 update guide. ([!5516])
- **Omnibus GitLab:** Exclude standard ports from Host header. ([!891])

[!592]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/592
[!593]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/593
[!597]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/597

[!5144]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5144
[!5399]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5399
[!5434]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5434
[!5459]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5459
[!5460]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5460
[!5466]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5466
[!5468]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5468
[!5472]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5472
[!5474]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5474
[!5476]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5476
[!5478]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5478
[!5486]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5486
[!5493]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5493
[!5497]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5497
[!5500]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5500
[!5503]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5503
[!5509]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5509
[!5512]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5512
[!5516]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5516

[!891]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/891

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
