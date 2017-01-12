---
title: "Building our web-app on GitLab CI"
author: Pierre de La Morinerie
author_twitter: pmorinerie
categories: GitLab CI
image_title: '/images/blogimages/cross-post-gitlab-ci/building-our-web-app-on-gitlab-ci-cover.jpg'
twitter_image: '/images/tweets/building-our-web-app-on-gitlab-ci.png'
description: "5 reasons why Captain Train migrated from Jenkins to GitLab CI"
date: 2016-07-22 16:00
---

The railway world is a fast-moving environment. To bring you the latest improvements and fixes as quick as possible, Captain Train’s web-app is often updated, sometimes several times per day.

Did you always wonder how we manage building and deploying all of this without a jolt? Then read-on: here is a technical peek into our engineering process.

**Note:** this post tells the customer story of [Captain Train][cap].
{: .note}

<!-- more -->

## From Jenkins to GitLab CI

We used to build our web-app using [Jenkins]. A robust and proven solution—which was polling our repositories every minute, and built the appropriate integration and production branches.

However we recently switched to a new system for building our web-app. To host our source-code and perform merge-requests, we’re using a self-hosted instance of [GitLab]. It’s nice, open-source—and features an integrated build system: [GitLab CI].

See it like Travis, but integrated: just add a custom `.gitlab-ci.yml` file at the root of your repository, and GitLab will automatically start building your app in the way you specified.

Now what’s cool about this?

## Reliable dockerized builds

Jenkins builds were all executed on a resource-constrained server—and this made builds slow and unreliable. For instance, we observed several times PhantomJS crashing randomly during tests: apparently it didn’t like several builds running on the same machine at the same time—and a single PhantomJS process crashing would bring all of the others down.

So the first step of our migration was to insulate builds into Docker containers. In this way:

- **Every build is isolated from the others**, and processes don’t crash each other randomly.
- **Building the same project on different architectures is easy**, and that’s good news, because we need this to support multiple Debian versions.
- Project maintainers have **greater control on the setup of their build environment**: no need to bother an admin when upgrading an SDK on the shared build machine.

## It scales

GitLab CI allows us to add more runners very easily. And now that builds are performed in Docker containers, we don’t have to configure the runners specifically with our build tools: any out-of-the-box server will do.

Once a new runner is declared, **scaling is automatic**: the most available runner will be picked to start every new build. It’s so simple that you can even add your own machine to build locally.

We’ve already reduced our build time by switching to a more powerful runner—a migration that would have been more difficult to do using Jenkins. Although we regularly optimize the run time of our test suite, sometimes you also need to just throw more CPU at it.

## Easier to control

With Jenkins, the configuration of the build job is stored in an external admin-restricted tool. You need the right credentials to edit the build configuration, and it’s not obvious how to do it.

Using GitLab CI, the build jobs are determined solely from the `.gitlab-ci.yml` file in the repository. This makes it really simple to edit, and you get all the niceties of your usual git work-flow: versioning, merge requests, and so on. You don’t need to ask permission to add CI to your project. Lowering the barrier to entry for CI is definitely a good thing for engineering quality and developer happiness.

## Tests on merge requests

GitLab CI makes it really easy to build and test the branch of a **merge request** (or a _“Pull request”_ in GitHub slang). Just a few lines added to our `.gitlab-ci.yml` file, and we were running tests for every push to a merge request.

![Merge automatically when the build succeeds][merge]{: .shadow}

We get nice red-or-green-status, the quite useful _“Merge automatically when the build succeeds”_ button — and, as branches are now tested before being merged, much less build breakage.

![Build Passed][build]{: .shadow}

## A slick UI

GitLab CI provides _“Pipelines”_, an overview of all your build jobs. This points you quickly to a failing build, and the stage where the problem occurs. Plus it gets you this warm and fuzzy feeling of safeness when everything is green.

![Pipelines]{: .shadow}

## In a nutshell

We found the overall experience quite positive. Once the initial hurdle of making the build pass in a Docker container, integrating it into GitLab CI was really easy. And it gave us tons of positive signals, new features and neat integrations. 10/10, would build again.👍

Our Android team also migrated their pipeline, and are now building the integration and production Android APK with GitLab CI.

For further reading, you can find on the official website a nice [overview of GitLab CI features][GitLab CI], and some [examples of `.gitlab-ci.yml` files][CI examples].

_This post was originally [published by Captain Train][cap-post]._

_[Captain Train][cap], the European train ticketing company, makes buying train tickets faster, easier, and ad-free. Their goal is to revolutionize the purchase of train tickets and their doing it by engineering the best user-experience._
{: .note}

<!-- identifiers -->

[build]: /images/blogimages/cross-post-gitlab-ci/build-passed.png
[cap]: https://www.captaintrain.com
[cap-post]: https://blog.captaintrain.com/12703-building-on-gitlab-ci
[Jenkins]: https://jenkins.io/
[GitLab]: https://about.gitlab.com
[GitLab CI]: https://about.gitlab.com/gitlab-ci/
[CI examples]: http://docs.gitlab.com/ce/ci/quick_start/README.html
[merge]: /images/blogimages/cross-post-gitlab-ci/merge-when-build-succeeds.png
[pipelines]:/images/blogimages/cross-post-gitlab-ci/pipelines.png
