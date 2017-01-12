---
title: "GitLab Runner 1.1 with Autoscaling"
date: 2016-03-29 14:00
categories: release
author: Kamil Trzciński
author_twitter: ayufanpl
image_title: '/images/unsplash/high-road.jpg'
---

Over the last year, GitLab Runner has become a significant part of the GitLab
family. We are happy to announce that GitLab Runner 1.1 is released today; a
release that brings major improvements over its predecessor. There is one
feature though that we are excited about and is the cornerstone of this release.

Without further ado, we present you GitLab Runner 1.1 and its brand-new, shiny
feature: Autoscaling!

<!-- more -->

## About GitLab Runner

GitLab has [built-in continuous integration][doc-ci] to allow you to run a
number of tasks as you prepare to deploy your software. Typical tasks
might be to build a software package or to run tests as specified in a
YAML file. These tasks need to run by something, and in GitLab this something
is called a [Runner][doc-runners]; an application that processes builds.

GitLab Runner 1.1 is the biggest release yet. Autoscaling provides the ability
to utilize resources in a more elastic and dynamic way. Along with autoscaling
come some other significant features as well. Among them is support for a
distributed cache server, and user requested features like passing artifacts
between stages and the ability to specify the archive names are now available.

Let's explore these features one by one.

## The Challenge of Scaling

Other continuous integration platforms have a similar functionality.
For example, Runners are called "Agents" in Atlassian's Bamboo (which integrates
with Bitbucket.) Some services, like Bamboo, charge individually for using these
virtual machines and if you need a number of them it can get quite expensive,
quite quickly. If you have only one available Agent or Runner, you could be
slowing down your work.

We don't charge anything for connecting Runners in GitLab, it’s all built-in.
However, the challenge up until now has been the scaling of these Runners. With
GitLab, Runners can be specified per project, but this means you have to create
a Runner per project, and that doesn't scale well.

An alternative up until now was to create a number of [shared Runners] which
can be used across your entire GitLab instance.

However, what happens when you need more Runners than there are available?
You end up having to queue your tasks, and that will eventually slow things down.

Hence the need for autoscaling.

## Autoscaling increases developer happiness

We decided to build autoscaling with the help of [Docker Machine][docker-machine].
Docker Machine allows you to provision and manage multiple remote Docker hosts
and supports a vast number of [virtualization and cloud providers][docker-machine-driver],
and this is what autoscaling currently works only with.

Because the Runners will autoscale, your infrastructure contains only as
many build instances as necessary at anytime. If you configure the Runner to
only use autoscale, the system on which the Runner is installed acts as a
bastion for all the machines it creates.

Autoscaling allows you to increase developer happiness. Everyone hates to wait
for their builds to be picked up, just because all Runners are currently in use.

The autoscaling feature promotes heavy parallelization of your tests, something
that is made easy by defining multiple [jobs] in your `.gitlab-ci.yml` file.

While cutting down the waiting time to a minimum makes your developers happy,
this is not the only benefit of autoscaling. In the long run, autoscaling
reduces your infrastructure costs:

- autoscaling follows your team's work hours,
- you pay for what you used, even when scaling to hundreds of machines,
- you can use larger machines for the same cost, thus having your builds run
  faster,
- the machines are self-managed, everything is handled by docker-machine, making
  your Administrators happy too,
- your responsibility is to only manage GitLab and one GitLab Runner instance.

Below, you can see a real-life example of the Runner's autoscale feature, tested
on GitLab.com for the [GitLab Community Edition][ce] project:

![Real life example of autoscaling](/images/runner_1_1/auto-scaling-gitlab-com.png)

Each machine on the chart is an independent cloud instance, running build jobs
inside Docker containers. Our builds are run on DigitalOcean 4GB machines, with
CoreOS and the latest Docker Engine installed.

[DigitalOcean] proved to be one of the best choices for us, mostly because of
the fast spin-up time (around 50 seconds) and their very fast SSDs, which are
ideal for testing purposes. Currently, our GitLab Runner processes up to 160
builds at a time.

If you are eager to test this yourself, read more on [configuring the new
autoscaling feature][doc-autoscale].

## Distributed cache server

In GitLab Runner 0.7.0 we introduced support for [caching]. This release brings
improvements to this feature too, which is especially useful with autoscaling.

GitLab Runner 1.1 allows you to use an external server to store all your caches.
The server needs to expose an S3-compatible API, and while you can use for
example Amazon S3, there are also a number of other servers that you can run
on-premises just for the purpose of caching.

Read more [about the distributed cache server][doc-cache] and learn how to set
up and configure your own.

## Artifacts improvements

We listen closely to our community to extend GitLab Runner with user requests.
One of the often-requested features was related to passing artifacts between
builds.

GitLab offers some awesome capabilities to define multiple [jobs] and group
them in different [stages]. The jobs are always independent, and can be run on
different Runners.

Up until now, you had to use an external method if you wanted to pass the files
from one job to another. With GitLab Runner 1.1 this happens automatically.
Going one step further, GitLab 8.6 allows you to fine-tune _what_ should be
passed. This is now handled by defining [dependencies]:

```yaml
build:osx:
  stage: build
  artifacts: ...

test:osx:
  stage: test
  dependencies:
  - build:osx
```

The second most-requested feature was the ability to change the name of the
uploaded artifacts archive. With GitLab Runner 1.1, this is now possible with
this simple syntax:

```yaml
build_linux:
  artifacts:
    name: "build_linux_$CI_BUILD_REF_NAME"
```

Read more [about naming artifacts][artifacts-name].

## Improved documentation

With GitLab Runner 1.1 we've also released improved documentation, explaining
all executors and commands. The documentation also describes what features are
supported by different configurations.

Read the [revised documentation][doc-improved].

## Using Runner on OSX

We also upgraded GitLab Runner 1.1 to be compatible with El Capitan and Xcode 7.3.
You should read the revised [installation guide for OSX][osx-install]
and FAQ section describing the [needed preparation steps][osx-faq].

## Changelog

So far we described the biggest features, but these are not all the changes
introduced with GitLab Runner 1.1. We know that even the smallest change can
make a difference in your workflow, so here is the complete list:

```
- Use Go 1.5
- Add docker-machine based autoscaling for docker executor
- Add support for external cache server
- Add support for `sh`, allowing to run builds on images without the `bash`
- Add support for passing the artifacts between stages
- Add `docker-pull-policy`, it removes the `docker-image-ttl`
- Add `docker-network-mode`
- Add `git` to gitlab-runner:alpine
- Add support for `CapAdd`, `CapDrop` and `Devices` by docker executor
- Add support for passing the name of artifacts archive (`artifacts:name`)
- Refactor: The build trace is now implemented by `network` module
- Refactor: Remove CGO dependency on Windows
- Fix: Create alternative aliases for docker services (uses `-`)
- Fix: VirtualBox port race condition
- Fix: Create cache for all builds, including tags
- Fix: Make the shell executor more verbose when the process cannot be started
- Fix: Pass gitlab-ci.yml variables to build container created by docker executor
- Fix: Don't restore cache if not defined in gitlab-ci.yml
- Fix: always use `json-file` when starting docker containers
```

You can see why we think version 1.1 is fantastic.
Go get it, test it and share your feedback with us!
You can meet with the CI team in our upcoming webcast.

## Live webcast: GitLab CI

Sign up for our webcast on April 14th, which includes an overview and tutorial
about using GitLab CI. Meet people from the GitLab CI team and get your questions
answered live!

- Date: Thursday, April 14, 2016
- Time: 5pm (17:00) UTC; 12pm EST; 9am PST
- [Register here](http://page.gitlab.com/apr-2016-gitlab-intro-ci-webcast.html)

Can't make it? Register anyway, and we'll send you a link to watch it later!

[docker-machine]: https://docs.docker.com/machine/
[docker-machine-driver]: https://docs.docker.com/machine/drivers/
[ce]: https://gitlab.com/gitlab-org/gitlab-ce
[doc-runners]: http://doc.gitlab.com/ce/ci/runners/README.html
[doc-ci]: /gitlab-ci
[doc-autoscale]: https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/configuration/autoscale.md
[doc-improved]: https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/README.md
[doc-cache]: https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/configuration/autoscale.md#distributed-runners-caching
[shared runners]: http://doc.gitlab.com/ce/ci/runners/README.html
[stages]: http://doc.gitlab.com/ce/ci/yaml/README.html#stages
[digitalocean]: https://www.digitalocean.com/
[caching]: http://doc.gitlab.com/ce/ci/yaml/README.html#cache
[jobs]: http://doc.gitlab.com/ce/ci/yaml/README.html#jobs
[dependencies]: http://doc.gitlab.com/ce/ci/yaml/README.html#dependencies
[artifacts-name]: http://doc.gitlab.com/ce/ci/yaml/README.html#artifactsname
[osx-install]: https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/install/osx.md#install-on-osx
[osx-faq]: https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/faq/README.md#12-failed-to-authorize-rights-0x1-with-status-60007
