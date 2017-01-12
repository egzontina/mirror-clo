---
title: "GitLab 8.8.3 released"
author: GitLab
author_twitter: gitlab
---

Today we are releasing version 8.8.3 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

It includes the following fixes:

- **EE:** Add standard web hook headers to Jenkins CI post. ([!374])
- **EE:** Gracefully handle malformed DNs in LDAP group sync. ([!392])
- **EE:** Reduce load on DB for license upgrade check. ([!421])
- **EE:** Make it clear the license overusage message is visible only to admins. ([!423])
- **EE:** Fix Git hook validations for fast-forward merges. ([!427])
- **EE:** [Elastic] In search results, only show notes on confidential issues that the user has access to.
- **CE/EE:** Fix 404 page when viewing TODOs that contain milestones or labels in different projects. ([!4312])
- **CE/EE:** Fixed JS error when trying to remove discussion form. ([!4303])
- **CE/EE:** Fixed issue with button color when no CI enabled. ([!4287])
- **CE/EE:** Fixed potential issue with 2 CI status polling events happening. ([!3869])
- **CE/EE:** Improve design of Pipeline view. ([!4230])
- **CE/EE:** Fix gitlab importer failing to import new projects due to missing credentials. ([!4301])
- **CE/EE:** Fix import URL migration not rescuing with the correct Error. ([!4321])
- **CE/EE:** Fix health check access token changing due to old application settings being used. ([!4332])
- **CE/EE:** Make authentication service for Container Registry to be compatible with Docker versions before 1.11. ([!4363])
- **CE/EE:** Add Application Setting to configure Container Registry token expire delay (default 5 min). ([!4364])
- **CE/EE:** Pass the "Remember me" value to the 2FA token form. ([!4369])
- **CE/EE:** Fix incorrect links on pipeline page when merge request created from fork.  ([!4376])
- **CE/EE:** Use downcased path to container repository as this is expected path by Docker. ([!4420])
- **CE/EE:** Fix wiki project clone address error (chujinjin). ([!4429])
- **CE/EE:** Fix serious performance bug with rendering Markdown with InlineDiffFilter.  ([!4392])
- **CE/EE:** Fix missing number on generated ordered list element. ([!4437])
- **CE/EE:** Prevent disclosure of notes on confidential issues in search results.

[!374]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/374
[!392]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/392
[!421]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/421
[!423]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/423
[!427]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/427
[!3869]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3869
[!4230]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4230
[!4287]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4287
[!4301]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4301
[!4303]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4303
[!4312]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4312
[!4321]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4321
[!4332]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4332
[!4363]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4363
[!4364]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4364
[!4369]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4369
[!4376]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4376
[!4392]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4392
[!4420]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4420
[!4429]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4429
[!4437]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4437

<!-- more -->

## Upgrade barometer

This version includes one new migration, but should not require any downtime.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

#### For elasticsearch users
If you use Elasticsearch please run following command after upgrade:

```
# Omnibus installations
sudo gitlab-rake gitlab:elastic:reindex_model MODEL=Note

# Installations from source
bundle exec rake gitlab:elastic:reindex_model MODEL=Note RAILS_ENV=production
```

## Updating

To update, check out our [update page](https://about.gitlab.com/update).

## Enterprise Edition

Interested in GitLab Enterprise Edition? Check out the [features exclusive to
EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](https://about.gitlab.com/subscription).
No time to upgrade GitLab yourself? Subscribers receive upgrade and installation
services.
