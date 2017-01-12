---
title: "GitLab 4.0 release details and schedule"
date: 2012-12-20 19:20
categories:
community: true
---

### Some details of upcoming GitLab 4.0 and release date

### Release schedule:

* Dec 21..22 - we test 4.0 release candidate
* Dec 22..23 - we will merge master into stable
* Dec 23 - Installation docs is ready. 4.0 is ready for fresh install
* Dec 24 - Updating docs. You will be able to migrate your GitLab instances to 4.0


<!-- more -->

### Important changes:

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

### Migration notes:

* Required: replace gitolite hooks
* Required: activate namspaces
* Required: update permissions on /home/git/repositories/
* Strongly recommended: replace gitlab.yml with new one

