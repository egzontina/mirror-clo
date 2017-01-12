---
title: "GitLab 4.0 released"
date: 2012-12-23 14:20
categories:
community: true
---

### GITLAB 4.0 released

Hi everyone!

Finally we released GITLAB v4.0.0!

There are a lot of changes so we introduce you to the important one

<!-- more -->


### Application behaviour changes:

* New projects will be namespaced (ex. gitlab/vagrant )
* Every group got own directory in gitolite
* All projects of group will be moved under group directory ( git remote should be updated )
* Projects w/o groups will stay with same remote
* User got username ( For existsing users it will be generated based on email )
* User create project under his username ( ex. randx/my-project )
* User can change username. All projects under his username will be moved 
* Group got owner
* Owner can create projects within group
* Owner can access every project within a group
* Admin can transfer any project from one namespace(group, user, global) to another
* Group or user is a namespace for project. Owner of namespace is an owner of project

### Other changes

* Better PostgreSQL support
* Added email notificatino on project move
* Fixed email notification on issue close/reopen
* Reorganized settings
* Fixed commits compare
* Update the UI to allow downloading Patch or Diff for Commit, MR
* Milestones can be closed now. Milestone stays open unless you close it
* Show comment events on dashboard
* Quick add team members via group#people page
* UI improvements
* In admin area projects, users and groups sorted alphabetically
* Issue management page on dashboard improved
* Better integration with GitLab CI ( requires GitLab CI  v1.1.1 )

### What we removed in 4.0:

* gitolite 2 support
* SQLite support (I like it but this database got locked when several users use gitlab at once)
* API v2 support (its simply incompatible with namespaced projects)

### What should be updated during migration:

* gitlab.yml config
* gitolite post-receive hooks
* permissions on /home/git/repositories/
* python2 symlink

## Screenshots:
Dashboard: 
![Screens](/images/4_0/gitlab_dash.png)
Merge Request with CI status
![Screens](/images/4_0/gitlab_project_mr.png)
Files browsing
![Screens](/images/4_0/gitlab_project_tree.png)
Issues
![Screens](/images/4_0/gitlab_project_issues.png)

### How to reinstall gitolite with new version

* [Reinstall gitolite](https://github.com/gitlabhq/gitlabhq/wiki/Reinstall-gitolite)

### How to migrate from sqlite 

* [Follow this guide](https://github.com/gitlabhq/gitlabhq/wiki/Migrate-from-SQLite-to-MySQL)

### How to install GitLab v4.0.0 

* [Complete Installation guide (Recommended)](https://github.com/gitlabhq/gitlabhq/blob/4-0-stable/doc/install/installation.md)
* [One-script installer for ubuntu 12.04 x64](https://github.com/gitlabhq/gitlab-recipes/tree/master/install/v4)

### How to update a GitLab to v4.0.0 

* [Update guide for v3.1](https://github.com/gitlabhq/gitlabhq/wiki/From-3.1-to-4.0)
* [Update guide for v3.0](https://github.com/gitlabhq/gitlabhq/wiki/From-3.0-to-4.0)
