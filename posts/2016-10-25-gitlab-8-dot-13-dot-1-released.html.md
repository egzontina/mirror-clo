---
title: "GitLab 8.13.1 released"
author: Rémy Coutable
author_twitter: rymai
categories: release
---

Today we are releasing version 8.13.1 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version resolves a number of regressions and bugs in the [recent 8.13
release](/2016/10/22/gitlab-8-13-released).

Please read on for more details.

<!-- more -->

- **CE/EE:** Fix branch protection API. ([!6215])
- **CE/EE:** Fix hidden pipeline graph on commit and MR page. ([!6895])
- **CE/EE:** Fix Cycle analytics not showing correct data when filtering by date. ([!6906])
- **CE/EE:** Ensure custom provider tab labels don't break layout. ([!6993])
- **CE/EE:** Fix issue boards user link when in subdirectory. ([!7018])
- **CE/EE:** Refactor and add new environment functionality to CI yaml reference. ([!7026])
- **CE/EE:** Fix typo in project settings that prevents users from enabling container registry. ([!7037])
- **CE/EE:** Fix events order in `users/:id/events` endpoint. ([!7039])
- **CE/EE:** Remove extra line for empty issue description. ([!7045])
- **CE/EE:** Don't append issue/MR templates to any existing text. ([!7050])
- **CE/EE:** Fix error in generating labels. ([!7055])
- **CE/EE:** Stop clearing the database cache on `rake cache:clear`. ([!7056])
- **CE/EE:** Only show register tab if signup enabled. ([!7058])
- **CE/EE:** Expire and build repository cache after project import. ([!7064])
- **CE/EE:** Fix bug where labels would be assigned to issues that were moved. ([!7065])
- **CE/EE:** Fix reply-by-email not working due to queue name mismatch. ([!7068])
- **CE/EE:** Fix 404 for group pages when GitLab setup uses relative url. ([!7071])
- **CE/EE:** Fix `User#to_reference`. ([!7088])
- **CE/EE:** Reduce overhead of `LabelFinder` by avoiding `#presence` call. ([!7094])
- **CE/EE:** Fix unauthorized users dragging on issue boards. ([!7096])
- **CE/EE:** Only schedule `ProjectCacheWorker` jobs when needed. ([!7099])

- **EE:** Hide multiple board actions if user doesnt have permissions. ([!816])
- **EE:** Fix Elasticsearch::Transport::Transport::Errors::BadRequest when ES is enabled. ([!818])

- **Omnibus GitLab:** Update docs for nginx status, fix the default server for status config. ([!1052])

[!6215]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6215
[!6895]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6895
[!6906]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6906
[!6993]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6993
[!7018]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7018
[!7026]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7026
[!7037]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7037
[!7039]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7039
[!7045]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7045
[!7050]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7050
[!7055]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7055
[!7056]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7056
[!7058]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7058
[!7064]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7064
[!7065]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7065
[!7068]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7068
[!7071]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7071
[!7088]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7088
[!7094]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7094
[!7096]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7096
[!7099]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7099

[!816]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/816
[!818]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/818

[!1052]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/1052

## Upgrade barometer

This version has one migration that requires a few minutes of downtime if mailroom
is used for reply-by-email. You can stop mailroom before installing this update if
you want to avoid downtime.

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
