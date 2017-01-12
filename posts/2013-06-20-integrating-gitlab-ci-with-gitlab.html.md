---
title: "Integrating GitLab CI with GitLab to enable distributed builds"
date: 2013-06-20 09:27
categories:
community: true
---

### Integrating GitLab CI with GitLab to enable distributed builds

The GitLab.com team strongly believes in using feature branches and merge requests in software development. 
We also think that Test Driven Development (TDD) should be used wherever possible. 
If you combine these things what follows is that you have to know the testing results of a feature branch before accepting the merge request. 
GitLab CI was build to offer this functionality and we think most people using GitLab would benefit from using GitLab CI as well.

To make this easier we have now integrated GitLab CI with GitLab. This tight integration offers three great benefits:

1. You can login to GitLab CI with your GitLab credentials.
2. The GitLab user interface shown the projects you have access to.
3. Setting up a testing environment for a new project no longer takes [8 steps](http://blog.bitnami.com/2013/05/deploy-gitlab-gitlab-ci-in-cloud-with.html) but just one.

<!-- more -->

**Clean separation through the GitLab API**

We still want a clean separation between GitLab and GitLab CI to allow them to develop independently, reduce security risks and keep each code base small.
Therefore, GitLab CI has its own database and uses GitLab's public API to communicate with GitLab. 
GitLab CI does not have access to more code or user information than what is accessible by the users who are logged in to GitLab CI.

**Integrated but flexible**

GitLab CI will be a rack application that you can mount where you want. 
In the future you can install GitLab CI as a rack application on the same server as GitLab. 
But you can also run GitLab CI on another server than GitLab if you would like to do so.

**Don't run tests on the CI server**

Hopefully some of you are now thinking, running tests on the same server that stores my source code? No way! 
Of course you are very correct but actually the problem is larger than that. 
Anybody who can push to a branch that is tested on a CI server can easily own that server. 
So you don't want to have projects with different authorization levels being tested on the same CI server. 
**If you are running tests on the CI server you are doing it wrong!** 
We must admit that we have done this ourselves too. 
But we have also seen it being set up this way by the majority of people that run other CI applications such as [Jenkins](http://jenkins-ci.org/) (even though Jenkins does allow you to [run the tests on other servers](https://wiki.jenkins-ci.org/display/JENKINS/Distributed+builds)).

**Coordinators and runners**

To solve the problem we have split the CI application in two parts, a coordinator and runners. 
The coordinator enables you to specify how you want to test and stores the results. 
This is a rack application that communicates with the GitLab API. 
The runners perform the actual build and they are installed on separate machines. 
This way you never run tests on the same server that stores all you code. 
You can bind runners to specific projects to preserve the exclusivity of your source code.

**Work in progress**

The integration work is still ongoing. Right now GitLab CI is still a standalone application. 
But it does already use runners [build from a separate repo](https://github.com/gitlabhq/gitlab-ci-runner). 
[![screenshot](/images/screens/runner.png)](/images/screens/runner.png)


**Conclusion**

Of course all this is optional, you can still use GitLab with other CI servers or install GitLab without installing GitLab CI. 
But we believe this 'distributed builds by default' design will encourage many people to do the right thing. 
Please let us know what you think about this change.
