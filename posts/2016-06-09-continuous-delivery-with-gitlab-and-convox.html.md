---
layout: post
title: "Continuous Delivery with GitLab and Convox"
date: 2016-06-09
comments: true
categories: technical overview
author: Noah Zoschke
author_twitter: nzoschke
image_title: '/images/unsplash/gitlab-convox-cover.jpg'
---

[Convox](https://convox.com/) is an open-source tool for deploying, managing, and monitoring applications on cloud infrastructure. It increases the productivity of your developers, reduces your infrastructure spend, and ensures that your architecture is resilient, consistent, and compliant.

Recently, Convox launched a native integration with [GitLab](https://about.gitlab.com/) for Continuous Delivery (CD). This tutorial will show you how to use GitLab and Convox together to ship software quickly and reliably.

**Note:** For this tutorial we assume you are familiar with Continuous Deployment (CD) and have a GitLab, [Slack](https://slack.com/) and [Amazon Web Services](https://aws.amazon.com/) (AWS) account. We also assume you are curious about how [Convox](https://convox.com/) utilities make setting up a private, production-ready cloud environment easy.
{: .note}

<!-- more -->

----------

### What's in this page?
{:.no_toc}

- TOC
{: toc}

----

## Continuous Delivery

Continuous Delivery (CD) is a modern software development best practice. Your team wants and needs the ability to safely push updates to production multiple times a day. With a great CD pipeline you can:

* Ship features faster and more frequently
* Roll out bug fixes and security patches instantly
* Keep your development team in a coding flow
* Eliminate work and interruptions on infrastructure that’s not core to your business

If you don’t have CD tools, you may be spending too much precious time and budget on infrastructure, servers and bespoke deployment tools.

See the [Wikipedia article on Continuous Delivery](https://en.wikipedia.org/wiki/Continuous_delivery) for more details about the Continuous Delivery approach.

## CD with GitLab and Convox

The best Continuous Delivery workflow offers a way to `git push` code and automatically deploy it to resilient cloud infrastructure.

Convox and GitLab together represent a modern open-source based Continuous Delivery solution. With both of them your team can:

* **Set up a private deployment cloud in minutes** with `convox install`
* **Create a production-ready application** with `convox apps create`
* **Link GitLab.com or GitLab CE/EE and Slack to your deployment cloud** through the Convox Console
* **Push code to GitLab** with `git push`
* **Let GitLab webhooks or CI automate builds**, tests and deploys of your code to Convox
* **Notify your team via Slack** when the new release is live

This level of automation enables your team to safely release new code as fast as possible, offering an extremely productive workflow for you and your team.

All of this is built on open-source software that you are free to read, modify, and work with the OSS communities to improve.

On top of the open-source projects, both GitLab and Convox offer enterprise-grade options to run this in a totally isolated environment where your code, images and containers never leave your control.

![Continuous Delivery from GitLab to Convox](/images/blogimages/continuous-delivery-with-gitlab-and-convox/gitlab-integration.png)*Continuous Delivery from GitLab to Convox*

![Push Code, Get Service](/images/blogimages/continuous-delivery-with-gitlab-and-convox/slack.png)*Push Code, Get Service*

### Setting up a Convox Deployment Environment

We first need to configure an isolated environment where we will deploy everything. When deploying to AWS, there is a minimum architecture we want for a production-ready environment. Convox makes this simple with the `convox install` and `convox apps create` tools. Click the "Get Started" button on [convox.com](https://convox.com/) to access the web or command line installer.

Convox expertly integrates the following AWS services:

* Virtual Private Cloud spanning 3 availability zones for network isolation
* EC2 and an AutoScale Group (ASG) with at least 3 instances for redundancy
* CloudFormation stacks for safe, automated updates for new AMIs or to scale up instance type and count
* EC2 Container Service (ECS) for container-based zero downtime deploys
* EC2 Container Registry (ECR) for storing build artifacts
* Elastic Load Balancer (ELB) for SSL, websockets and load balancing
* CloudWatch Logs for log tailing, archiving and search

With this consistent, batteries-included cluster setup with the `convox` tools we can now relibly deploy, configure and scale our applications.

You can read the [Getting Started on Convox](https://convox.com/docs/getting-started/) guide for more detailed instructions about setting everything up.

### Granting GitLab and Slack Auth to Convox

Every service integration begins with authorizing two services to talk to each other. For the first iteration of GitLab and Convox, we opted for a simple token-based solution.

![Get your GitLab Private Token](/images/blogimages/continuous-delivery-with-gitlab-and-convox/gitlab-account.png)*Get your GitLab Private Token*

![Give Convox your GitLab Endpoint and Token](/images/blogimages/continuous-delivery-with-gitlab-and-convox/gitlab-setup.png)*Give Convox your GitLab Endpoint and Token*

Convox encrypts this token, and decrypts it when it needs to perform actions on your GitLab instance like creating a webhook and deploy key.

Similarly, you integrate Convox and Slack with an OAuth flow.

Now Convox has access tokens to get and send information to GitLab and Slack.

### Git Push Webhooks

[Webhooks](http://docs.gitlab.com/ce/web_hooks/web_hooks.html) — user-defined HTTP callbacks — are the fabric on which Continuous Deployment systems are built.

GitLab has tremendous webhook support, allowing you to configure how it will make an HTTPS request to an external system on events like every comment, code push and code merge.

When you integrate GitLab with a Convox app, the first thing Convox does is add a new Push Event webhook to your project pointing to a secure and secret Convox URL.

![Tell Convox About the Push](/images/blogimages/continuous-delivery-with-gitlab-and-convox/gitlab-webhooks.png)*Tell Convox About the Push*

When this is configured, Convox will get a notification every time your team pushes new code.

### GitLab Deploy Keys

GitLab has an impeccable security model. If a system like Convox happens to learn the URL for a private repo via a webhook, we still want to control its ability to read or write to this private repo.

To grant Convox limited, read-only access to your private repo, GitLab offers “[Deploy Keys](http://docs.gitlab.com/ce/ssh/README.html#deploy-keys).” These are SSH keys that have read-only access to a repo, guaranteeing that a third-party system can clone code, but can not push any code back.

![Read-only SSH key](/images/blogimages/continuous-delivery-with-gitlab-and-convox/gitlab-deploy-key.png)*Read-only SSH key*

When you integrate GitLab with a Convox app, the next thing Convox does is generate a new SSH keypair, encrypt and save the private key, and set up a new Deploy Key with the public key.

With a webhook and deploy key, Convox can dutifully perform an automatic build and/or deploy.

### Delivering Code to Production

Now that a Convox environment is running and it is authorized to get webhooks and pull code from GitLab, and send notifications to Slack, we can do our first `git push` deploy that rolls out new containers:


```
$ git push gitlab master
Counting objects: 8, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (8/8), done.
Writing objects: 100% (8/8), 758 bytes | 0 bytes/s, done.
Total 8 (delta 7), reused 0 (delta 0)
To https://gitlab.com/nzoschke/httpd.git
   176d4d2..896d06b  master -> master

$ convox builds
ID           STATUS    RELEASE      STARTED         ELAPSED  DESC                                                                          
BCPSBDTVSVB  complete  RQYRSVEXGLD  56 seconds ago  52s      push nzoschke/httpd refs/heads/master 896d06b2a72e702c3c2efe8fae9670bd19f5f255
BSZIBYZFDDU  complete  RVUEQWAOHTN  5 days ago      60s      push nzoschke/httpd refs/heads/master 176d4d22d0631c1223ea7ba31d80f837e4a24390

$ convox builds info BCPSBDTVSVB
RUNNING: git clone --progress git@gitlab.com:nzoschke/httpd.git src
RUNNING: git checkout 896d06b2a72e702c3c2efe8fae9670bd19f5f255
RUNNING: /usr/local/bin/git-restore-mtime .
RUNNING: docker pull httpd
...
cb604ab7d359: Pull complete
Digest: sha256:3eae43b977887f7f660c640ba8477dc1af1626d757ff1a7ddba050418429f2f6
Status: Downloaded newer image for httpd:latest
RUNNING: docker tag -f httpd httpd/web
RUNNING: docker tag -f httpd/web 132866487567.dkr.ecr.us-east-1.amazonaws.com/convox-httpd-owdnefujkr:web.BCPSBDTVSVB
RUNNING: docker push 132866487567.dkr.ecr.us-east-1.amazonaws.com/convox-httpd-owdnefujkr:web.BCPSBDTVSVB
The push refers to a repository [132866487567.dkr.ecr.us-east-1.amazonaws.com/convox-httpd-owdnefujkr] (len: 1)
...
web.BCPSBDTVSVB: digest: sha256:943ca8f7dbbbfa99f761fae8f8f8d57fa99b6ac7b939ce787ec33735ec68edcb size: 23914

$ convox releases
ID           CREATED       STATUS
RQYRSVEXGLD  1 minute ago  active
RVUEQWAOHTN  5 days ago    active

$ convox ps 
ID            NAME  RELEASE      SIZE  STARTED         COMMAND         
1bac0db9b7b5  web   RQYRSVEXGLD  256   25 seconds ago  httpd-foreground
47542b8458a8  web   RVUEQWAOHTN  256   5 days ago      httpd-foreground
d29eb239fda9  web   RQYRSVEXGLD  256   25 seconds ago  httpd-foreground
ef1d2825f528  web   RVUEQWAOHTN  256   1 day ago       httpd-foreground
```

You can see that release `RQYRSVEXGLD` is rolling out and replacing an older release `RVUEQWAOHTN`. In a few more seconds the new code will be up and running. The build and zero-downtime deploy is fully automated by Convox and GitLab.

The final icing on the cake is that your whole team is notified about the new release on Slack:

![Push Code, Get Service](/images/blogimages/continuous-delivery-with-gitlab-and-convox/slack.png)*Push Code, Get Service*

### Automated Testing

I'm sure you noticed that we went directly from a code push to production. This demonstrates all the heavy lifting, and may be suitable for QA or staging workflows, but for anything going out to production we almost certainly want to run some tests too.

This is possible to set up with a few changes. [GitLab CI](https://about.gitlab.com/gitlab-ci/) is an excellent tool and service for automating tests. 

You can tell GitLab to deploy to Convox by setting `CONVOX_PASSWORD` as a User-defined variable, then adding a `.gitlab-ci.yml` file similar to:

```yaml
test:
  script:
  - make test

production:
  type: deploy
  script:
  - curl -Ls https://install.convox.com/linux.zip > convox.zip
  - unzip convox.zip
  - convox login
  - convox switch org/rack
  - convox deploy --app app
  only:
  - tags
```

See the [CI Variables](http://docs.gitlab.com/ce/ci/variables/README.html) doc and [GitLab CI Examples](http://docs.gitlab.com/ce/ci/examples/README.html) doc for more information.

## Open Source Evolution

Both GitLab and Convox are always working hard to improve APIs, integrations and tools for automating continuous delivery as open-source projects.

We encourage you to participate in the open-source projects future enhancements in this space such as a more formal [GitLab Deploy](https://gitlab.com/gitlab-org/gitlab-ce/issues/3286#note_4141009) enhancement and the [Convox Build / Deploy / Release Pipeline](https://github.com/convox/rack/milestones/Build%20/%20Deploy%20/%20Release%20Pipeline) milestone.

## Conclusion

As you can tell, there are a lot of details to coordinate between your team pushing code and delivering it as a production service in the cloud.

GitLab and Convox understand how important Continuous Delivery is and have gone to great lengths to make this process available to everyone with free and open-source software.

## About guest author Noah Zoschke

[Noah](https://medium.com/@nzoschke) is CTO at Convox. Previously he was Platform Architect at Heroku. He believes that the cloud should be easy to use, secure, reliable and cost effective for teams and systems of all sizes. He believes that simple, open-source tools will unlock this true utility of the cloud.
