---
title: "GitLab.com now runs GitLab Enterprise Edition"
date: 2014-06-27
categories:
author: Sytse Sijbrandij
---

[GitLab.com](https://about.gitlab.com/gitlab-com/) now runs [GitLab Enterprise Edition (EE)](https://about.gitlab.com/gitlab-ee/).
GitLab.com is our free SaaS offering allowing you to use GitLab with private repositories and unlimited collaborators.
You now get to use the most fully featured GitLab edition on GitLab.com.

<!--more-->

The reason for this is twofold.
First, we want to make it easy to allow you to experience all GitLab features.
Second, we want to run EE at scale ourselves since it contains more features than CE.
We want to be able to monitor all features on our own server for things like performance regressions.
Monitoring our own servers is much easier since we have access to all graphs and logs.
This way we can solve problems before anybody notices them.

By the way, besides GitLab.com we also run another installation.
This is a server accessible only to GitLab B.V. employees because problems here are more noticeable to end users.
This server is updated daily to the master branch of GitLab Community Edition.
This ensures we quickly discover situations where someone merged a breaking change.
