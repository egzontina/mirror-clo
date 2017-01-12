---
title: "Getting started with GitLab and GitLab CI"
date: 2015-12-14
author: Achilleas Pipinellis
author_twitter: _axil
image_title: '/images/unsplash/stairwaycompressed.jpg'
---

This is the start of a series of posts to get you started with GitLab and
GitLab CI.

In this first post, we will explain what CI is, why you would use it, and we will
briefly explore a higher overview of the components that make GitLab and GitLab
CI work together.

Let's dive in!

<!-- more -->

## What is this CI thing?

CI stands for [Continuous Integration][ci-wiki] and has gained in popularity
the last few years. Together with [Continuous Delivery][cd-wiki] (CD), they
form the spine of modern agile software development.

Martin Fowler described this approach in [his article][ci-fowler] as:

> Continuous Integration is a software development practice where members of a
> team integrate their work frequently, usually each person integrates at least
> daily - leading to multiple integrations per day. Each integration is
> verified by an automated build (including test) to detect integration errors
> as quickly as possible.

The benefits of Continuous Integration are huge when automation plays an
integral part of your workflow.

They are many applications in the field which try to tackle this practice. The
majority of them are either closed source, making you rely on external sources
(meaning a single point of failure), or need a lot of configuration just to set
up, let alone the millions of plugins you have to install to meet your needs.

Would you rather have a CI service tightly integrated with your favorite code
management tool with next to zero configuration? If so, you will love GitLab
CI!

## Meet GitLab CI

What started as a side project [three years ago][ci-first-post], has now
become one of GitLab's key features. Back then, it was a separate application
that talked to GitLab via webhooks. Now, starting from GitLab 8.0,
GitLab CI has been [fully integrated with GitLab itself][8-post]. No more need
to setup and maintain another application, which means less work for you or
your Ops team.

GitLab CI is enabled by default on new projects, so you can start using its
features right away. All you need is a file called
[.gitlab-ci.yml](/2015/06/08/implementing-gitlab-ci-dot-yml/) (where you
describe how the build should run) placed in the root directory of your git
project, and a configured Runner to perform the actual build.

Each project comes with a Builds page where you can follow the output of each
build, see the commit that introduced it and other useful information such as
the time the build started, how long it lasted and the commiter's name.

The statuses for each build are exposed in the GitLab UI, and you can see
whether a build succeeded, failed, got canceled or skipped within a single
Merge Request or commit, or at the Merge Requests and commits pages.

Another win having GitLab CI integrated with GitLab is that people can see
other users' CI/CD approaches and learn from them.

There is one last component without which, most of the features above wouldn't
have been possible. It does all the heavy work by performing the actual builds.

Enter GitLab Runner.

## GitLab Runner

GitLab Runner is the missing piece that leverages the power of GitLab CI. A
Runner is responsible for the actual build and can be configured to be used
with one or many projects. It talks to the GitLab CI API, reads `.gitlab-ci.yml`,
follows the steps defined in that file and sends the results to GitLab CI.

Some of the key features of GitLab Runner are:

* [Is open source][runner-repo]
* Is written in Go and distributed as a single binary without any other
	requirements
* Works on Linux, OSX, *BSD and Windows (and anywhere you can run Docker)
* Easy installation as a service for Linux, OSX and Windows
* [Linux users can install it using deb or rpm packages][runner-linux-repo]
* Easy to use setup with support for Docker, Docker with SSH, Parallels or
  plain SSH running environments
* Allows to run:
  - multiple jobs concurrently
  - use multiple tokens with multiple servers (even per-project)
  - limit number of concurrent jobs per-token
* Jobs can be run:
  - locally using your shell
  - using Docker containers
  - using Docker containers and executing jobs over SSH
  - by connecting to a remote SSH server
* Supports Bash, Windows Batch and Windows PowerShell
* Allows to customize the running environment per job
* Automatic configuration reload without restart
* Enables caching of Docker containers
* List of files and directories can be attached to build after success
  (the so-called `artifacts` feature)

As you can see, there is much flexibility in installing and configuring
a GitLab Runner.

## What the future holds

We will keep pushing forward in making GitLab CI a breeze to use and extend it
to adapt to present and future technologies of the CI field.

Some notable features that we would like to see happening are listed in the
issues below:

- [Pass CI build artifacts between stages][issue-3423]
- [GitLab container registry][issue-3299]
- [GitLab Pipeline][issue-3743]
- [GitLab Deploy][issue-3286]

As always, you can visit our [direction page](/direction) and get a taste of
the forthcoming features.

## What's next? 

By now you should have an overview of what GitLab CI is and why you should
start using it.

If you are eager to give it a go, be sure to visit our [quick start guide][].

In the following posts, we will explore how to use GitLab CI to test your
projects in specific languages such as PHP.

Subscribe to our newsletter which includes links to our latest blog posts.

[ci-wiki]: https://en.wikipedia.org/wiki/Continuous_integration
[cd-wiki]: https://en.wikipedia.org/wiki/Continuous_delivery
[ci-fowler]: http://www.martinfowler.com/articles/continuousIntegration.html
[ci-first-post]: https://about.gitlab.com/2012/11/13/continuous-integration-server-from-gitlab/
[8-post]: https://about.gitlab.com/2015/09/22/gitlab-8-0-released/
[ci-page]: https://about.gitlab.com/gitlab-ci
[issue-3423]: https://gitlab.com/gitlab-org/gitlab-ce/issues/3423
[issue-3299]: https://gitlab.com/gitlab-org/gitlab-ce/issues/3299
[issue-3743]: https://gitlab.com/gitlab-org/gitlab-ce/issues/3743
[issue-3286]: https://gitlab.com/gitlab-org/gitlab-ce/issues/3286
[quick start guide]: http://doc.gitlab.com/ce/ci/quick_start/
[runner-repo]: https://gitlab.com/gitlab-org/gitlab-ci-multi-runner
[runner-linux-repo]: https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/install/linux-repository.md
