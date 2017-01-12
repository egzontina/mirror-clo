---
title: "GitLab Partners with DigitalOcean to make Continuous Integration faster, safer, and more affordable"
date: 2016-04-19 13:00
author: Amara Nwaigwe
author_twitter: its_amaracle
categories:
image_title: /images/unsplash/ios-development.jpg
---

Today, we are excited to announce our partnership with DigitalOcean, the world’s simplest
cloud infrastructure provider. Together, GitLab and DigitalOcean want to help developers
eliminate the scaling challenges that come with Continuous Integration (CI), such as speed,
security, and cost. To help alleviate these challenges, GitLab partnered with DigitalOcean to
provide free Runners to all projects on GitLab.com as well as discount codes for GitLab
Community Edition and Enterprise Edition users.

<!-- more -->

![GitLab + DigitalOcean](/images/blogimages/gitlab-do.jpg)

## Eliminating Scaling Challenges with DigitalOcean

At GitLab, we have a new release every month on the 22nd, so we respect the importance of
agile development and timely testing. That is why we [built Continuous Integration](https://about.gitlab.com/gitlab-ci/) directly into
our platform. Our continuous integration allows you to run a number of tests as you prepare to
deploy your software. Naturally, we are heavy users of our own software. We run about 16 tests
in parallel. While the benefits of testing are undeniable, we realized that running several
parallel tests requires a lot of CPU. The need to scale servers up to meet testing demands often
forces developers to sacrifice speed, security, and/or money.

We want to help solve the challenges arising from agile development processes and growing code
bases. “Together with DigitalOcean, we’ve taken the challenges of expensive and slow build
processes head on—changing the way developers approach the build process,” said Sid Sijbrandij,
our CEO and co-founder. “Complementing our collaborative platform, DigitalOcean is uniquely
suited to help us solve these problems as it can spin up new, provisioned servers in
under a minute, an industry record. Developers can have the needed resources simply and
immediately for testing and launching their code.”

To further support the needs of developers, in late March we introduced a new autoscaling
feature to our existing GitLab Runner. GitLab Runner is a hosted application that processes
builds. This new feature, called [GitLab Runner Autoscale](https://about.gitlab.com/2016/03/29/gitlab-runner-1-1-released/), enables you to automatically spin up
new instances (and wind them down) as needed. This dynamic availability makes it faster, safer
and more affordable for you to run your builds in parallel. While instances can be hosted at all
the major cloud providers, DigitalOcean is uniquely suited to support this autoscaling feature.
With the fastest start in the industry, DigitalOcean can make new instances available in under a
minute versus up to eight minutes on a leading cloud platform.

## Benefits to Developers

DigitalOcean has made tremendous strides in supporting the development community with a simple
and scalable cloud computing solution. DigitalOcean’s dedication to simplicity and scale
perfectly aligns with GitLab’s focus on delivering a code collaboration tool that makes it
easier for developers to code, test, and deploy together. Our goal in partnering with
DigitalOcean was to make continuous integration fast, secure, and cost-effective. We hope that
this partnership will offer the following benefits:

* Speed: You no longer have to wait to test your code. Running tests can take multiple hours,
  especially if it’s the end of the sprint and your tests are the last one in the queue.
  Now, you can scale your Runners up to test in parallel.
* Security: Test your code in a controlled and safe environment. After the machine
  runs the test, it’s discarded to ensure security.
* Affordability: Save money by only paying for servers when you use them.

Ben Uretsky, CEO and co-founder of DigitalOcean, is equally excited about the benefits this
partnership brings to developers. “We want to make it easier for teams building and scaling
distributed applications in the cloud,” he said. “This partnership with GitLab enhances the open-
source, collaborative approach to development.”

## Start using GitLab + DigitalOcean Today

If you’re not a GitLab.com customer, simply [create a GitLab.com account](https://gitlab.com/users/sign_in) to get free Runners
for your public and private repositories.

For existing GitLab.com users, great news, [your Runners are powered by DigitalOcean][rundo] and are
completely free.

For GitLab Community Edition users, use the promotional code `GitLab10` to receive a $10
credit*, when creating a new DigitalOcean account.

For GitLab Enterprise Edition users, you'll receive an email with a unique promo for
a $250 credit* to use to host your own Runners on DigitalOcean.

**Note: Promotion code available for new DigitalOcean customers only.*

[rundo]: /2016/04/05/shared-runners/

## Need help setting up your Runners?

For help setting up your GitLab Runners, read the tutorial documentation,
[How to setup GitLab Runner on DigitalOcean](/2016/04/19/how-to-set-up-gitlab-runner-on-digitalocean/).
