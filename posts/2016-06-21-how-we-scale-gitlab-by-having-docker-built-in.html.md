---
layout: post
title: "How we scale GitLab by having Docker built in"
date: 2016-06-21
author: DJ Mountney
author_twitter: twk3
categories: technical overview, integrations
image_title: '/images/blogimages/scale-GitLab-Docker-built-in-cover.png'
---

Our [Docker image](http://docs.gitlab.com/omnibus/docker/) is a great way to
quickly bring up an instance of GitLab. You can use it to try new features, or
mount the storage volumes and use it for all your GitLab needs.

It has been over two years since we started thinking about [Docker and GitLab together](https://gitlab.com/gitlab-org/omnibus-gitlab/issues/59).
In those years we have pushed over 100 CE and EE docker images to [Docker Hub](https://hub.docker.com/u/gitlab/),
and have built new features like GitLab CI with [built-in Docker support](http://docs.gitlab.com/ce/ci/docker/using_docker_images.html),
helping us (and you!) to test and build our applications easier and faster.

Read on for more details on how we scale GitLab by having Docker built in.

<!-- more -->

## Why Docker?

[Docker](https://www.docker.com/) provides a set of tools for running processes
in a virtualized container. This satisfies most of the same use-cases as a
virtual machine, but re-uses the host system's kernel, making it faster to boot
up. It uses a layered filesystem which can be re-used among several containers,
allowing it to take up less space.

[Docker Hub](https://hub.docker.com/) provides a central registry of images,
which helps make our GitLab image more discoverable. Docker's popularity has
resulted in increased development in virtual containers, and now has a large
community around it to provide support.

For the GitLab application image, we use Docker because it is the most familiar
container provider for our users, and is well supported.

For use within GitLab CI, we chose it because it is easy to manage and its
lightweight nature makes it easy to scale our CI tasks.

## Docker built right into GitLab

### A GitLab CI Docker executor

[GitLab CI](/gitlab-ci) is our continuous integration feature, built right into
GitLab. It allows us to run several tasks against our code as we develop
and deploy our applications. These tasks are run by something called a [Runner](http://doc.gitlab.com/ce/ci/runners/README.html)
which processes builds.

In 2015 the community created a Runner which supported running tasks using a
Docker executor. This soon became our [officially supported Runner](https://about.gitlab.com/2015/05/03/unofficial-runner-becomes-official/).
It runs tasks concurrently, which was a big win.

This new Runner was built with Docker support right from the beginning because
Docker provides an easy way for us to run each task in a fresh clean environment,
without any leftovers from previous builds. It also takes care of downloading and
installing our build dependencies for us. Because of this, using the Docker
executor in GitLab CI is our _recommended_ approach for running most tasks.

### GitLab CI autoscaling with Docker Machine

The GitLab CI Runners also support autoscaling, which allows us to provision and
manage multiple remote Docker hosts. We built autoscaling with the help of [Docker Machine](https://docs.docker.com/machine/).
Docker Machine supports a vast number of [virtualization and cloud providers](https://docs.docker.com/machine/drivers/).

Because the Runners will autoscale, our infrastructure contains only as many
build instances as necessary. The autoscaling feature promotes heavy
parallelization of our tests, so they run quickly. The machines we don't
need are shut down, so we only need to pay for what we are using.

Check out our [autoscale runners release blog post](https://about.gitlab.com/2016/03/29/gitlab-runner-1-1-released/#autoscaling-increases-developer-happiness)
for more information on how we've found autoscaling to increase developer
happiness.

### An integrated Docker Registry

[GitLab Container Registry](http://docs.gitlab.com/ce/administration/container_registry.html)
is a secure and private registry for Docker images. Built on [open source software](https://github.com/docker/distribution),
GitLab Container Registry isn't just a standalone registry; it's _completely_
integrated with GitLab.

The registry is the place to store and tag images for later use. Developers may
want to maintain their own registry for private, company images, or for
throw-away images used only in testing. Using GitLab Container Registry means
you don't need to set up and administer yet another service, or use a public
registry.

Check out our [announcement blog post](https://about.gitlab.com/2016/05/23/gitlab-container-registry/)
for more details on how the GitLab Container Registry simplify your development
and deployment workflows.

## How we continue to scale using Docker

### Scaling our Tests

All of our source branches for GitLab are [tested](https://gitlab.com/gitlab-org/gitlab-ce/pipelines)
using GitLab CI. We switched our builds to use the autoscaled Docker executor when
we released support for it in GitLab CI back in March.

Before switching to the autoscaled runners, tests were on average waiting for **10
minutes** before an executor became available for them to run. Now the tests only
ever need to wait a **few seconds** for a new Docker Machine to be brought up.

It is not just our own tests though. We have [enabled autoscaling on our Shared Runners
on GitLab.com](https://about.gitlab.com/2016/04/05/shared-runners/) for all
your projects on GitLab.com. And you run a lot of builds! On average, we have
been running **94** autoscaled instances. We've seen the number currently running
jump up to a couple hundred at times. It's those peak times when you would have
been waiting several minutes for their builds to start. Now it's only seconds!

### Scaling our Builds

This month we have moved the building of our GitLab Omnibus Packages into Docker
as well. Previously we were running a single dedicated VM for all 9 of the
Operating Systems that we build GitLab packages for. Most package builds took
about half-an-hour, but because there was only one VM for each OS, doing a
[security patch across 7 releases](https://about.gitlab.com/2016/06/15/gitlab-8-dot-8-dot-5-released/)
would take a long time.

Moving the builds to Docker and turning on auto-scaling allows us to run as many
builds at a time as we need. We are not finished with the move quite yet, our
Docker builds are currently half the speed of our previous system, taking a full
hour per build. And flaky build failures often cause us to retry the builds at
least once per release. We still need to reintroduce some build caching and
other improvements to fix these problems, but we expect to be able to quickly and
concurrently build our packages when it is all done. Feel free to
[track our progress](https://gitlab.com/gitlab-org/omnibus-gitlab/issues/1232).

## We <i class="fa fa-heart" style="color:rgb(107,79,187); font-size:.85em" aria-hidden="true"></i> Docker
{: #we-love-docker}

As you can see, providing a GitLab Docker image was just the beginning of our
Docker obsession. Building Docker directly into GitLab CI, and adding a deeply
integrated Docker Registry into GitLab, is helping us to build and test GitLab
quicker and more often. We hope it's helping you too!
