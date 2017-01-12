---
title: "GitLab CI 4.0 released"
date: 2013-11-21 14:15
author: Dmitriy Zaporozhets
categories: release
community: true
---

### GitLab CI version 4.0 released

Hi everyone!

Today we release a new version of GitLab CI.
We have done a lot of work to improve the flexibility of the architecture.
In addition this release contains bug fixes and UI improvements.

[![screenshot](/images/ci_4_0/dashboard.png)](/images/ci_4_0/dashboard.png)

<!-- more -->

### These are some of the awesome things in GitLab CI 4.0:


#### 1. Set up a new project in just one click

It is no longer necessary to manually copy a token from GitLab CI to the corresponding GitLab instance; GitLab CI will do this for you.
This means that it now only takes one click in GitLab CI to enable builds for your GitLab project!
Just click the 'Add' button next to your project on the GitLab CI Dashboard and you are ready to set up your build script.

[![screenshot](/images/ci_4_0/one-click.png)](/images/ci_4_0/one-click.png)

#### 2. Administrator privileges

GitLab CI 4.0 restricts certain privileges to users who have Administrator rights on the corresponding GitLab server.
Only administrators can manage runners now.

[![screenshot](/images/ci_4_0/runners.png)](/images/ci_4_0/runners.png)

In addition, administrators can list and remove projects.

[![screenshot](/images/ci_4_0/admin-projects.png)](/images/ci_4_0/admin-projects.png)

#### 3. Shared and specific runners

From now on a runner can be in one of two states: 'shared' or 'specific'.
By default every runner is 'shared' and will run builds for any project.
After a runner is assigned to a project it becomes 'specific' and it will exclusively run builds for that specific project.

[![screenshot](/images/ci_4_0/runner-page.png)](/images/ci_4_0/runner-page.png)

#### 4. New build page

We re-designed the build page a bit to concentrate more on build output, moving all additional information to right-hand side.

[![screenshot](/images/ci_4_0/build-page.png)](/images/ci_4_0/build-page.png)

#### 5. More options for build configuration

Now you can choose the method of fetching new code for each repeat build.
Before we used `git fetch` but if you want to use `git clone` it is now available as a radio button in the project settings screen.
It can be useful to use `git clone` if your project directory changes state during the build and you want to have a clean directory for each build.

#### 6. Profile page

We have also made small improvements to the profile page.

[![screenshot](/images/ci_4_0/profile.png)](/images/ci_4_0/profile.png)


*GitLab CI 4.0 requires [GitLab 6.3](/2013/11/21/gitlab-ce-6-dot-3-released) or higher*
- - -

# Setup and update links:

### [Update from GitLab CI 3.2](https://github.com/gitlabhq/gitlab-ci/blob/master/doc/update/3.2-to-4.0.md)
### [Setup](https://github.com/gitlabhq/gitlab-ci/blob/4-0-stable/doc/installation.md)
