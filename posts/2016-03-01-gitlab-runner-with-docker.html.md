---
title: "Setting up GitLab Runner For Continuous Integration"
date: 2016-03-01
categories:
author: Ahmet Kizilay
author_twitter: ahmetkizilay

---

There are many cloud-based continuous integration (CI) providers out there and
most of them generously offer free plans for open-source projects.
While this is great for the open-source community, paid plans can get a little
bit too expensive for small start-ups that would prefer to keep their source code private.
In such an ecosystem, GitLab Inc. stands out as a viable option with unlimited private
repositories and its GitLab Runner, a free and open-source tool to automate the
testing and building of projects, thus giving software
developers the freedom to experiment with different approaches to build the
optimal pipeline for their needs.

This tutorial will demonstrate how to get started with a CI workflow using
[GitLab Runner](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner).
We will first setup a sample NodeJS project hosted on Gitlab.com to run tests
on build machines provided by GitLab Inc.
Then, we will setup and configure our own specific runner on a private server.
Finally we will go over some good practices to speed up the build time as the project grows.
By the end of this tutorial you will feel comfortable building your own
CI solution, custom-tailored for your existing projects.
This post will be useful for project managers looking for affordable
CI solutions and developers wanting to build test-driven
and sustainable software projects.

<!-- more -->

### Introducing the sample project

Before we start with the GitLab Runner, let's briefly review this simple
[NodeJS project](https://gitlab.com/gitlab-examples/nodejs/) we will
work with throughout this tutorial.
Our project contains two independent modules we would like to test.
One module consists of some utility methods for asynchronous operations.
The other module implements a simple wrapper around a PostgreSQL database to
insert and retrieve records. Thanks to the latter module, we will need a
database instance in our testing environment to run the tests.

After starting a test database, we can run the tests locally and see all tests pass.

```
DB_USER=[db-username] \
BD_PASS=[db-password] \
DB_HOST=[db-host:db-port] \
node ./specs/start.js
```

Feel free to explore the project [source code](https://gitlab.com/gitlab-examples/nodejs/tree/master)
if you are interested.

### Getting started with GitLab Runner

GitLab Runner is triggered with every push to the central repository if a
`.gitlab-ci.yml` file is present (unless explicitly configured not to).
This file specifies how the build environment should be set up and what
commands to be executed to build, test, and deploy our project in a series of
jobs that can be parallelized. In this tutorial, we will be using GitLab Runner's
built-in **docker executor** to set up the build environment.
This executor provides a powerful abstraction that uses Docker in the
background to load our app and run the tests in a container.
In addition, this executor conveniently starts any dependent services (such as
databases) before running jobs and links containers to communicate with each other.

### Creating `.gitlab-ci.yml` file

We will add our `.gitlab-ci.yml` file to the root directory of our project.

```
image: node:4.2.2

services:
  - postgres:9.5.0

all_tests:
  script:
   - npm install
   - node ./specs/start.js
```

Now let's go over the parts of this file.

The first line specifies the base image against which our tests will run.
Since we are testing a NodeJS app, our base image will be a recent NodeJS version.

The `services` section is where external dependencies are listed.
In our tests, we need a PostgreSQL database, so we add the image name for this database.
Any Docker image name can be specified here, such as `mysql` for MySQL databases.
The database will start with default credentials before tests run and it will be
accessible under the the host name `postgres` on the default PostgreSQL port, 5432.

If we needed to use any credentials other than the defaults, we could add them
inside the `variables` tag. Values under this tag are passed to all services
on initialization. As per the PostgreSQL service [documentation](http://doc.gitlab.com/ce/ci/services/postgres.html),
the following settings will overwrite the user and password for our database:

```
image: node:4.2.2

variables:
  POSTGRES_USER: testuser
  POSTGRES_PASSWORD: testpass

services:
  - postgres:9.5.0

all_tests:
  script:
   - npm install
   - node ./specs/start.js
```

Note that since these test credentials are internal to our project, it is OK to simply
add them to the `.gitlab-ci.yml` file. However, you should register any external
configuration variables, such as API keys, in the **Secure Variables**
page (**Settings -> Variables**) and reference them here by name.

In the final section, we define a job named `all_tests`, which contains the command
that will run our tests.
In the `script` subsection here, we simply add our commands to install the dependencies
and start the tests.

To be extra cautious, we could lint-check our yml file on the
[GitLab CI Lint page](https://gitlab.com/ci/lint) to see the breakdown of
the build steps to make sure we don't have a typo.

### Using Shared Runners

GitLab Inc. provides a number of servers with GitLab Runner installed.
On the **Runners** page (**Settings -> Runners**), we can see the list of currently available runners.
We should see that Shared Runners are already available for us, so we can immediately queue our first build by simply pushing our `.gitlab-ci.yml` file to our repository.
We can track the progress of our build on the [Builds page](https://gitlab.com/gitlab-examples/nodejs/builds).
Once our build starts, we should see that it completes with success in a couple of minutes.

### Installing a specific runner

While these Shared Runners are great to get a sense of how to get started with
CI, we will now install GitLab Runner on a private server to run exclusively
for our project.
We will use exactly the same [open-source software](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner)
GitLab.com uses on their Shared Runners, so we will have the extra benefit of
optimizing and securing our builds for our specific project.


We will need a server instance where we will install the GitLab Runner.
GitLab Runner can be installed on [Linux](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/install/linux-repository.md), [OSX](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/install/osx.md) and [Windows](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/install/windows.md).
For our sample project, a small server instance with 1 GB RAM should be enough.
In addition, since we will be running with the Docker executor, we also need to have [Docker Engine](https://docs.docker.com/engine/installation/) installed.

Upon installation, we will register a new runner for our project.
Start the registration with the following command:

```
gitlab-ci-multi-runner register
```

The registration will walk us through a few steps to configure our runner.

```
Running in system-mode.                            

Please enter the gitlab-ci coordinator URL (e.g. https://gitlab.com/ci):
https://gitlab.com/ci
```

Since our project is hosted on Gitlab.com, we will use the default
gitlab-ci coordinator URL.

```
Please enter the gitlab-ci token for this runner:
[your private gitlab-ci token]
```

On **Runners** page (**Settings -> Runners**), we will copy the private gitlab-ci token for our project and paste it here.

```
Please enter the gitlab-ci description for this runner:
[ubuntu-2gb-nyc3-01]: new-docker-executor
Please enter the gitlab-ci tags for this runner (comma separated):
docker
Registering runner... succeeded                     runner=8tB1zBiU
```

It is a good practice to give a descriptive name and tags for runners to
be able to remember and target them later on. We will add the `docker` tag to this
runner since we can run any Docker image and services with it.

```
Please enter the executor: virtualbox, ssh, shell, parallels, docker, docker-ssh:
docker
Please enter the default Docker image (eg. ruby:2.1):
node:4.2.2
Runner registered successfully. Feel free to start it, but if it's running already the config should be automatically reloaded!
```

Notice that there are several executor options available.
In this post, we are using the `docker` executor.
Remember from the `.gitlab-ci.yml` file, our base image is already set as node:4.2.2.
Note that the default Docker image specified here will be used only when `.gitlab-ci.yml`
file does not contain an image declaration.

Specific runners take precedence over the Shared Runners.
Our project won't be using Shared Runners as long as our specific runner is available.
If preferred, we can disable the Shared Runners on the **Runners** page
(**Settings -> Runners**) by toggling off the Shared Runners button.

Finally, we are ready to trigger a new build.
We should see the next build running with our specific runner on our private server.

### Enabling cache

Now that we have a functional CI workflow, let's talk about
how to make it faster and more efficient.

To start, we can eliminate redundant downloading of dependency libraries by
caching and restoring dependencies between builds.
For NodeJS projects, dependent libraries are installed in a folder called `node_modules`.
We should specify this folder to cache in our `.gitlab-ci.yml` file:

```
image: node:4.2.2

cache:
  paths:
  - node_modules/

services:
  - postgres:9.5.0

all_tests:
  script:
   - npm install
   - node ./specs/start.js
```

After a successful build, you should see the `node_modules` folder is archived at
the end of builds to be restored at the beginning of following builds.
As long as our dependencies file remains unchanged, no new libraries will be
downloaded and our total build time will significantly decrease.

### Adding concurrency

Another modification we can add to speed up the build process is to
parallelize the tests.
In our project, we can split the tests into two jobs.
One for the database tests and another for the async module tests.
Furthermore, we can restrict the PostgreSQL service to run only for our database
job since we won't need a database for the async module.

```
image: node:4.2.2

cache:
  paths:
  - node_modules/

test_async:
  script:
   - npm install
   - node ./specs/start.js ./specs/async.spec.js

test_db:
  services:
    - postgres:9.5.0
  script:
   - npm install
   - node ./specs/start.js ./specs/db-postgres.spec.js
```

Note that we still need to introduce concurrency to the build.
To do that we could either create a new server and register a runner for
our project, or increase the concurrency level for our existing runner.
We will go with the latter and edit the `concurrent` setting on the first
line of our `config.toml` file in the server.
If you installed GitLab Runner as the root user with the deb or rpm packages,
the config file will be in `/etc/gitlab-runner/config.toml` by default:

```
concurrent = 2
```

After triggering a new build, we can see two jobs running
at the same time.

### Conclusion

In this tutorial, we set up automated testing with GitLab Runner for a NodeJS
project to get started with continuous integration on Gitlab.com.
For more information on the GitLab Runner and GitLab CI platform, check out the [documentation](http://doc.gitlab.com/ce/ci/).
Happy coding!

### About Guest Author: Ahmet Kizilay

[Ahmet Kizilay](https://about.me/ahmetkizilay) is a software developer living in Istanbul.
He is currently working as a full-stack developer at [Graph Commons](https://graphcommons.com/).
