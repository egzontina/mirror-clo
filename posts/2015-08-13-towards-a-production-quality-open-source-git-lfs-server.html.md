---
title: "Towards a production quality open source Git LFS server"
date: 2015-08-13
author: Sytse Sijbrandij
author_twitter: sytses
image_title: '/images/unsplash/FILENAME.jpg'
---

## Update

Since GitLab 8.2 we [supports Git LFS](https://about.gitlab.com/2015/11/23/announcing-git-lfs-support-in-gitlab/) in GitLab CE and EE.

## Original article

At GitLab we would love to be compatible with Git Large File Support (LFS).
We plan to base our implementation on a reference implementation that is currently not in a production ready state.
But we hope that over time we can get to production level support.
What follows is some background how and why we are taking this path instead of reusing an existing solution.

<!-- more -->

Git repositories can't get larger than a few gigabytes so if you want to use large binaries you need to extend it.
The most extensive open source project to do this is Git Annex, which [started in 2010](https://en.wikipedia.org/wiki/Git-annex).
There were many other projects similar to this such as [Git Media](https://github.com/alebedev/git-media).
GitHub chose to start a new project in private called Git LFS [in September 2013 based on Git Media](https://github.com/github/git-lfs/commit/d8f780329b64e789553bc8ccccfb993ebc430325).

In February of 2015 we [released support for Git Annex](https://about.gitlab.com/2015/02/17/gitlab-annex-solves-the-problem-of-versioning-large-binaries-with-git/) in our proprietary GitLab Enterprise Edition.
Almost all of the code to support this was included in the open source [GitLab Shell](https://gitlab.com/gitlab-org/gitlab-shell).

In April of 2015 GitHub [announced Git LFS](https://github.com/blog/1986-announcing-git-large-file-storage-lfs) and open sourced [the client](https://github.com/github/git-lfs) and a [reference implementation for the server](https://github.com/github/lfs-test-server).
The reference implementation is called 'lfs-test-server' and the [first section of the readme](https://github.com/github/lfs-test-server#lfs-test-server) mentions that "It is intended to be used for testing the Git LFS client and is not in a production ready state."
The client implementation is really well done and many people request support for it [on our feature request tracker](http://feedback.gitlab.com/forums/176466-general/suggestions/7502608-git-large-file-storage-lfs-support).

Obviously we would like to support it properly and wondered [if the test server code is something we can use in production](https://twitter.com/gitlab/status/623089117983821824).
We did not get a response to the above tweet nor to an email we sent.
Of course nobody owes us a response and GitHub is free to do as they please with their code.

Interestingly a day later the twitter account [gitlabceohere](https://twitter.com/gitlabceohere) is also [in the market for something production-ready](https://twitter.com/gitlabceohere/status/623521722424295425).
We don't know who is behind the account (which has been pretty funny so far), we only know that the first 6 [followers of the account](https://twitter.com/gitlabceohere/followers) are all current or former GitHub employees.

We think that the best course of action is to use the Git LFS reference implementation and make it work for GitLab.
Unfortunately we'll have to fork the project since we have to remove the [user management that is included in the project](https://github.com/github/lfs-test-server#running).
Of course our fork will be open source and in addition we plan to add Git LFS support to both GitLab CE and EE.
The work on this has already started with https://github.com/gitlabhq/gitlab-shell/pull/230#issuecomment-116735181 that was contributed by Artem Navrotskiy.
Hopefully there will be more merge requests from the rest of the community and the people at GitLab the company will do their best to contribute too.
Currently our estimate is to release an alpha version of Git LFS with GitLab 8.1 and a beta in 8.2.
