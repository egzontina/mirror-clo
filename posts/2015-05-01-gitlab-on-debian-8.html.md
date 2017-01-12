---
title: "GitLab on Debian 8"
date: 2015-05-01
author: Job van der Voort
author_twitter: Jobvo
---

Debian is among the most popular platforms to run GitLab on.
With the stable [release](https://www.debian.org/News/2015/20150426) of Debian 8,
we wanted to make sure that early-adopters could run GitLab on their new machines.

So from now on, GitLab Omnibus packages for Debian 8 will be available with every
release, find them on our [downloads page](/downloads).

And don't forget that we're running our package server in beta with the help
of [Packagecloud.io](https://www.packagecloud.io). You can install GitLab Community Edition with:

```
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb | sudo bash
sudo apt-get install gitlab-ce
```
