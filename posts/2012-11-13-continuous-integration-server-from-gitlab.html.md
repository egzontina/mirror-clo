---
title: "Continuous integration server from GitLab"
date: 2012-11-13 16:00
categories:
community: true
---

### Continuous integration server from GitLab

Hi everyone!

Today I'd like to share a new software crafted by me and Valeriy Sizov. 

Its more than year since we released first version of GitLab. And we dont want to stop on it. 

We wish to have a continuous integration server closely integrated with GitLab.

And today we announced another FOSS software for developers. Its GitLab CI.

![Screenshot](/images/ci_1_0/gitlab_ci_preview.png)

<!-- more -->

[Source Code](https://github.com/gitlabhq/gitlab-ci)


**GitLab CI is based on Ruby on Rails and Resque/Redis and**

**GitLab CI supports only git SCM.**

**GitLab CI requires present of GitLab instance with webhooks setup to make builds automatically**

### How it works: 

1. First of all you need to setup GitLab CI on VPS or any linux server
2. Then you clone projects you want to test and setup test environment
3. Next step is just add projects to GitLab CI via web UI
  ![Screenshot](/images/gitlab_ci_new_project.png)
4. Add just copy HTTP POST url provided by GitLab CI to your GitLab webhooks
  ![Screenshot](/images/gitlab_ci_project.png)
5. When you push code to GitLab webhook will trigger CI to make a build


[Source Code](https://github.com/gitlabhq/gitlab-ci)
