---
title: "7 reasons why you should be using Continuous Integration"
date: 2015-02-03
image_title: '/images/unsplash/vespa.jpeg'
categories:
author: Patricio Cano
---

When developing software you are usually spoiled for choice. There are many languages you can choose from, different
test suites to try, countless frameworks you can use and many Continuous Integration (CI) offerings.

You can always go with the language you like the most, the test suite you find most practical and choose not to use a
framework, but you should always think about CI.

Continuous Integration is a way to increase code quality without putting an extra burden on the developers.
Tests and checks of your code are handled on a server and automatically reported back to you.

Here are out top 7 reasons why we think you should be using CI and why you should consider it from the beginning of your
project.

<!-- more -->

## 1. Run your tests in the real world

Have you ever had your tests pass on your machine, but fail on someone else's? Well, with CI you can avoid that embarrassment.
Just push your code to your new branch and the CI server will take care of running the tests for you. If everything is
green, you can be sure that you didn't break anything. And if they fail for someone else, you have evidence that they
are wrong.

## 2. Increase your code coverage

Think your tests cover most of your code? Well think again. A CI server can check your code
for test coverage. Now, every time you commit something new without any tests,
you will feel the shame that comes with having your coverage percentage go down because of your changes.

## 3. Deploy your code to production

You can have the CI server automatically deploy your code to production if all the test within a given branch are green.
This is what is formally known as **Continuous Deployment**, or **Oh my God, that was scary, I'm glad my code worked!**
in some circles.

## 4. Build stuff now

All your tests are green and the coverage is good, but you don't handle code that needs to be deployed? No worries! CI
servers can also trigger build and compilation processes that will take care of your needs in no time. No more having to
sit in front of your terminal waiting for the build to finish, only to have it fail at the last second. The CI server will
run this for you within its scripts and notify you as soon as something goes wrong.

## 5. Build stuff faster

With parallel build support, you can split your tests and build processes into different machines, so everything will
finish even faster than if you ran it locally. It will also consume less local power and resources, so you can continue
working on something else while the builds run.

## 6. Don't break stuff

Having your code tested before and after it is merged will allow you to decrease the amount of times your master build
is broken. Don't wait until it's too late, test yo-self, before you brake yo-self.

## 7. Decrease code review time

You can have your CI and Version Control Server communicate with each other and tell you when a merge request is
good to merge. It can also show how the code coverage would be affected by it. This can dramatically reduce the time
it takes to review a merge request.

# GitLab CI

Of course if you are in the market for a CI server, we kindly encourage you to use [GitLab CI](https://about.gitlab.com/gitlab-ci/),
especially because it includes all features we mentioned here and more!

Want to give it a try right now? Grab a [runner package](https://gitlab.com/gitlab-org/omnibus-gitlab-runner/blob/master/doc/install/README.md)
install it on your server and you can have free CI for your private repositories on GitLab.com and [https://ci.gitlab.com/](https://ci.gitlab.com/)
