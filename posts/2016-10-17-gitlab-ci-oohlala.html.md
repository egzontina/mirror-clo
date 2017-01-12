---
title: Why We Chose GitLab CI for our CI/CD Solution
author: James Dang
author_twitter: JamesDangry
categories: GitLab CI
image_title: '/images/blogimages/gitlab-ci-oohlala-cover.png'
description: "Find out why we choose GitLab CI and what we've found through our experience using it."
twitter_image: '/images/tweets/gitlab-ci-oohlala.png'
date: 2016-10-17 03:35
---


At [OOHLALA Mobile][oohlala], our testing and deployment of code is done 
through Fabric, essentially a set of Python scripts (called “fabfiles”) that 
are executed on various servers. Recently, we started looking for a [CI/CD solution][ci-cd] 
that help manage our fabfile deployment system, which is growing 
more complex each day. In the end, we went with [GitLab CI][gitlab-ci], and here’s what we 
found through our experience.

## Simple to Use
Since the bulk of the work is done in Fabric, the CI/CD solution can be very simple, 
as it only needs to be able to execute fabfiles. GitLab CI’s shell executor is perfect 
for this. The complexities of other solutions (e.g. Jenkins) are unnecessary for us.

## Fast

We will be using the system for all code deploys, including development and QA environments, 
so the CI/CD system needs to be fast, to keep up with the fast-paced changes required for 
development. Primarily Docker based solutions, such as CircleCI, took considerably longer 
to run due to the dependency set up stage. With GitLab CI, we can set up our own runner 
with all dependencies pre-installed, and **jobs are executed really fast**.

We would like to have a solution that can be installed on arbitrary hardware, specifically 
our own dedicated macOS and Windows machines that perform our mobile app CI/CD for iOS and 
Android respectively. The reasoning is that in the future we may use the same CI/CD service 
for our mobile teams as well. GitLab CI can do this for free, as we can simply install GitLab 
runners on our dedicated machines. Other CI solutions (e.g. Travis CI, CircleCI etc.) 
do offer mobile CI/CD solutions, but will not meet our requirements since we need our in-house 
build and deploy scripts on dedicated hardware to effectively manage the hundreds of mobile apps that we maintain.

## Economical and Secure 

The solution should be relatively economical, especially since our development team
is still relatively small. Most CI solutions are relatively expensive (e.g. Travis 
CI starts at $129/month minimum), and the ones that have free tiers are very 
limited in capacity (e.g. CircleCI and Shippable both allow only 1 concurrent 
job on their free tier). GitLab CI only costs as much as the machine used to run it, 
which is very flexible (a $40/month DO instance can run many concurrent jobs without issue).

Ideally (i.e. not a hard requirement), we would like to keep all SSH private keys 
within our own infrastructure for better security. With most other CI solutions, 
we would have to hand them the private keys for all the servers we need to deploy to. 
With GitLab CI, the keys are stored on the CI runner instance, which is hosted by us 
and fully under our control.

In the end, we actually chose to host our code on [GitLab.com][gitlab-com], because of the seamless 
integration with GitLab CI. There weren’t any major differences in features 
(at least ones that we wanted) in the repository hosting solutions we looked at 
(GitHub, Gogs, and GitLab mostly), and the CI solution made the choice easier.

## About the author

James Dang is the co-founder the CTO of [OOHLALA Mobile][oohlala], an education technology 
company building the mobile platform for universities and colleges to connect and 
engage with their students. 

<!-- identifiers -->

[ci-cd]: /2016/08/05/continuous-integration-delivery-and-deployment-with-gitlab/
[gitlab-ci]: https://about.gitlab.com/gitlab-ci/
[gitlab-com]: https://gitlab.com/
[oohlala]: https://oohlalamobile.com/
[oohlala-jobs]: https://oohlalamobile.com/jobs/