---
title: "GitLab 6.0 released"
date: 2013-08-20 19:30
categories: release
community: true
---

### GitLab 6.0 released!

Hi everyone!

Today we present a new major GitLab version. There are a lot of improvements to make GitLab even more awesome.

![gitlab](/images/6_0/signin.png)

<!--more-->

### First and foremost are the improved groups. 

![gitlab](/images/6_0/group_members.png)

From now on a group is not just a directory for projects. It also allows you to add users. After user is added to group - it automatically get access to all existing and new projects inside group. 
You can also have have multiple owners for a group who can manage members/projects. With this GitLab becomes more group oriented. That is why we no longer support global namespaces. Project can be part of group or user only.

### Merge requests are now possible between a fork and the original project.

![gitlab](/images/6_0/mr_on_fork_edit.png)
![gitlab](/images/6_0/mr_on_fork.png)

Another nice improvement comes from contributor __Izaak Alpert__. 
It allows you to use different workflow depending on your needs.

Still we have more things to present. 

### Now you can create or remove both git branches and tags with the GitLab UI.

![gitlab](/images/6_0/branches.png)
![gitlab](/images/6_0/create-tags.png)

It gives you ability to work with the web ui only. For example to create branch, fix something with the web editor and submit a Merge Request.

### Also we polished our UI and made a lot of bug fixes. 

![gitlab](/images/6_0/Dashboard.png)

Under the hood we refactored a lot of stuff and improved the performance. 
And one last piece of good news. The upgrade to 6.0 is not so complicated as it used to be for major versions. The only big change is that all projects must be part of a group or user. A bit of preparations, few commands - and you are running GitLab 6.

- - - 

#### GitLab 6.0 will be the first release that will also be available in an Enterprise Edition, for more information please see [the GitLab.com Blog](http://www.gitlab.com/2013/08/22/introducing-gitlab-6-0-enterprise-edition/)

- - - 

### Links

For full list see [CHANGELOG](https://github.com/gitlabhq/gitlabhq/blob/master/CHANGELOG)

For new setup follow [Setup Guide](https://github.com/gitlabhq/gitlabhq/blob/6-0-stable/doc/install/installation.md)

__For update instructions see [Update Guide](https://github.com/gitlabhq/gitlabhq/blob/master/doc/update/5.4-to-6.0.md)__

No time to upgrade or maintain Gitlab yourself? GitLab.com offers [upgrade consulting services](http://www.gitlab.com/consultancy/) and [support subscriptions](http://www.gitlab.com/subscription/).
