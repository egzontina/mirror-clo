---
title: "GitLab 8.11.4 and 8.10.8 released"
author: Rubén Dávila
author_twitter: rdavila
categories: release, security
---

Today we are releasing versions 8.11.4 and 8.10.8 for GitLab Community
Edition (CE) and Enterprise Edition (EE).

Version 8.11.4 contains two security fixes for GitLab, plus fixes for minor
regressions.

Please read on for more details.

<!-- more -->

- **CE/EE:** Fix information disclosure in issue boards.
- **CE/EE:** Fix privilege escalation in project import.
- **CE/EE:** Remove ugly horizontal scrollbars in windows. ([!5942])
- **CE/EE:** Check for pipelines when setting page_gutter_class. ([!5952])
- **CE/EE:** Add body as data-container on pipeline graph tooltip. ([!5955])
- **CE/EE:** Remove gitorious. ([!5866])
- **CE/EE:** Removes leading space from hover state in graph links. ([!5980])
- **CE/EE:** Remove max height on pipelines graph. ([!5988])
- **CE/EE:** Fixed issue where filtering one dropdown will filter another on the page. ([!5985])
- **CE/EE:** Ensure we update dropdown label after input has been added. ([!5999])
- **CE/EE:** GitHub importer use default project visibility for non-private projects. ([!6023])
- **CE/EE:** Fix diff comments on legacy MRs. ([!6029])
- **CE/EE:** Curved lines at top of pipeline graph. ([!6033])
- **CE/EE:** docs: make sure to update 8.10-to-8.11 workhorse version too. ([!6049])
- **CE/EE:** Fix "Wiki" link not appearing in navigation for projects with external wiki. ([!6057])
- **CE/EE:** Do not enforce using a hash with hidden ci key. ([!6079])
- **CE/EE:** Fix resolving conflicts on forks. ([!6082])
- **CE/EE:** Block concurrent pipeline processings. ([!6090])
- **CE/EE:** Fix sorting issues by "last updated" after import from GitHub. ([!6110])
- **CE/EE:** Fix toggler_behavior.js to toggle ajax loaded contents like `diffs` page. ([!6119])
- **CE/EE:** Fixed escaping issue with labels filter. ([!6123])

- **Omnibus GitLab:** Added shared_preload_libraries to postgresql. ([!964])
- **Omnibus GitLab:** Add postgresql option log_line_prefix for log improvements. ([!978])
- **Omnibus GitLab:** Fix the missing passing of the logrotate directory value and add specs. ([!980])

[!5942]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5942
[!5952]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5952
[!5955]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5955
[!5866]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5866
[!5980]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5980
[!5988]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5988
[!5985]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5985
[!5999]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5999
[!6023]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6023
[!6029]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6029
[!6033]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6033
[!6049]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6049
[!6057]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6057
[!6079]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6079
[!6082]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6082
[!6090]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6090
[!6110]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6110
[!6119]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6119
[!6123]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6123

[!964]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/964
[!978]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/978
[!980]: https://gitlab.com/gitlab-org/omnibus-gitlab/merge_requests/980

## Information disclosure in issue boards

It was possible for an attacker to create a new Issue Board column based on the
label of any project, including private ones, potentially leaking the label's
name and description. See [the issue][21167] for more information.

Thanks to [Jobert Abma](https://twitter.com/jobertabma) of
[HackerOne](https://hackerone.com/jobert) for responsibly disclosing this issue
to us.

[21167]: https://gitlab.com/gitlab-org/gitlab-ce/issues/21167

## Privilege escalation in project import

When importing a project from another service, it was possible for a user to
create a GitLab group when they didn't have permission to do so. See [the
issue][21457] for more information.

Thanks to [Skylar Kelty](https://hackerone.com/skylarkelty) for responsibly
disclosing this issue to us.

[21457]: https://gitlab.com/gitlab-org/gitlab-ce/issues/21457

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
