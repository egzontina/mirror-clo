---
title: "GitLab CI 4.1 released"
date: 2013-12-20 13:22
author: Dmitriy Zaporozhets
categories: release
community: true
---

### GitLab CI version 4.1 released

Hi everyone!

As you know GitLab CI is a continuous integration server.
It integrates with your GitLab installation and run tests for your projects.

Today we release a new version of GitLab CI.
The main new feature of this release is the ability to get email notifications.
You can configure a list of email notification recipients per project.
In addition GitLab CI can send emails to the author of the build commit.
You have the choice of receiving notifications for all builds or only for failed builds.

Thanks to Jeroen Knoops for contributing this feature!

<!--more-->

[![screenshot](/images/ci_4_1/email.png)](/images/ci_4_1/email.png)


*GitLab CI 4.1 requires [GitLab 6.3](/2013/11/21/gitlab-ce-6-dot-3-released/) or higher*
- - -

# Setup and update links:

### [Update from GitLab CI 4.0](https://github.com/gitlabhq/gitlab-ci/blob/master/doc/update/4.0-to-4.1.md)
### [Setup](https://github.com/gitlabhq/gitlab-ci/blob/4-1-stable/doc/installation.md)
