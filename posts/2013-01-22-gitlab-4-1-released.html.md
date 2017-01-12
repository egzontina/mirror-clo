---
title: "GitLab 4.1"
date: 2013-01-22 17:20
categories: release
community: true
---

### GITLAB 4.1 Released

Hi everyone!

Today we released GitLab v4.1.0. 

We improved performance, fixed some bugs, added public repos and more
 
<!-- more -->

### Good news 

We have some very good news to share. From today onwards, __[Dmitriy Zaporozhets](https://github.com/randx) will work on GitLab development full time!__ 

In the last year, GitLab has grown from a small project to a grown-up solution.
Right now, more than 10.000 organizations have upgraded to GitLab 4.0! [link](http://rubygems.org/gems/gitlab_meta)

Dmitriy wants to give GitLab his full attention and continue giving the community great features each month. 
To do this, we will need your help. If you like GitLab and want to help with the development, please make a donation. [Donation page](http://gitlab.org/donate/)

### Replaced Resque with Sidekiq:

We replaced Resque with Sidekiq to proccess background jobs. 
Sidekiq uses threads instead of forks so it is much more efficient with memory compared to Resque.

### Discussions:

We improved comments system, especially for merge requests. You see it shows a code related to comments

![discussion](/images/4_1/discussion.png)

### Optional SignUp:

You can enable signup page.

![signup](/images/4_1/signup.png)

### Public mode:

GitLab allows you to open selected projects to be accessed publicly.
These projects will be clonable without any authentication.
Also they will be listed on the public access directory

![signup](/images/4_1/public_dir.png)


### Remember dashboard filter in cookies:

![dashboard](/images/4_1/dashboard.png)


### Line numbers for git blame:

![dashboard](/images/4_1/line-numbers-blame.png)

### Show line diff stats:

![dashboard](/images/4_1/gitlab-line-diff.png)



### CHANGELOG

  - Optional Sign-Up
  - Discussions
  - Satellites outside of tmp
  - Line numbers for blame
  - Project public mode
  - Public area with unauthorized access
  - Load dashboard events with ajax
  - Remember dashboard filter in cookies
  - Replace resque with sidekiq
  - Fix routing issues
  - Cleanup rake tasks
  - Fix backup/restore
  - Show preview for note images 
  - Improved network-graph
  - Reduce amount of gitolite calls
  - Ability to add user in all group projects
  - Remove deprecated configs
  - Replaced Korolev font with open font
  - Restyled admin/dashboard page
  - Restyled admin/projects page



- - -

### Guides: [Update from 4.0](https://github.com/gitlabhq/gitlabhq/wiki/From-4.0-to-4.1),  [New Setup](https://github.com/gitlabhq/gitlabhq/blob/4-1-stable/doc/install/installation.md)
- - -
