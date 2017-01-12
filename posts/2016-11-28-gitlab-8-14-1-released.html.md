---
layout: post
title: "GitLab 8.14.1, 8.13.7 and 8.12.10 Released"
date: 2016-11-28
author: GitLab
author_twitter: gitlab
---
Today we are releasing version 8.14.1, 8.13.7 and 8.12.10 for GitLab Community Edition (CE) and
Enterprise Edition (EE).
This version contains an important security fix for a critical remote command
execution vulnerability in Mattermost, and we **strongly recommend** that anyone
running GitLab 8.14.0 with Mattermost enabled upgrade to this version
**immediately**.
Please read on for more details.
<!-- more -->
## Remote Command Execution via Mattermost Service in 8.14.0
Mattermost recently released a critical security update to address a remote
command execution vulnerability. Because the Omnibus version of GitLab 8.14.0
ships with Mattermost we are providing this emergency security patch.
Details of the vulnerability can be found at
[https://docs.mattermost.com/administration/changelog.html#release-v3-5-1](https://docs.mattermost.com/administration/changelog.html#release-v3-5-1)

We **strongly recommend** that all installations running GitLab 8.14.0 with
Mattermost enabled upgrade immediately. Mattermost is *not* enabled by default.
### Workarounds
If you're unable to upgrade right away, you can secure your GitLab installation
against this vulnerability using the workaround outlined below until you have
time to upgrade.
#### Disable Mattermost
Login to your GitLab server(s) and perform the following:
1. Edit your `/etc/gitlab/gitlab.rb` file
1. Verify `mattermost['gitlab_enable']` is set to `false`
1. Save the file
1. Run `sudo gitlab-ctl reconfigure`
Note: If you are running Mattermost on an external server and not through GitLab
this workaround will not be sufficient. Please consult your Mattermost
documentation on how to disable the service until you can install the patch.

## 8.14.1, 8.13.7 and 8.12.10 Security fixes

### Users with Read Access to a Project Can Create Labels
Hari Gopal reported a vulnerability involving non-members of a project who have
read-only access being able to create labels inside the project. [#23416](https://gitlab.com/gitlab-org/gitlab-ce/issues/23416)
### Information Disclosure for Private Project Names
An internal code review discovered that it was possible to enumerate private
project names. [#22869](https://gitlab.com/gitlab-org/gitlab-ce/issues/22869)
### Information Disclosure for Private Issues
An internal code review discovered that it was possible to read private issues
using specifically-crafted search queries for projects with issues visibility
restricted to ‘Only team members'.

## Other fixes in 8.14.1

This version resolves a number of regressions and bugs in the [recent 8.14 release](https://about.gitlab.com/2016/11/22/gitlab-8-14-released/).
- CE/EE: Fix deselecting calendar days on contribution graph ([!6453](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6453))
- CE/EE: 500 error on project show when user is not logged in and project is still empty ([!7376](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7376))
- CE/EE: Unify all MR widget text colors and background colors ([!7571](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7571))
- CE/EE: If Build running change accept merge request when build succeeds button from orange to blue ([!7577](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7577))
- CE/EE: External jobs do not have show page nor traces ([!7617](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7617))
- CE/EE: Issue creation now accepts trailing whitespace ([!7633](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7633))
- CE/EE: Resolve "Labeling system notes downcase labels" ([!7636](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7636))
- CE/EE: Fix NPM install warnings due to incompatible dependency version ([!7641](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7641))
- CE/EE: Clean up globals exemptions within .eslintrc ([!7642](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7642))
- CE/EE: Fix IID filter for merge requests and milestones ([!7648](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7648))
- CE/EE: Fix sidekiq stats in admin area ([!7654](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7654))
- CE/EE: Fix exceptions when loading build trace ([!7658](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7658))
- CE/EE: Fixed bug to do with calculating durations ([!7663](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7663))
- CE/EE: Resolve "Wrong `render 'index'`, should be `render 'show'` in `Projects::PipelinesSettingsController#update`" ([!7665](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7665))
- CE/EE: Fix spacing between icon and word in status badge ([!7678](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/7678))
- EE: Fix MergeRequestSerializer breaks on  when source_project doesn't exist anymore ([!903](https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/903))

## Upgrade barometer
These versions do not include any new migrations, and should not require any
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
Access to GitLab Enterprise Edition is included with a
[subscription](https://about.gitlab.com/pricing/). No time to upgrade GitLab
yourself? Subscribers receive upgrade and installation services.
