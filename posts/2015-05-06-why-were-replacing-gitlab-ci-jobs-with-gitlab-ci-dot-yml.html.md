---
title: "Why we're replacing GitLab CI jobs with .gitlab-ci.yml"
date: 2015-05-06
author: Job van der Voort
author_twitter: Jobvo
image_title: '/images/stock/ci-yml.jpg'
---

In case you didn't know yet: Every single GitLab installation
ships with a powerful continuous integration tool: GitLab CI.
Read how to [enable it in 2 minutes](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/gitlab-ci/README.md#getting-started).
With GitLab CI you can run tests of your projects and triggers
builds and deployments easily,
as it integrates deeply with GitLab.

Up until now, to set up the build / deploy commands you had to
go into GitLab CI and edit the scripts in a form. This made
it very low-threshold to setup, but it felt lacking.

We're glad to tell you we'll get a better solution built on the principles and libraries of [Travis CI](https://www.travis-ci.org):
`.gitlab-ci.yml`.

<!--more-->

Instead of editing a form, in the future you will be able to
add a `.gitlab-ci.yml` file to your repository in which you
can specify your builds for GitLab CI.
This has some major (positive) repercussions for GitLab CI
builds:

#### 1. Version controlled

Currently, the script is just a single field in a form:
![current setup of scripts](/images/ci-yml/jobs_old.png)

This means you get none of the advantages of git: no version control.
By moving this into the repository you get all the power of git and GitLab.

#### 2. Builds for older versions

Having the job script live outside of the repository means that it will be the
same for every commit. That means that any change to the script will influence
the build for any commit, even if you are working on older branches / commits
that could be incompatible with the new build script.

By putting the build in the repository, your older commits can still be tested
by an older version of the build script, while newer work can safely make changes
to the build.

#### 3. Build Forks

Forking a project with the latest version of GitLab CI will also copy the contents
of the jobs settings, making it possible to build tests with your fork.
However, this only works if the project and fork have the same owner and able
to use the same runners.

With the script in the repository this makes this process a lot more transparent.
On top of that, a fork can easily add dependencies to its `.gitlab-ci.yml` file.

#### 4. Different builds for different branches

At the moment you can't easily run different scripts for different branches.

By moving the script to the repository this opens up a whole new world of
specific builds for certain branches. For instance, you could setup your
time-intense integration tests to only run on pushes to your `production` branch
- and on success, deploy your code immediately.

#### 5. Single Source of Truth

Currently, only people with `master` access or higher to the project in GitLab
are able to view and edit the `job settings` in GitLab CI. That makes it hard
to see what is happening for all other developers.

With a single file in the repository, everyone with read access can see the contents,
making it much more inviting to improve and review the build scripts.

#### 6. Build matrices

Currently you can define multiple jobs, but you have to define each one yourself.

If you have multiple versions of the programming language, multiple environments and
multiple lists of dependencies, you end up making a job for each.

With `.gitlab-ci.yml` you will be able to run _build matrices_, where these jobs are
generated for you. If you define each of the dimensions, the combinations
will be generated. This makes it easier to set up complex
test suites that require this.

### Current jobs

Your current job can be run by putting your
`job.sh` in the root of the repo and referencing that in your
.gitlab-ci.yml: `script:./job.sh`.

## Where we got our inspiration

The awesome [Travis CI](https://travis-ci.org/) had the great
idea to use a `.yml` file for builds and was followed
by the popular [CircleCI](https://circleci.com). We're happy
to follow this approach, which we believe is superior than
any other. Jenkins jobs, for instance, do not solve the problems mentioned
in the introduction.

As usual, our amazing community was already fully aware of this
and we've seen demand for this on our [feedback page](http://feedback.gitlab.com/forums/176466-general/suggestions/5591851-store-build-configuration-in-the-repo-like-travi)
and even [implementations](https://github.com/claudyus/ci-yml) for this!

We'll be using some of the great [Travis CI projects](https://github.com/travis-ci/travis-ci) that are freely available to build this.

## Ships with GitLab 8.0

This change will deprecate the existing jobs, as we want to keep
GitLab CI simple to use and develop for.
Multiple ways of doing things is
confusing for new users, it makes documentation much harder and complicates
development and debugging.

That means it is also a breaking change for anyone using
GitLab CI. For this reason we will only introduce this
change with GitLab 8.0.

We're not sure yet after which minor version we'll release GitLab 8.0 (7.11, 7.12 or later).

Follow the progress in the [GitLab CI repository](https://gitlab.com/gitlab-org/gitlab-ci).
