---
title: "GitLab without gitolite"
date: 2013-02-12 09:15
categories:
community: true
---

### Yeap GitLab 5.0 will be without gitolite

Gitolite was a real help when we started with GitLab. 
It saves us a lot of work and provide a pretty functional solution.

But after time we understood - keep gitlab and gitolite synced is harder than build own solution.

#### Problems: 

* out of sync between gitlab and gitolite
* gitolite becomes slower on bigger count of repos
* 2 system users increased complexity of setup
* code complexity, easy to make a mistake
* gitolite does not allow to create repositories, keys in simultaneously

<!-- more -->



#### GitLab Shell

GitLab Shell is my replacement for gitolite.

Basically it's a few scripts on ruby and shell for managing `/home/git/.ssh/authorized_keys` and `/home/git/repositories`

You can find [source code on github](https://github.com/gitlabhq/gitlab-shell.git)

#### 2 users -> 1 user

Earlier we have 2 users for GitLab. gitlab for GitLab and git for gitolite. 

Now its only one `git` user for GitLab and GitLab Shell


#### New GitLab directory structure

This is the directory structure you will end up with following the instructions in the Installation Guide.

    |-- home
    |   |-- git
    |       |-- .ssh
    |       |-- gitlab
    |       |-- gitlab-satellites
    |       |-- gitlab-shell
    |       |-- repositories



#### PROFIT


##### 1. Amount of code 

Its was ~ 1000 lines of code related to gitolite inside of GitLab. And one library for parsing gitolite config. 

Now it is only 150 lines of pretty simple code related to gitlab shell. 

##### 2. Performance 

For [https://gitlab.com](https://gitlab.com) we decreased project creation time in 10 times. 

##### 3. Stability

GitLab Shell does not store Access Control List. It asks GitLab for permissions via api. 

No out of sync between GitLab and GitLab Shell == much stable backend solution.

##### 4. Simplicity of update

You can update gitlab-shell just by `git pull`

You dont even need to restart gitlab service


- - -

### Feb 22: GitLab 4.2 - last release with gitolite
### Mar 22: GitLab 5.0 - requires gitlab-shell

- - -

Currently I'm working on migration docs to GitLab 5.0.0pre. You can find a [draft here](https://github.com/gitlabhq/gitlabhq/wiki/From-4.2-to-5.0)
