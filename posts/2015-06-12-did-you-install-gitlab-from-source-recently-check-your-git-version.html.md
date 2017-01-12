---
title: "Did you install GitLab from source? Check your Git version"
date: 2015-06-12
author: Jacob Vosmaer
author_twitter: jacobvosmaer
---

Although the preferred way to install GitLab is to use our [omnibus
packages](/downloads), you can also install GitLab Community Edition or
Enterprise Edition 'from source'. If you used this installation method, and if
you compiled Git from source in the process then please check whether your Git
version defends against Git vulnerability CVE-2014-9390. This issue does not
apply to our Omnibus packages (DEB or RPM).

<!-- more -->

Although [GitLab itself is not affected by
CVE-2014-9390](/2014/12/19/gitlab-not-affected-by-CVE-2014-9390-git-vulnerability/),
a GitLab server may be used to deliver 'poisoned' Git repositories to users on
vulnerable systems. Upgrading Git on your GitLab server stops users from
pushing poisoned repositories to your GitLab server.

Due to an oversight, the [guide for installing GitLab from
source](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/install/installation.md)
still contained instructions telling administrators to install Git 2.1.2 if the
version of Git provided by their Linux distribution was too old. Git 2.1.2 does
not defend against CVE-2014-9390.

If your GitLab server uses `/usr/local/bin/git` please check your Git version
using the instructions in this [upgrade
guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/7.11-to-7.12.md#0-double-check-your-git-version).
