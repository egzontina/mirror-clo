---
title: "Getting Started with GitLab and Shippable Continuous Integration"
author: GitLab
author_twitter: gitlab
categories: 
image_title: /images/blogimages/shippable-blog-images/1-aye_aye_gitlab.png
---

_This tutorial is a re-post of [Shippable's blog post](http://blog.shippable.com/getting-started-gitlab-with-shippable-ci)._

GitLab is a fast-growing choice for enterprises managing their application code and team
collaboration both on-premises and in the cloud. Today we are excited to announce Shippable
support for application delivery pipelines for GitLab developers.

Shippable now extends [GitLab](https://about.gitlab.com/)'s combination of Git-based source code repositories and enterprise 
features such as authentication and security with CI/CD pipelines. Shippable connects with 
GitLab self-hosted community and enterprise editions as well as their cloud offering so we 
work the way you want to. 

<!-- more -->

> "We're excited that Shippable now integrates with GitLab. With Shippable anyone using GitLab 
can now easily deploy their code, independent of their stack and cloud environment." says Job van der Voort 
VP of Product at GitLab. "Like GitLab, Shippable works with established technologies, as well as with 
containers, making this an excellent solution for organizations of any size to bring their code from 
their repositories in GitLab to production."

Our new Shippable integration for GitLab supports running builds for your push commits, merge requests 
and even show the build status in GitLab, so you can enjoy the power of Shippable within GitLab. To know 
more about how to setup Shippable CI with GitLab, read on.

---

## Setting up GitLab account integration

To start off, [sign into Shippable](https://app.shippable.com/). (GitLab.com identity support coming soon.)
Once signed into Shippable:

* Click on the gear icon for 'Account Settings' in the top right navigation bar
* Click on the 'Integrations' tab
* Click on 'Add Integration' 

![Add integration in account settings](images/blogimages/shippable-blog-images/2-Add_Integration_in_Account_settings.png)

* Select the drop down under the 'Master Integration' & select 'GitLab'
* For the 'Integration Name', use a distinctive name that's easy to recall
* For 'url', enter the API end-point of your GitLab instance, this is usually of the format [https://your-gitlab.com/api/v3](https://your-gitlab.com/api/v3). If you're using GitLab.com, this will be [https://gitlab.com/api/v3](https://gitlab.com/api/v3). 
* For 'token', navigate to your GitLab Profile Settings in your GitLab instance and copy the Private Token provided under Account.

![Account integration](images/blogimages/shippable-blog-images/3-acc_int.png)

* Click save. 

Next, let's sync the Account to ensure the permissions are up to date. To do this, go to the 'Accounts' 
tab & click 'Sync'.

![Account sync](images/blogimages/shippable-blog-images/4-accountSync.png)

Once synced, your GitLab subscription should be available from the 'Subscriptions' drop down in 
the dashboard page. You can now proceed to enable any repository (project) and configure your
[Continuous Integration](http://docs.shippable.com/ci_configure/).

## Build triggers 

Shippable automatically triggers build runs for all GitLab code commits or merge requests, indepenedent 
of the user who initiated it. Once the build triggers, you can view the [build status and build details](http://docs.shippable.com/ci_builds/). In addition, Shippable integrates with GitLab build status API and displays the build status directly in GitLab as shown below.

![Account sync](images/blogimages/shippable-blog-images/5-example.png)

## Get a build going 

To get a build going for a project, [add the Shippable config](http://docs.shippable.com/ci_configure/) to it and then proceed to enable the project 
from your subscription in Shippable. Any build failures are notified instantly via email, and in Gitlab's 
build status. Slack, and Hipchat, IRC notifications can also be [configured](http://docs.shippable.com/int_notifications/).

You can even proceed to configure [Continuous Delivery](http://docs.shippable.com/pipelines_overview/) using Shippable Pipelines and Docker. With Continuous Integration
ensuring that the features are working fine, and Continuous Delivery automatically deploying the successful builds, 
you can ensure a smooth, fast, bug-less transition from development to production.

---

At GitLab, we are always excited to integrate with products that our customers use. Thanks to the Shippable team 
for writing this blog post and for working with us. 
