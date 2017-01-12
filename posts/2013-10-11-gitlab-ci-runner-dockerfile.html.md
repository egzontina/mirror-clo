---
title: GitLab CI Runner Dockerfile
---
  [Docker](https://www.docker.io/) is an awesome tool to run virtual machines without overhead. Docker containers start in 2 seconds and use less memory and disk space. One requirements is that the host needs to be a Linux (virtual) machine.

If you use [GitLab CI](http://gitlab.org/gitlab-ci/) to run your tests you have one or more runners performing the tests. More runners are better because they enable multiple tests running in parallel. With the new [Dockerfile for GitLab CI runner](https://github.com/gitlabhq/gitlab-ci-runner/blob/master/Dockerfile) you can add runners with less overhead. Enjoy!