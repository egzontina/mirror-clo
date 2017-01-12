---
title: "GitLab 7.13.2 released"
date: 2015-07-28
author: Valery Sizov
author_twitter: gitlab
---

We've released GitLab 7.13.2 for GitLab CE, EE and CI.

It includes the following fixes for CE and EE:

  - Fix randomly failed spec
  - Create project services on Project creation
  - Add admin_merge_request ability to Developer level and up
  - Fix Error 500 when browsing projects with no HEAD (Stan Hu)
  - Fix labels / assignee / milestone for the merge requests when issues are disabled
  - Show the first tab automatically on MergeRequests#new
  - Add rake task 'gitlab:update_commit_count' (Daniel Gerhardt)
  - Fix Gmail Actions


<!-- more -->

## Upgrade barometer

This release upgrade will require downtime, because redis has been updated to 2.8.21.

## Updating

To update, check out our [update page](https://about.gitlab.com/update).

## Enterprise Edition

Interested in GitLab Enterprise Edition?
For an overview of feature exclusive to GitLab Enterprise Edition please have a look at the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/pricing).
No time to upgrade GitLab yourself?
A subscription also entitles to our upgrade and installation services.