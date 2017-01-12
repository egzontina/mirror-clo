---
title: "GitLab CI 5.0 released"
date: 2014-05-06 15:55:40 +0300
categories: release
author: Dmitriy Zaporozhets
---

Hi everyone!

As you know GitLab CI is a continuous integration server.
It integrates with your GitLab installation and runs tests for your projects.

Today we release a new version of GitLab CI.

[![screenshot](/images/ci_5/dash.png)](/images/ci_5/dash.png)

<!--more-->

## Why version 5?

You may know that GitLab CI contains 2 components: Coordinator (a web application) and Runner.
We are releasing a new version of GitLab CI because of important changes to GitLab CI Runner.

Runner is the component that runs your builds. In this release we have changed the way a build is served.
Before this release, each line in the build script was executed in a separate process. That meant that a command such as `cd` or an `ENV` variable was not available on the next line.

With this release, Runner will concatenate all lines in the build script into one file and execute that.
This means that if you change the working directory or environment in one line, it will affect the following lines as well.


[![screenshot](/images/ci_5/edit.png)](/images/ci_5/edit.png)

The former releases had some other problems as well:

* Aborting running tests from the gitlab-ci didn't work (it marked the job as failed, but didn't kill the build)
* The runner didn't properly handle crashing build scripts (it considered the build seemed to continue running endlessly)

With this release, Runner creates a single temporary bash script which contains all the commands the build needs. 
The script itself is then exectued as a child process in its own session (process group) by the runner. 
This way we can ensure that killing the script also kills all its child processes.

__We would like to thank Corin Langosch for contributing these improvements.__

## Webhooks

In order to build some services based on GitLab CI you may need hooks that send data when the build finishes.
GitLab already has such hooks, but up until now, GitLab CI did not.
With GitLab CI version 5, we have added webhook functionality. We thank Võ Anh Duy for help with this feature.

[![screenshot](/images/ci_5/hooks.png)](/images/ci_5/hooks.png)

## Screenshots

We've also changed the colors a bit for a fresher look.
See screenshots below:

[![screenshot](/images/ci_5/project.png)](/images/ci_5/project.png)

[![screenshot](/images/ci_5/build.png)](/images/ci_5/build.png)


## Update process

If you already use GitLab CI you need to follow our [Update guide](https://gitlab.com/gitlab-org/gitlab-ci/blob/master/doc/update/4.3-to-5.0.md) for Coordinator and update all your Runners to version 5.
You can find the Runner update guide [here](https://gitlab.com/gitlab-org/gitlab-ci-runner/blob/master/doc/update-from-v4-to-v5.md). Also check the build scripts of your projects to make sure they are compatible with the new behavior.

## New setup

You can setup new GitLab CI instance using [installation guide](https://gitlab.com/gitlab-org/gitlab-ci/blob/master/doc/install/installation.md)

## Support

If you are looking for paid support for GitLab CI, please <a href="mailto:sales@gitlab.com">email us</a>.
