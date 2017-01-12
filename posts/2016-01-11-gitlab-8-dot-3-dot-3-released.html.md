---
title: "GitLab 8.3.3 Released"
date: 2016-01-11
author: GitLab
author_twitter: gitlab
filename: 2016-01-11-gitlab-8-dot-3-dot-3-released.markdown
---

_**Warning** (2016-01-12 13:25 UTC)_: Do not upgrade to GitLab 8.3.3 at this time.
GitLab 8.3.3 ships with gitlab-workhorse 0.5.3, which contains an [API routing bug](https://gitlab.com/gitlab-org/gitlab-workhorse/issues/14).
GitLab 8.3.4 [has been released](https://about.gitlab.com/2016/01/12/gitlab-8-dot-3-4-released/)
to correct the issue.

---

Today we are releasing version 8.3.3 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

It includes the following changes:

- **CE/EE:** Preserve CE behavior with JIRA integration by only calling API if
  URL is set ([#2341])
- **CE/EE:** Fix duplicated branch creation/deletion events when using Web UI
  ([#2343])
- **CE/EE:** Add configurable LDAP server query timeout ([#2267])
- **CE/EE:** Get "Merge when build succeeds" to work when commits were pushed to
  MR target branch while builds were running ([#2304])
- **CE/EE:** Suppress e-mails on failed builds if allow_failure is set ([#2178])
- **CE/EE:** Fix project transfer e-mail sending incorrect paths in e-mail
  notification ([#2235])
- **CE/EE:** Enable "Add key" button when user fills in a proper key ([#2208])
- **CE/EE:** Better support for referencing and closing issues in Asana service
  ([#2111])
- **CE/EE:** Fix error in processing reply-by-email messages ([#2288])
- **CE/EE:** Fix Error 500 when visiting build page of project with nil
  `runners_token` ([#2294])
- **CE/EE:** Use WOFF versions of SourceSansPro fonts ([#2357])
- **CE/EE:** Fix regression when builds were not generated for tags created
  through web/api interface ([#2366])
- **CE/EE:** Bump gitlab-workhorse to 0.5.3 ([#2367])
- **EE:** Fix undefined method call in Jenkins integration service ([#106])

[#2111]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2111
[#2136]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2136
[#2178]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2178
[#2208]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2208
[#2224]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2224
[#2235]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2235
[#2267]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2267
[#2283]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2283
[#2288]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2288
[#2294]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2294
[#2304]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2304
[#2341]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2341
[#2343]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2343
[#2357]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2357
[#2359]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2359
[#2366]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2366
[#2367]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2367
[#106]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/106

<!-- more -->

## Upgrade barometer

This version does not include any new migrations, and should not require any
downtime.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

### Update gitlab-workhorse

This version requires gitlab-workhorse version 0.5.3. Omnibus installations will
automatically have the latest version; installations from source should follow
the [update guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/8-3-stable/doc/update/8.2-to-8.3.md#5-update-gitlab-workhorse)
to ensure the required version is used.

### Update Asana Tokens

[Asana API Keys have been deprecated](https://asana.com/developers/feed/api-key-deprecation)
in favor of Personal Access Tokens and OAuth. You can create a personal access
token for GitLab on [the Apps tab of your profile settings](https://app.asana.com/-/account_api).

Once you have a token, you can update all projects via the console:

```ruby
AsanaService.all.each { |s| s.api_key = '[PERSONAL_ACCESS_TOKEN]'; s.save }
```

See [#2111] for more details on this change.

## Updating

To update, check out our [update page](https://about.gitlab.com/update).

## Enterprise Edition

Interested in GitLab Enterprise Edition? Check out the [features exclusive to
EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself? Subscribers receive upgrade and installation
services.
