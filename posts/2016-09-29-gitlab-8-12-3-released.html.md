---
title: "GitLab 8.12.3, 8.11.8, 8.10.11 and 8.9.11 released"
author: Rubén Dávila
author_twitter: rdavila
categories: release
---

Today we are releasing versions 8.12.3, 8.11.8, 8.10.11 and 8.9.11 for GitLab Community
Edition (CE) and Enterprise Edition (EE).

Version 8.12.3 contains some security fixes for GitLab, plus fixes for minor
regressions. Version 8.11.8, 8.10.11, and 8.9.11 only contain the security fixes.

If you're wondering what happened to 8.12.2, good eye! That version was accidentally packaged without including some fixes for the CE version.

Please read on for more details.

<!-- more -->

- **CE/EE:** Enforce the `fork_project` permission in `Projects::CreateService`.
- **CE/EE:** Set a restrictive CORS policy for the API.
- **CE/EE:** API: Disable Rails session auth for non-GET/HEAD requests.
- **CE/EE:** Escape HTML nodes in builds commands in CI linter.
- **CE/EE:** Send ajax request for label update only if they are changed. ([!5071])
- **CE/EE:** Pass the full project path for resolve buttons. ([!6129])
- **CE/EE:** Fix list issues not loading with spaces in filtered values. ([!6258])
- **CE/EE:** Fix LDAP omniauth regression (Closes: #22357). ([!6462])
- **CE/EE:** Fix awards dropdown search text from repeating. ([!6498])
- **CE/EE:** Fix issue with rails reserved keyword type exporting/importing services. ([!6499])
- **CE/EE:** Fix snippets pagination. ([!6500])
- **CE/EE:** Wrap `List-Unsubscribe` link in angle brackets. ([!6511])
- **CE/EE:** Fix the "Commits" section of the cycle analytics summary. ([!6513])
- **CE/EE:** Fix Import/Export milestone and 1to1 models issue. ([!6521])
- **CE/EE:** Bump Gitlab Shell to support low IO priority for storage moves. ([!6525])
- **CE/EE:** Add `v-cloak` to resolve disc button. ([!6528])
- **CE/EE:** Be nice to Docker Clients talking to JWT/auth. ([!6536])
- **CE/EE:** Fix `IssuesController#show` degradation including project on loaded notes. ([!6540])
- **CE/EE:** Fix pipelines table headers. ([!6542])
- **CE/EE:** Do not regenerate the `lfs_token` every time `git-lfs-authenticate` is called. ([!6551])
- **CE/EE:** Change the `v-cloak` attr to hash rocket and string 'true'. ([!6553])
- **CE/EE:** Fix duplicate master entries in the merge request versions dropdown. ([!6567])

- **EE:** ES: Fix internal data exposure. (8.12.2 only)
- **EE:** Add missing URL param to ajax call. ([!760])
- **EE:** Ignore unknown project ID in RepositoryUpdateMirrorWorker. ([!754])
- **EE:** Fix prevent_secrets checkbox on admin view. ([!761])

- **Omnibus GitLab** Update openssl to 1.0.2j to get the latest security fixes. ([!1006])
- **Omnibus GitLab** Update to latest cacerts file. ([!1007])

[!6525]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6525
[!6536]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6536
[!5071]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5071
[!6542]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6542
[!6540]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6540
[!6521]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6521
[!6513]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6513
[!6511]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6511
[!6498]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6498
[!6129]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6129
[!6528]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6528
[!6462]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6462
[!6258]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6258
[!6500]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6500
[!6499]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6499
[!6553]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6553
[!6567]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6567
[!6551]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6551
[!760]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/760
[!754]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/754
[!761]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/761
[!1006]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/1006
[!1007]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/1007

## Information disclosure through Global Code Search

The new Global Code Search feature introduced in [GitLab 8.12.0] was returning titles of projects,
milestones, issues, and merge requests from internal projects to anonymous. See [#1046] for more information.

Thanks to **Christian Bönning** for reporthing this issue.

[GitLab 8.12.0]: https://about.gitlab.com/2016/09/22/gitlab-8-12-released/
[#1046]: https://gitlab.com/gitlab-org/gitlab-ee/issues/1046

## API: Restrictive CORS policy

Previous versions set `Access-Control-Allow-Credentials: true` for all origins in their CORS policy.
Combined with [#18302], this resulted in a JavaScript request spoofing vulnerability. See [#22450] for more information.

[#22450]: https://gitlab.com/gitlab-org/gitlab-ce/issues/22450

## API: CSRF protection

Issue [#18302] also introduced a vulnerability allowing third-party websites to spoof API requests using forms,
which is mitigated in these releases. See [#22435] for more information.

[#18302]: https://gitlab.com/gitlab-org/gitlab-ce/issues/18302
[#22435]: https://gitlab.com/gitlab-org/gitlab-ce/issues/22435

## Wrong permission enforcement in ForkService

A user with the "Guest" role could fork a project, and therefore gain access to the code,
even though this was restricted to the "Reporter" level and above.
See [#18028] for more information.

[#18028]: https://gitlab.com/gitlab-org/gitlab-ce/issues/18028

## Upgrade barometer

This version has no migrations and should not require any downtime.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

## Updating

To update, check out our [update page](https://about.gitlab.com/update/).

## Sign up for security notices

Want to be alerted to new security patches as soon as they're available? Sign up
for our [Security Newsletter](https://about.gitlab.com/contact/).

## Enterprise Edition

Interested in GitLab Enterprise Edition? Check out the [features exclusive to
EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](https://about.gitlab.com/pricing/).
No time to upgrade GitLab yourself? Subscribers receive upgrade and installation
services.
