---
title: "GitLab v4.2 has been released"
date: 2013-02-21 16:45
categories: release
community: true
---

### GITLAB 4.2 has been released

Hi everyone!

Today we released GitLab v4.2 

We improved performance, fixed some bugs, added teams, users pages and more
 
<!-- more -->


### CHANGELOG

1. Features:

    * Teams
    * User show page. Via /u/username
    * Projects page. At /dashboard/projects
    * Group edit page for non-admins
    * Switchable base branch for network graph
    * Groups API added

2. Performance: 

    * Async gitolite calls
    * Process webhooks async

3. Permissions:

    * User can create group or team even if he is not admin.
    * Admin can allow/deny team or group creation for any user.

4. Misc:

    * added satellites logs
    * GFM: Fix images escaped inside links
    * Fixed project download
    * Show help contents on help pages for better navigation



### SCREENSHOTS

![discussion](/images/4_2/dashboard.png)

![discussion](/images/4_2/group_edit.png)

![discussion](/images/4_2/new_team.png)

![discussion](/images/4_2/team_page.png)

![discussion](/images/4_2/profile.png)

![discussion](/images/4_2/projects.png)


- - -

### Guides: [Update from 4.1](https://github.com/gitlabhq/gitlabhq/wiki/From-4.1-to-4.2),  [New Setup](https://github.com/gitlabhq/gitlabhq/blob/4-2-stable/doc/install/installation.md)
- - -
