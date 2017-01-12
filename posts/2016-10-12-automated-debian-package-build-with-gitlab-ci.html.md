---
title: "Automated Debian Package Build with GitLab CI"
author: Adfinis SyGroup
author_twitter: adfinissygroup
categories: GitLab CI
image_title: '/images/blogimages/automated-debian-package-build-with-gitlab-ci/adfinis-sygroup-cover.png'
description: "Continuous Deployment with GitLab: how to build and deploy a Debian Package with GitLab CI"
twitter_image: '/images/tweets/automated-debian-package-build-with-gitlab-ci.png'
ee_cta: true
---

This post is a customer story by [Adfinis SyGroup][adf].
{:.note}

We've decided to use [GitLab CI][ci] to build Debian packages
automatically. GitLab CI allows users to execute tasks based
on definable events, such as Git tags.

We've created a generic Docker container which contains the base
package-building tools and is used by GitLab to build the package.
Updates can be easily installed in the build environment, since the
Docker container can be simply replaced with a new one.

The following shows the automated packaging of the [GoAccess] log
analysis tool. Many tools are not packaged in their latest version
and thus have to be created manually.

<!-- more -->

## Prepare the Debian Package

First, the files which control the building of the Debian package
are created. In the case of GoAccess, these are:

```shell
debian/changelog # Changes to the package and software  
debian/compat    # Compatibility level for debhelper  
debian/control   # Package-specific information such as dependencies and description  
debian/rules     # Instructions for debhelper 
```

Debian themselves already offer [detailed documentations][debian-doc]
to simplify the introduction to packaging.

## Prepare the Docker Container

On a host system, a container must be prepared in which a package can
then be built. Start by creating a `Dockerfile`:

```dockerfile
FROM debian:wheezy  
ADD  setup.sh /opt/  
RUN  /bin/bash /opt/setup.sh  
```

In the `Dockerfile` ([official documentation][dockerfile-doc]) is indicated
which base image is to be used. In this case, it's Debian Wheezy. After
that, the `setup.sh` script is copied into the `/opt/` directory of the container. 
In `setup.sh`, the mirror which is going to be used is configured, and
the most basic dependencies are installed, which can be used in any build:


```shell
#!/bin/sh

# change to our own mirror
echo "deb http://pkg.adfinis-sygroup.ch/debian/ wheezy main non-free contrib" > /etc/apt/sources.list  
echo "deb http://security.debian.org/ wheezy/updates main" >> /etc/apt/sources.list  
echo "deb http://pkg.adfinis-sygroup.ch/debian/ wheezy-updates main contrib non-free" >> /etc/apt/sources.list

# requirements
apt-get update  
apt-get -y install git dh-make build-essential autoconf autotools-dev  
```

As soon as these files have been prepared, we can build the Docker container:

```shell
docker build -t generic-package-build-runner:v1 
```

The container is now created and ready for use.

## Configure GitLab CI

Now, the prepared Docker container has to be [registered for the
current project][ci-docker-registry], in which a package is to be built:

```shell
gitlab-ci-multi-runner register \
--non-interactive \
--url "$(GITLAB_URL)" \
--registration-token "$(CI_TOKEN)" \
--description "Generic debian wheezy package build runner" \
--executor "docker" \
--docker-image "generic-package-build-runner:v1"
```

The GitLab URL and the CI token can be found in the GitLab
project on the page **Settings** > **Runners**. Each project has its own CI token.

In order for GitLab CI to know which commands in the container
should be executed, [the file `.gitlab-ci.yml`][ci-doc] is created within the repository.

```yaml
# Is performed before the scripts in the stages step
before_script:  
  - source /etc/profile

# Defines stages which are to be executed
stages:  
  - build

# Stage "build"
run-build:  
  stage: build
  script:
    - apt-get install -y libncurses5-dev libglib2.0-dev libgeoip-dev libtokyocabinet-dev zlib1g-dev libncursesw5-dev libbz2-dev
    - autoreconf -fvi
    - cp COPYING debian/copyright
    - dpkg-buildpackage -us -uc
    - mkdir build
    - mv ../goaccess*.deb build/

  # This stage is only executed for new tags
  only:
    - tags

  # The files which are to be made available in GitLab
  artifacts:
    paths:
      - build/*
```

The most important part of this file is the `run-build` stage.
This part defines which actions are executed, when they are
executed and the locations of the files created in the build.

Since a generic Docker container was created, the necessary
dependencies have to be installed in the first step.

After that, the building procedure is prepared with `autoreconf`.
Among other things, this results in the creation of the Makefile,
which is indispensable for the build. Since we're using the copyright
from the package, we'll copy it to `debian/`.

The building process is then started with the command `dpkg-buildpackage`.
The package is compiled and the Debian package is created. These packages
are then moved to the `build` directory that was created and uploaded to GitLab.

## Workflow

As soon as we have a new release, a Git tag is created. This Git tag
starts a new build in GitLab, which builds the package using the latest version.
The package that is created will then be made available in the web
interface of GitLab, where it can be downloaded. 

![Build Debian Package with GitLab CI](/images/blogimages/automated-debian-package-build-with-gitlab-ci/gitlab-ci-build.png){:.shadow}

## Outlook

Ideally, the packages or artifacts built should be processed automatically,
for example by uploading them to a mirror. In our case, we're using a
bot which, when instructed by a [GitLab Webhook][webhooks-doc], downloads the artifacts
onto a target server, adds them to a Aptly repository and publishes the
repository, such that the process can be [fully automated from package
build to publication][gitlab-cd]. The final result can be freely viewed on our Aptly mirror.

----

This post was [originally published][original-post] by [Adfinis SyGroup][adf].
{:.note}

<!-- identifiers -->

[adf]: https://www.adfinis-sygroup.ch/
[ci-doc]: https://docs.gitlab.com/ee/ci/quick_start/README.html
[ci-docker-registry]: https://docs.gitlab.com/ee/ci/docker/using_docker_build.html
[ci]: /gitlab-ci/
[debian-doc]: https://www.debian.org/doc/manuals/maint-guide/index.en.html
[dockerfile-doc]: https://docs.docker.com/engine/tutorials/dockerimages/#/building-an-image-from-a-dockerfile
[gitlab-cd]: /2016/08/05/continuous-integration-delivery-and-deployment-with-gitlab/#continuous-deployment "Continuous Deployment with GitLab"
[GoAccess]: https://goaccess.io/
[original-post]: https://blog.adfinis-sygroup.ch/en/automated-debian-packagebuild-gitlabci/
[webhooks-doc]: https://docs.gitlab.com/ce/web_hooks/web_hooks.html
