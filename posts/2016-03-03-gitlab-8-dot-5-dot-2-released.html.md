---
title: "GitLab 8.5.2 Released"
date: 2016-03-03 11:00
author: GitLab
author_twitter: gitlab
filename: 2016-03-03-gitlab-8-dot-5-dot-2-released.markdown
---

Today we are releasing version 8.5.2 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version includes many fixes for the Issues sidebar, Todos, Labels, relative URL
installations, and forks list. It also ports a feature from GitLab Enterprise
Edition to GitLab Community Edition, adds documentation for the Todos feature
and updates the required Rails and OpenSSL versions.

Read on for all the details!

<!-- more -->

- **EE:** Update LDAP groups asynchronously ([!221])
- **EE:** Fix an issue when weight text was displayed in Issuable collapsed sidebar ([!222])
- **CE/EE:** Fix sidebar overlapping content when screen width was below 1200px ([!2620])
- **CE/EE:** Don't repeat labels listed on Labels tab ([!2924])
- **CE/EE:** Bring the "branded appearance" feature from EE to CE ([!2927])
- **CE/EE:** Fix error 500 when commenting on a commit ([!2964])
- **CE/EE:** Show days remaining instead of elapsed time for Milestone ([!2978])
- **CE/EE:** Fix broken icons on installations with relative URL ([!2979])
- **CE/EE:** Fix issue where tag list wasn't refreshed after deleting a tag ([!2986])
- **CE/EE:** Fix import from gitlab.com ([!2988])
- **CE/EE:** Improve implementation to check read access to forks and add pagination ([!2991])
- **CE/EE:** Don't show any "2FA required" message if it's not actually required ([!3014])
- **CE/EE:** Fix help keyboard shortcut on relative URL setups ([!3016])
- **CE/EE:** Update Rails to 4.2.5.2 ([!3020])
- **CE/EE:** Fix permissions for deprecated CI build status badge ([!3030])
- **CE/EE:** Don't show "Welcome to GitLab" when the search didn't return any projects ([!3059])
- **CE/EE:** Add Todos documentation ([!3064])
- **Omnibus GitLab:** Fix regression where NGINX config for standalone ci was not created ([!659])
- **Omnibus GitLab:** Execute package preinst when starting Docker image ([!663])
- **Omnibus GitLab:** Update openssl to 1.0.2g ([!665])
- **Omnibus GitLab:** Add Redis server password support ([!668])

[!221]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/221
[!222]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/222

[!2620]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2620
[!2924]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2924
[!2927]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2927
[!2964]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2964
[!2978]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2978
[!2979]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2979
[!2986]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2986
[!2988]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2988
[!2991]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2991
[!3014]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3014
[!3016]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3016
[!3020]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3020
[!3030]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3030
[!3059]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3059
[!3064]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3064

[!659]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/659
[!663]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/663
[!665]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/665
[!668]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/668

## Branded login page is now part of GitLab Community Edition

This patch release [ports the branded login page feature][!2927] from
[GitLab Enterprise Edition](https://about.gitlab.com/features/#enterprise) to
[GitLab Community Edition](https://about.gitlab.com/features/#community).

## Rails security update

As soon as [Rails 4.2.5.2 was announced][rails-4.2.5.2], we reviewed the two CVEs
it addresses. However, we are confident in the fact that **GitLab is not
affected** by these vulnerabilities.

That being said, we are [upgrading to Rails 4.2.5.2][!3020] in GitLab 8.5.2 regardless of
that fact.

[rails-4.2.5.2]: http://weblog.rubyonrails.org/2016/2/29/Rails-4-2-5-2-4-1-14-2-3-2-22-2-have-been-released/

## OpenSSL security update

As soon as [OpenSSL Security Advisory was announced][openssl-security-advisory],
we reviewed it. However, we are confident in the fact that **GitLab is not
affected** by these vulnerabilities since [we are not using SSLv2 anywhere].

That being said, we are [upgrading to OpenSSL 1.0.2g][!665] in GitLab 8.5.2
regardless of that fact.

[openssl-security-advisory]: https://mta.openssl.org/pipermail/openssl-announce/2016-March/000066.html
[we are not using SSLv2 anywhere]: https://gitlab.com/gitlab-org/omnibus-gitlab/issues/1154#note_4031640

## Upgrade barometer

This release includes one minor database migration which can be run without
causing any downtime.

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
