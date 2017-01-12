---
title: "Announcing GitLab CI 3.0"
date: 2013-07-09 13:01
categories:
community: true
---

### Announcing GitLab CI 3.0

We are excited to announce the [release](https://twitter.com/gitlab/status/353214946978459648) of GitLab CI 3.0, the latest version of our Continuous Integration system that connects with GitLab.
This is a major redesign, reflecting our recent [ideas of what a CI system should look like](/2013/06/20/integrating-gitlab-ci-with-gitlab): a flexible architecture for distributed, isolated builds.
GitLab CI 3.0 consists of two components: the [coordinator](https://github.com/gitlabhq/gitlab-ci) and its [runners](https://github.com/gitlabhq/gitlab-ci-runner)

<!-- more -->

### The Coordinator
The [coordinator](https://github.com/gitlabhq/gitlab-ci) is a Rack app that can run on the sames server as your GitLab installation.
It provides a status and management interface for all your builds.
The coordinator manages the build queues for all the projects you have registered with it and assigns the builds to individual runners.

[![View builds for a CI project](/images/ci_3_0/gitlab_ci_3.0_overview.png)](/images/ci_3_0/gitlab_ci_3.0_overview.png)

You can associate multiple runners to one CI project.
This would allow you for example to have test suites running for two feature branches at the same time.

[![Multiple runners for one CI project](/images/ci_3_0/gitlab_ci_3.0_multiple_runners.png)](/images/ci_3_0/gitlab_ci_3.0_multiple_runners.png)

You can also associate secondary CI projects to a single GitLab project. We use this to run the test suite for [gitlabhq](https://github.com/gitlabhq/gitlabhq) on a machine running MySQL (the primary build) and on another one running PostgresSQL (the secondary build).

[![Attach a CI project as a primary or secondary build](/images/ci_3_0/gitlab_ci_3.0_multiple_projects.png)](/images/ci_3_0/gitlab_ci_3.0_multiple_projects.png)

### The Runners
A [runner](https://github.com/gitlabhq/gitlab-ci-runner) is a Ruby process that asks its coordinator for build jobs to perform.
You can host a runner on a dedicated build server, a VM, a spare laptop, etc.
One machine may host multiple runners.
For example, you could use two runners on the same machine to build release packages and publish the static company website.
On the other hand, runners can also be isolated.
For instance, a runner that will publish your website may need special credentials.
By isolating this runner in a trusted environment you can restrict access to the publishing credentials.
The runner only needs to have network access to its coordinator and to your GitLab installation.

### This is just the beginning
These are just a few of the possible uses and configurations of the new GitLab CI.
We look forward to hearing your stories!
