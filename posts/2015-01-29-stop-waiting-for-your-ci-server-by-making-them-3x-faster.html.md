---
title: "Stop waiting for your tests by making them 3x faster"
date: 2015-01-29
author: "Sytse Sijbrandij"
image_title: '/images/unsplash/milkyway.jpg'
categories:
---

Are you working on a serious software project?
You probably have an extensive test suite that takes a while to run.
Why not run only the directly related unit tests locally and have your CI server take care of the rest 3x faster than you could?
This way you can start with the next feature while your feature branch is being tested.

Having the tests run 3x faster on the CI server requires adding multiple workers to execute the tests in parallel.
So far this has been very expensive, but with GitLab CI it is affordable for everyone.

<!-- more -->

[![screenshot](/images/ci_5_4/parallel.png)](/images/ci_5_4/parallel.png)


## Price comparison

Right now it is expensive for people to test private repositories quickly.

Most serious projects have a long test suite and you want to run tests in parallel.
You want to be able to test multiple commits at the same time,
so you can merge everything quickly at the end of the sprint.

Suppose you want to have 5 tests in parallel on 2 different commits.
For this you would need 10 runners/workers.

On [Travis](https://travis-ci.com/plans) the plan for 10 concurrent jobs is $489 per month.

On [CircleCI](https://circleci.com/pricing) the cost for 1 free and 9 paid jobs is $450 per month.

As you can easily set up your own workers (Runners) with GitLab CI,
this scale becomes much more affordable:

If you get 10 dedicated [Digital Ocean boxes](https://www.digitalocean.com/pricing/) with 2GB each you would pay 10 * $20 per month = $200 per month.
You save more than 50% and most DO boxes are [faster](http://uncrunched.com/2013/08/07/digital-ocean-v-aws-10x-performance-for-13-cost/) than those at other providers.

## Continuous Integration (CI) hosted for free

At ci.gitlab.com you can run CI completely free except that you need to bring your own test Runners.
This is not a temporary beta, we intend to continue to offer this for free, a world's first as far as we know.

Simply add your projects from GitLab.com to ci.gitlab.com and configure the build script(s).
You can use the parallel build feature of GitLab CI and we'll store the build logs and configuration for you.

To run your tests you need to install GitLab Runner on one or more of your instances.
The CI status will show in merge requests on GitLab.com.

## No instances available? No problem!

Don't have any instances handy to install the runner on? We can help.

**In total, we're giving away up to $520,000.- in cloud hosting for people to host their Runner!**
This is a collaboration with Google Compute Engine and Digital Ocean, we're very grateful for their offer.
Did you know they both also offer one-click-installs of GitLab?
To claim your credit please see the instructions below.

The credit is a limited time offering but the free CI for private projects on ci.gitlab.com is permanent.

## Claim Google Cloud Platform credit

Google Cloud Platform offers $500 in credit for the first 1000 users.
To get started, follow the three steps below:

1. Go to [http://cloud.google.com/startercredit](http://cloud.google.com/startercredit)
1. Click Apply Now
1. Complete the form with code: gitlab

With Cloud Platform you can access application, compute, storage and big data services.
You’re now building on the same infrastructure that powers Google.

## Claim Digital Ocean credit

DigitalOcean offers $40 in credit for the first 500 users.
This is valid only for new DigitalOcean accounts, not for existing users.
The offer is valid for one week and you can claim up to one promo per person.
You need to setup a project on GitLab.com and add it to ci.gitlab.com before you can claim it.

To claim it please fill out [this form](https://docs.google.com/a/gitlab.com/forms/d/1YXTRwDz2C8o4DqNrFCT78UQf_iHnN1Ekrt4p8yv6fd4/viewform) with your name, email or handle and project url.
Once submitted, the GitLab team will email you your unique promo code.
If you have any questions about this promotion, please contact the GitLab support team at support@gitlab.com.

## On your server

If you want to run CI on your own servers that is also possible.
GitLab CI is included if the [GitLab Omnibus packages](https://about.gitlab.com/downloads/)
To enable it just [change a single line](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/gitlab-ci/README.md##getting-started).

## What do you think?

How much time can you save with parallel tests on fast machines?
