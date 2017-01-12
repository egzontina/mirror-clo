---
title: "GitLab 8.9.1 released"
author: Robert Speicher
author_twitter: rspeicher
categories: release
---

Today we are releasing version 8.9.1 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This version resolves a number of regressions and bugs in the [recent 8.9
release](/2016/06/22/gitlab-8-9-released/).

Please read on for more details.

<!-- more -->

- **EE:** Improve Geo documentation. ([!431])
- **EE:** Fix remote mirror stuck on started issue. ([!491])
- **EE:** Fix MR creation from forks where target project has approvals enabled. ([!496])
- **EE:** Fix MR edit where target project has approvals enabled. ([!496])
- **EE:** Fix vertical alignment of git-hooks page. ([!499])
- **CE/EE:** Refactor labels documentation. ([!3347])
- **CE/EE:** Eager load award emoji on notes. ([!4628])
- **CE/EE:** Fix some CI wording in documentation. ([!4660])
- **CE/EE:** Document `GIT_STRATEGY` and `GIT_DEPTH`. ([!4720])
- **CE/EE:** Add documentation for the export & import features. ([!4732])
- **CE/EE:** Add some docs for Docker Registry configuration. ([!4738])
- **CE/EE:** Ensure we don't send the "access request declined" email to access requesters on project deletion. ([!4744])
- **CE/EE:** Display group/project access requesters separately in the admin area. ([!4798])
- **CE/EE:** Add documentation and examples for configuring cloud storage for registry images. ([!4812])
- **CE/EE:** Clarifies documentation about artifact expiry. ([!4831])
- **CE/EE:** Fix the Network graph links. ([!4832])
- **CE/EE:** Fix MR-auto-close text added to description. ([!4836])
- **CE/EE:** Add documentation for award emoji now that comments can be awarded with emojis. ([!4839])
- **CE/EE:** Fix typo in export failure email. ([!4847])
- **CE/EE:** Fix header vertical centering. ([!4170])
- **CE/EE:** Fix subsequent SAML sign ins. ([!4718])
- **CE/EE:** Set button label when picking an option from status dropdown. ([!4771])
- **CE/EE:** Prevent invalid URLs from raising exceptions in WikiLink Filter. ([!4775])
- **CE/EE:** Handle external issues in IssueReferenceFilter. ([!4789])
- **CE/EE:** Support for rendering/redacting multiple documents. ([!4828])
- **CE/EE:** Update Todos documentation and screenshots to include new functionality. ([!4840])
- **CE/EE:** Hide nav arrows by default. ([!4843])
- **CE/EE:** Added bottom padding to label color suggestion link. ([!4845])
- **CE/EE:** Use jQuery objects in ref dropdown. ([!4850])
- **CE/EE:** Fix GitLab project import issues related to notes and builds. ([!4855])
- **CE/EE:** Restrict header logo to 36px so it doesn't overflow. ([!4861])
- **CE/EE:** Fix unwanted label unassignment. ([!4863])
- **CE/EE:** Fix mobile Safari bug where horizontal nav arrows would flicker on scroll. ([!4869])
- **CE/EE:** Restore old behavior around diff notes to outdated discussions. ([!4870])
- **CE/EE:** Fix merge requests project settings help link anchor. ([!4873])
- **CE/EE:** Fix 404 when accessing pipelines as guest user on public projects. ([!4881])
- **CE/EE:** Remove width restriction for logo on sign-in page. ([!4888])
- **CE/EE:** Bump gitlab_git to 10.2.3 to fix false truncated warnings with ISO-8559 files. ([!4884])
- **CE/EE:** Apply selected value as label. ([!4886])
- **CE/EE:** Fix temp file being deleted after the request while importing a GitLab project. ([!4894])
- **CE/EE:** Fix user creation with stronger minimum password requirements. ([!4054]) (nathan-pmt)
- **CE/EE:** Fix a wrong MR status when merge_when_build_succeeds & project.only_allow_merge_if_build_succeeds are true. ([!4912])
- **CE/EE:** Add SMTP as default delivery method to match gitlab-org/omnibus-gitlab!826. ([!4915])

[!431]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/431
[!491]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/491
[!496]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/496
[!496]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/496
[!499]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/499
[!3347]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/3347
[!4628]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4628
[!4660]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4660
[!4720]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4720
[!4732]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4732
[!4738]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4738
[!4744]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4744
[!4798]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4798
[!4812]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4812
[!4831]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4831
[!4832]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4832
[!4836]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4836
[!4839]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4839
[!4847]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4847
[!4170]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4170
[!4718]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4718
[!4771]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4771
[!4775]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4775
[!4789]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4789
[!4828]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4828
[!4840]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4840
[!4843]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4843
[!4845]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4845
[!4850]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4850
[!4855]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4855
[!4861]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4861
[!4863]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4863
[!4869]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4869
[!4870]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4870
[!4873]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4873
[!4881]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4881
[!4888]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4888
[!4884]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4884
[!4886]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4886
[!4894]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4894
[!4054]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4054
[!4912]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4912
[!4915]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4915

## Upgrade barometer

This version does not include any migrations, and should not require any
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
