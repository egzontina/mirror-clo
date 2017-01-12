---
title: "GitLab CI 4.2 released"
date: 2014-01-30 13:22
author: Dmitriy Zaporozhets
categories: release
community: true
---

### GitLab CI version 4.2 released

Hi everyone!

As you know GitLab CI is a continuous integration server.
It integrates with your GitLab installation and runs tests for your projects.

Today we release a new version of GitLab CI.

[![screenshot](/images/ci_4_2/build.png)](/images/ci_4_2/build.png)

<!--more-->

## Improvements

### Responsive UI

We have upgraded our front-end code to use Twitter Bootstrap 3.
Thanks to this upgrade we now support devices with resolutions of 768x1024 and higher.

Below you can see the result in a desktop screenshot and an iPad screenshot.

[![screenshot](/images/ci_4_2/dash.png)](/images/ci_4_2/dash.png)
[![screenshot](/images/ci_4_2/ipad.png)](/images/ci_4_2/ipad.png)

### Build duration chart

You can now see the build duration of the last 30 builds in one handy chart.

[![screenshot](/images/ci_4_2/chart.png)](/images/ci_4_2/chart.png)

### Turbolinks

We have added turbolinks support to GitLab CI.
Turbolinks makes following links in your web application faster.
Instead of letting the browser recompile the JavaScript and CSS between each page change, it keeps the current page instance alive and replaces only the body and the title in the head. 

- - -

*GitLab CI 4.2 requires [GitLab 6.3](/2013/11/21/gitlab-ce-6-dot-3-released/) or higher*
- - -

# Setup and update links:

### [Update from GitLab CI 4.1](https://gitlab.com/gitlab-org/gitlab-ci/blob/master/doc/update/4.1-to-4.2.md)
### [Fresh installation](https://gitlab.com/gitlab-org/gitlab-ci/blob/4-2-stable/doc/install/installation.md)
