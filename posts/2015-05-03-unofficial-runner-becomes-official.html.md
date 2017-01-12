---
title: "Unofficial runner becomes official one"
date: 2015-05-03
author: Kamil Trzciński
author_twitter: ayufanpl
---

Not long time ago I built and wrote about the alternative CI runner written in Go. The single binary that can be easily run on any server with support for all latest technologies, including Docker. If you are interested here's blog post about it: [Unofficial GitLab Runner](https://about.gitlab.com/2015/04/17/unofficial-gitlab-ci-runner/). With great help of the community involved in testing today the runner becomes the official one, making the [old one](https://gitlab.com/gitlab-org/gitlab-ci-runner) written in Ruby deprecated.

<!-- more -->

## Should I migrate?

If everything works for you on the old runner, there's no need to install the Go runner unless you need some of it's specific features, like: multiple concurrent jobs or Docker support.

## How to get started?

Everything related to **GitLab CI Multi-purpose Runner** was moved to the official repository: [GitLab.com/gitlab-org/gitlab-ci-multi-runner](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/). On the official page you will be able to find a project documentation with example setups that will help you build your projects. If you have any ideas or problems please let us know by creating an issue: [Issues](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/issues). We also always happy to accept contributions: [Merge Request](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests).

## How to install?

This is really simple:

* [Install using Debian/Ubuntu/CentOS/RedHat package](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/install/linux-repository.md)
* [Install on OSX](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/install/osx.md)
* [Install on Windows](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/install/windows.md)
* [Install as Docker Service](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/install/docker.md)

## How to use it?

```bash
$ cd ~gitlab_ci_multi_runner
$ gitlab-ci-multi-runner register
```

You will be asked about how it should be configured. Once you do it you are pretty much ready to build projects.

## Final word

I'm also happy to join [GitLab Core Team](https://about.gitlab.com/core-team/). I guess that my role there will be to make this project better and better and to make the CI solution simpler and more robust.
