---
title: "GitLab Container Registry"
date: 2016-05-23 17:00
author: Mark Pundsack
author_twitter: markpundsack
image_title: /images/containers.jpg
---

Yesterday [we released GitLab 8.8][8.8], super powering GitLab's built-in
continuous integration. With it, you can build a pipeline in GitLab,
visualizing your builds, tests, deploys and any other stage of the life cycle of
your software. Today (and already in GitLab 8.8), we're releasing the next
step: GitLab Container Registry.

GitLab Container Registry is a secure and private registry for Docker images.
Built on [open source software](https://github.com/docker/distribution),
GitLab Container Registry isn't just a standalone registry;
it's _completely_ integrated with GitLab.

GitLab is all about having a single, integrated experience and our registry
is no exception. You can now easily use your images for GitLab CI, create
images specific for tags or branches and much more.

Our container registry is the first Docker registry that is
fully integrated with Git repository management and comes out of the box with
GitLab 8.8. So if you've upgraded, you already have it!
This means our integrated Container Registry requires no additional
installation. It allows for easy upload and download of images
from GitLab CI. And it's free.

Read the [administration documentation][admin-docs] to learn how to enable it
on your GitLab instance.

[8.8]: https://about.gitlab.com/2016/05/22/gitlab-8-8-released/

<!-- more -->

## Docker Basics

The main component of a Docker-based workflow is an image, which contains
everything needed to run an application. Images are often created automatically
as part of continuous integration, so they are updated whenever code changes.
When images are built to be shared between developers and machines, they need to
be stored somewhere, and that's where a container registry comes in.

The registry is the place to store and tag images for later use. Developers may
want to maintain their own registry for private, company images, or for
throw-away images used only in testing. Using GitLab Container Registry means
you don't need to set up and administer yet another service, or use a public
registry.

## Tight Integration

GitLab Container Registry is fully-integrated with GitLab making it easy for
developers to code, test, and deploy Docker container images using GitLab CI
and other Docker-compatible tooling.

- User authentication is from GitLab itself, so all the user and group
  definitions are respected.
- There's no need to create repositories in the registry; the project is already
  defined in GitLab.
- Projects have a new tab, **Container Registry**, which lists all images
  related to the project.
- Every project can have an image repository, but this can be turned off
  per-project.
- Developers can easily upload and download images from GitLab CI.
- There's no need to download or install additional software.

## Simplify your workflow

GitLab Container Registry is seamless and secure.
Here are some examples of how GitLab Container Registry can simplify your
development and deployment workflows:

- Easily build Docker images with the help of GitLab CI and store them in the
  GitLab Container Registry.
- Easily create images per branches, tags, or any other way suitable to your
  workflow, and with little effort, store them on GitLab.
- Use your own build images, stored in your registry to test your applications
  against these images, allowing you to simplify the docker-based workflow.
- Let the team easily contribute to the images, using the same workflow they are
  already accustomed to. With the help of GitLab CI you can automatically
  rebuild images that inherit from yours, allowing you to easily deliver fixes
  and new features to a base image used by your teams.
- Have a full Continuous Deployment and Delivery workflow by pointing your
  CaaS to use images directly from GitLab Container Registry. You'll be able to
  perform automated deployments of your applications to the cloud
  (Docker Cloud, Docker Swarm, Kubernetes and others) when you build and test
  your images.

## Start using it

First, ask your system administrator to enable GitLab Container Registry
following the [administration documentation][admin-docs].

After that, you will be allowed to enable **Container Registry** for your project.

![](/images/container-registry/project_feature.png)

To start using your brand new **Container Registry** you first have to login:

```
docker login registry.example.com
```

Then you can simply build and push images to GitLab:

```
docker build -t registry.example.com/group/project .
docker push registry.example.com/group/project
```

GitLab also offers simple Container Registry management. Go to your project and click **Container Registry**.
This view will show you all tags in your repository and will easily allow you to delete them.

![](/images/container-registry/container_registry.png)

> Read more in the [GitLab Container Registry user guide][user-docs].

## Use with GitLab CI

You can use GitLab's integrated CI solution to build, push, and deploy your
Container Images.

> **Note:** This feature requires GitLab Runner 1.2.

> **Note:**
To use Docker in Docker images you need to have [the `privileged` flag][privflag]
set up in your Runner's configuration. This is **not** the case for the shared
Runners on GitLab.com for now; we plan to enable this flag next week. For the
moment you can use your own Runners.

Here's an example GitLab CI configuration file (`.gitlab-ci.yml`) which builds
an image, runs tests, and if the tests are successful, tags the build and
uploads the build to the container registry:

```yaml
build_image:
  image: docker:git
  services:
  - docker:dind
  script:
    - docker login -u gitlab-ci-token -p $CI_BUILD_TOKEN registry.example.com
    - docker build -t registry.example.com/my-group/my-project .
    - docker run registry.example.com/my-group/my-project /script/to/run/tests
    - docker push registry.example.com/my-group/my-project:latest
  only:
    - master
```

Here's a more elaborate example that splits up the tasks into four stages,
including two tests that run in parallel. The build is stored in the container
registry and used by subsequent stages, downloading the image automatically
when needed. Changes to `master` also get tagged as `latest` and deployed using
an application-specific deploy script:

```yaml
image: docker:git
services:
- docker:dind

stages:
- build
- test
- release
- deploy

variables:
  CONTAINER_TEST_IMAGE: registry.example.com/my-group/my-project:$CI_BUILD_REF_NAME
  CONTAINER_RELEASE_IMAGE: registry.example.com/my-group/my-project:latest

before_script:
  - docker login -u gitlab-ci-token -p $CI_BUILD_TOKEN registry.example.com

build:
  stage: build
  script:
    - docker build -t $CONTAINER_TEST_IMAGE .
    - docker push $CONTAINER_TEST_IMAGE

test1:
  stage: test
  script:
    - docker run $CONTAINER_TEST_IMAGE /script/to/run/tests

test2:
  stage: test
  script:
    - docker run $CONTAINER_TEST_IMAGE /script/to/run/another/test

release-image:
  stage: release
  script:
    - docker pull $CONTAINER_TEST_IMAGE
    - docker tag $CONTAINER_TEST_IMAGE $CONTAINER_RELEASE_IMAGE
    - docker push $CONTAINER_RELEASE_IMAGE
  only:
    - master

deploy:
  stage: deploy
  script:
    - ./deploy.sh
  only:
    - master
```

## Summary

GitLab Container Registry is the latest addition to GitLab's integrated set of
tools for the software development life cycle and comes with
[GitLab 8.8 and up][8.8]. With GitLab Container Registry,
testing and deploying Docker containers has never been easier.
GitLab Container Registry is available on-premises in GitLab CE and GitLab EE
at no additional cost and installs in the same infrastructure as the rest of
your GitLab instance.

Container Registry is enabled on GitLab.com; it's completely free, and you can
start using it right now!

> **Note:**
To use Docker in Docker images you need to have [the `privileged` flag][privflag]
set up in your Runner's configuration. This is **not** the case for the shared
Runners on GitLab.com for now. We plan to enable this flag next week.

[8.8]: https://about.gitlab.com/2016/05/22/gitlab-8-8-released/
[user-docs]: http://docs.gitlab.com/ce/container_registry/README.html
[admin-docs]: http://docs.gitlab.com/ce/administration/container_registry.html
[privflag]: https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/executors/docker.md#use-docker-in-docker-with-privileged-mode
