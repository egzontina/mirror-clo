---
title: "GitLab CI 5.1 released"
date: 2014-10-22 16:54:59 +0300
categories: release
---

Hi everyone!

Today we've released version 5.1 of our continuous integration server GitLab CI.

This version contains many cool, new features.

We've created a new admin page which shows all builds.

In addition, GitLab CI can now parse coverage information from builds and will show this on Merge Requests in GitLab and on the build page.

You don't always want to trigger a CI build with every push. With GitLab CI 5.1, it's now possible to define a list of branches that should be ignored by GitLab CI.

<!--more-->

You can find a more detailed list of changes [here](https://gitlab.com/gitlab-org/gitlab-ci/blob/5-1-stable/CHANGELOG)

## Builds page.

You can now get an overall picture of the runners, which is useful if you have to make decisions on the amount of runners you might need.

[![screenshot](/images/ci_5_1/builds_page.png)](/images/ci_5_1/builds_page.png)

## Coverage parsing.

With Coverage parsing, you will be able to track your test coverage. This feature enables you to determine which change led to a change in coverage, allowing you to take appropriate action.

[![screenshot](/images/ci_5_1/coverage_index.png)](/images/ci_5_1/coverage_index.png)
[![screenshot](/images/ci_5_1/coverage_show.png)](/images/ci_5_1/coverage_show.png)
[![screenshot](/images/ci_5_1/setting_coverage_parsing.png)](/images/ci_5_1/setting_coverage_parsing.png)

## Update process

If you already use GitLab CI you need to follow our [Update guide](https://gitlab.com/gitlab-org/gitlab-ci/blob/master/doc/update/5.0-to-5.1.md) for Coordinator and update all your Runners to version 5.
You can find the Runner update guide [here](https://gitlab.com/gitlab-org/gitlab-ci-runner/blob/master/doc/update-from-v4-to-v5.md). Also check the build scripts of your projects to make sure they are compatible with the new behavior.

## New setup

You can setup a new GitLab CI instance using [installation guide](https://gitlab.com/gitlab-org/gitlab-ci/blob/master/doc/install/installation.md)

## Support

If you are looking for paid support for GitLab CI, please <a href="mailto:sales@gitlab.com">email us</a>.
