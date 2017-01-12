---
title: "GitLab 8.12.5, 8.11.9, and 8.10.12 released"
author: Rémy Coutable
author_twitter: rymai
categories: release
date: 2016-10-11 18:20
---

Today we are releasing versions 8.12.5, 8.11.9, and 8.10.12 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

Version 8.12.5 contains two security fixes for GitLab, plus fixes for minor
regressions. Versions 8.11.9 and 8.10.12 only contain the security fixes.

Please read on for more details.

<!-- more -->

- **CE/EE:** Switch from request to env in ::API::Helpers. ([!6615])
- **CE/EE:** Update the mail_room gem to 0.8.1 to fix a race condition with the mailbox watching thread. ([!6714])
- **CE/EE:** Improve issue load time performance by avoiding ORDER BY in find_by call. ([!6724])
- **CE/EE:** Add a new gitlab:users:clear_all_authentication_tokens task. ([!6745])
- **CE/EE:** Don't send Private-Token (API authentication) headers to Sentry
- **CE/EE:** Share projects via the API only with groups the authenticated user can access

- **Omnibus GitLab** Update the storage directory helper to check permissions for symlink targets. ([!1028])

[!6615]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6615
[!6714]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6714
[!6724]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6724
[!6745]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6745

[!1028]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/1028


## Private tokens sent to Sentry

_This vulnerability only affects GitLab instances that use Sentry exception
tracking. This feature is off by default in GitLab._

As a GitLab administrator you have the option to integrate your GitLab instance
with Sentry, an external exception tracking system. When this feature is
enabled, you can see details of each error ('500 page') that occurs on your
GitLab server. These details include HTTP headers of the request that
experienced the exception. Prior to GitLab 8.12.5, when an exception occured in
the GitLab API (a URL starting with `/api/v3/`), GitLab would inadvertently send
the `Private-Token` header used to authenticate with the GitLab API in the error
report to Sentry. This meant that when you viewed a Sentry error report for an
exception that occurred during a GitLab API request you could see the Private
token of the user that performed the request. This also meant that if there is a
data breach at your Sentry server, GitLab user private tokens may be exposed.

The holder of the private token for a GitLab user can impersonate that user in
GitLab via the API. That includes writing comments, adding SSH keys, creating
repositories. The holder of the private token of a GitLab administrator is able
to do much more, for instance creating new user accounts. See [#22537] for more
information.

### Mitigation

Even though private tokens are not sent to Sentry starting with GitLab 8.12.5,
the tokens are valid forever as long as they are in the GitLab database.

That's why we **strongly** advise you to invalidate all your users' Private
tokens with [the following Rake task]:

```
# omnibus-gitlab
sudo gitlab-rake gitlab:users:clear_all_authentication_tokens

# installation from source
bundle exec rake gitlab:users:clear_all_authentication_tokens RAILS_ENV=production
```

New tokens will automatically be issued once users sign-in.

As a less secure alternative (or as an additional precaution), you can also
[clear the exception history for your GitLab instance in Sentry].

Note: At any time, individual GitLab users can reset their private token on
their `Account` page (`/profile/account`).

[the following Rake task]: https://docs.gitlab.com/ce/raketasks/user_management.html#clear-authentication-tokens-for-all-users.-important-data-loss
[clear the exception history for your GitLab instance in Sentry]: https://docs.sentry.io/learn/sensitive-data/#removing-data
[#22537]: https://gitlab.com/gitlab-org/gitlab-ce/issues/22537

## Information disclosure via the "Share project with group" API endpoint

The new implementation of the "Share project with group" API endpoint allowed
projects to be shared with groups that the current user wasn't allowed to see,
leaking the group name and the name of its owners. See [#23004] for more
information.

[#23004]: https://gitlab.com/gitlab-org/gitlab-ce/issues/23004

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
