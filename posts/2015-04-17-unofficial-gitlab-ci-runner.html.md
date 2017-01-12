---
title: "Unofficial GitLab CI Runner"
date: 2015-04-17
author: Kamil Trzciński
author_twitter: ayufanpl
---

[GitLab CI Multi-purpose Runner](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner) is yet another CI runner, but this time written in Go with a vast number of features that leverage all the latest technologies. It's an unofficial project made by me, Kamil Trzciński, with love for GitLab CI to help aid some problems with current runner and make the use of CI really simple and secure.

<!-- more -->

## Why it was created?

I created that project, because I needed a runner that allows to use virtualization technology (Docker and Parallels for OSX) to build our ([Polidea](https://www.polidea.com/)) projects. The main reason is that the official GitLab-CI-Runner is a very simple application written in Ruby, but works well in quite basic setups. You can think of it as a reference implementation of what a bare runner can look like. It's distributed as source code or as a simple omnibus package to install on one of the supported Linux distributions. However, there are some areas where that makes it quite hard to use:

* The runner can only run one concurrent at a time. If you want to run more either you set up a new server or create an additional user to build the jobs.
* What is important is that the official runner always runs projects on the server shell. This makes it really hard to test projects using different versions of Ruby or any other dependencies. It also makes the build environment dirty and builds are not really 100% reliable. This collides with a recent approach to always have a clean build environment.
* The runner works only on Linux-based platforms and it's not really an easy task to make the runner a service that is run at system start. Additional hacks are required to make it run on OSX. There is no support for Windows. 
* It's quite hard to set up the next server with all dependencies required to build project.
* It's quite hard to perform some administrative tasks with the official runner.

## Why do I need it?

The Gitlab-CI Multi-purpose Runner is one binary that you can put on your machine of any kind. It is really easy to set up as a service and can work with multiple projects and multiple GitLab CI coordinators. With support for Docker it makes it really easy to setup build environment with different versions of packages. 

## How to install?

It's really simple. There's a multiple ways to install GitLab-CI Multi-purpose Runner:

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

## Maybe use Docker?

You can also use Docker to create runner with specific dependencies. What is important that every time your project is built it will be run in clean environment without any leftovers from previous builds. With this simple commands below you don't have to install any dependencies, because Docker will download everything required to run your tests.

```bash
$ cd ~gitlab_ci_multi_runner
$ gitlab-ci-multi-runner register \
  --non-interactive \
  --url "https://ci.gitlab.com/" \
  --registration-token "REGISTRATION_TOKEN" \
  --description "Ruby 2.1 with MySQL" \
  --executor "docker" \
  --docker-image ruby:2.1 --docker-mysql latest

$ gitlab-ci-multi-runner register \
  --non-interactive \
  --url "https://ci.gitlab.com/" \
  --registration-token "REGISTRATION_TOKEN" \
  --description "Python 3.4 with MySQL" \
  --executor "docker" \
  --docker-image python:3.4 --docker-mysql latest
```

The exemplary integrations for GitLab CE and GitLab CI can be found here:

* [Integrate GitLab CE](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/examples/gitlab.md)
* [Integrate GitLab CI](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/examples/gitlab-ci.md)

## Why Go?

Go is pretty young language already used by same major brands (Docker). It's proven to be stable, well supported with pretty rich library. However the most important thing is that Go compiler can produce single binary without any dependencies for Linux, Mac OS X, FreeBSD, NetBSD, OpenBSD, Plan 9 and Microsoft Windows and the i386, amd64, ARM and IBM POWER processor architectures. The binary is of reasonable size (around 10MB in case of GitLab-CI-Multi-Runner).
What is important is that this is the one project to rule them all. With Go's multiplatform approach it is really simple to build projects than can run on all platforms and in most cases it's sufficient to distribute the application binary only, because it has all required bits to run the project.

## Features

* Allows to run:
 - multiple jobs concurrently
 - use multiple tokens with multiple server (even per-project)
 - limit number of concurrent jobs per-token
* Jobs can be run:
 - locally
 - using a Docker container
 - using a Docker container and executing jobs over SSH
 - using dynamically provisioned Parallels VM machines
 - connecting to a remote SSH server
* Is written in Go and is also distributed as single binary without any other requirements
* Supports Bash, Windows Batch and Windows PowerShell
* Works on Ubuntu, Debian, OS X and Windows (and anywhere you can run Docker)
* Allows to customize job running environment
* Automatic configuration reload without restart
* Easy to use setup with support for all running environments
* Support for caching when using Docker containers
* Support to make runner a Service on Linux, OSX and Windows
* Current jobs are aborted when service receives interrupt signal - ex. when shutting down the server.

## Is it stable?

This runner has been in use for quite some time already to build our mobile projects at [Polidea](https://www.polidea.com/). Polidea is a mobile software house that creates and develops apps for a variety of clients. We like customizing and improving our processes as much as possible to make the development process as smooth as it gets – and to create great tools for everyone. We will soon be publishing series of posts how we use GitLab CI to build projects for Android and iOS devices.

## This project needs your help

I think that you got interested. Please try to run it and post some comments on how it works for you. You can also join discussion on [GitLab.com](https://gitlab.com/gitlab-org/omnibus-gitlab-runner/issues/7#note_1074777) whether this runners should become the official one. Thanks!
