---
title: "Building an Elixir Release into a Docker image using GitLab CI - Part 1"
author: Alexander Malaev
author_twitter: spscream
categories: GitLab CI
image_title: '/images/containers.jpg'
description: "Deploying projects written in Elixir/Erlang to production with Docker Containers and GitLab CI!"
twitter_image: '/images/tweets/building-an-elixir-release-into-docker-image-using-gitlab-ci-part-1.png'
---

**Note:** this post is a customer story by Alexander Malaev, a software developer.
{: .note}

Well, we are actively using Phoenix/Elixir in our projects for backend development, we also have a RoR project as a frontend-service for our Admin UI. Our project consists of a bunch of microservices written in Elixir/Erlang, and we are running it in production with Docker-containers linked together and composed by Docker-compose.

On every push to a project's branch on [GitLab], [GitLab CI] runs tests, style checking, and other tasks. These tasks are configured using `.gitlab-ci.yml`. On every merge to `master` GitLab builds a release image for us and uploads it to [GitLab Container Registry][registry]. After all, we run `docker-compose pull && docker-compose up -d` on the servers to download the latest release images and upgrade our containers.

<!-- more -->

## CI pipeline

So, in the following I will describe our release pipeline for Elixir services, using snippets from our project’s `.gitlab-ci.yml`.

We are using `docker:latest` image for our Runner, and several stages:

```yaml
image: docker:latest
stages:
  - build
  - styles
  - test
  - release
  - cleanup
```

Passing some variables:

```yaml
variables:
  APP_NAME: project
  APP_VERSION: 0.0.1
  CONTAINER_RELEASE_IMAGE: gitlab.example.org/example/project:latest
  POSTGRES_HOST: postgres
  POSTGRES_USER: postgres
  POSTGRES_PASSWORD: password
```

These variables are used during the release's build, so they will be available for all the stages. E.g., `CONTAINER_RELEASE_IMAGE` is used on the release stage, as a link to push the release image to. The `POSTGRES_*` variables are used to configure postgres service, and to connect later from containers.

Our build stage:

```yaml
build:
  before_script:
    - docker build -f Dockerfile.build -t ci-project-build-$CI_PROJECT_ID:$CI_BUILD_REF .
    - docker create
      -v /build/deps
      -v /build/_build
      -v /build/rel
      -v /root/.cache/rebar3/
      --name build_data_$CI_PROJECT_ID_$CI_BUILD_REF busybox /bin/true
  tags:
    - docker
  stage: build
  script:
    - docker run --volumes-from build_data_$CI_PROJECT_ID_$CI_BUILD_REF --rm -t ci-project-build-$CI_PROJECT_ID:$CI_BUILD_REF
```

Before running this stage, we create a container which provides volumes for building artifacts. By the way, GitLab CI has a cache volume itself for similar purposes, but I couldn’t make it working correctly with GitLab Runner using Docker image.

```yaml
test:
  services:
    - postgres
  tags:
    - docker
  stage: test
  script:
    - env
    - docker run --rm
      --link $POSTGRES_NAME:postgres
      -e POSTGRES_HOST=$POSTGRES_HOST
      -e POSTGRES_PASSWORD=$POSTGRES_PASSWORD
      -e POSTGRES_USER=$POSTGRES_USER
      -e MIX_ENV=$MIX_ENV
      --volumes-from build_data_$CI_PROJECT_ID_$CI_BUILD_REF ci-project-build-$CI_PROJECT_ID:$CI_BUILD_REF sh -c "mix ecto.setup && mix test"
```

Notice that we must pass the variables and link postgres manually, since GitLab Runner is passing the variables only to the first level of Docker, but we go deeply ;)

We could link as many services as we want. For example, we are using Kafka for production, and on our test stage we make Kafka service available for running tests.

Style checking:

```yaml
styles:
  tags: 
    - docker
  stage: styles
  script:
    - docker run --rm
      --volumes-from build_data_$CI_PROJECT_ID_$CI_BUILD_REF ci-project-build-$CI_PROJECT_ID:$CI_BUILD_REF sh -c "mix credo --strict"
```

Release task; we run it only on pushes to `master`:

```yaml 
release:
  tags:
    - docker
  stage: release
  script:
    - docker run
      --volumes-from build_data_$CI_PROJECT_ID_$CI_BUILD_REF
      -e MIX_ENV=prod --rm -t ci-project-build-$CI_PROJECT_ID:$CI_BUILD_REF
      sh -c "mix deps.get && mix compile && mix release"
    - docker cp build_data_$CI_PROJECT_ID_$CI_BUILD_REF:/build/rel/$APP_NAME/releases/$APP_VERSION/$APP_NAME.tar.gz .
    - docker build -t $CONTAINER_RELEASE_IMAGE .
    - docker login -u gitlab-ci-token -p $CI_BUILD_TOKEN gitlab.example.org:4567
    - docker push $CONTAINER_RELEASE_IMAGE
  only:
    - master
```

We are using Conform to achieve runtime configuration of the release using environment variables. I use the approach described on this [blog post][post-env].

Task to cleanup things:

```yaml
cleanup_job:
  tags:
    - docker
  stage: cleanup
  script:
    - docker rm -v build_data_$CI_PROJECT_ID_$CI_BUILD_REF
    - docker rmi ci-project-build-$CI_PROJECT_ID:$CI_BUILD_REF
  when: always
```

It removes the container with volumes created for build artifacts, and removes the image used during the pipeline. This task is running every time, despite the results of any previous tasks.

Below are our Dockerfiles:

`Dockerfile.build`:

```dockerfile
FROM msaraiva/elixir-gcc
RUN apk add postgresql-client erlang-xmerl erlang-tools --no-cache
WORKDIR /build
ADD . /build
CMD mix deps.get
```

This image is used to create a container for running tests and style checks.

`Dockerfile`:

```dockerfile
FROM alpine:edge
RUN apk — update add postgresql-client erlang erlang-sasl erlang-crypto erlang-syntax-tools && rm -rf /var/cache/apk/*
ENV APP_NAME project
ENV PORT 4000
RUN mkdir -p /app
COPY $APP_NAME.tar.gz /app/
WORKDIR /app
RUN tar -zxvf $APP_NAME.tar.gz
EXPOSE $PORT
CMD trap exit TERM; /app/bin/$APP_NAME foreground & wait
```

This Dockerfile is used to build an actual image with the Elixir release.

## Existing problems

- Now we don’t use the "Erlang hot upgrade" feature;
- We don’t test if the release is correctly starting, now we are testing it manually and locally;
- Every container uses its own "epmd" and intercommunication between the services, now made using REST apis, but I’m working on integration of [Erlang-In-Docker approach][approach] to use native erlang messaging between services.

## What’s next?

I have a plan to write and publish several articles about our release pipeline, to answer the following questions:

- How do we compile and publish assets?
- How do we run our database migrations, since mix tasks aren’t available from the release image?
- What problems are we facing during the implementation of this pipeline, and what solutions have we found.

Thanks for reading!

----

This article was [originally published][post] by Alexander Malaev himself.
{: .note}


[approach]: https://github.com/Random-Liu/Erlang-In-Docker
[post]: https://medium.com/@spscream/building-an-elixir-release-into-docker-image-using-gitlab-ci-part-1-790edca45ac1#.uq1fwin6r
[post-env]: http://carlo-colombo.github.io/2016/05/04/The-3-E-Elixir-Exrm-and-Environment-Variables/

<!-- new links -->

[gitlab ci]: /gitlab-ci/
[gitlab]: /
[registry]: /2016/05/23/gitlab-container-registry/
[runner]: https://gitlab.com/gitlab-org/gitlab-ci-multi-runner