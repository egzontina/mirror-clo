---
title: "GitLab CI: Deployment & Environments"
description: "GitLab CI: Learn how to set up deployment pipeline to multiple environments"
categories: GitLab CI
author: Ivan Nemytchenko
author_twitter: inemation
image_title: '/images/blogimages/ci-deployment-and-environments/intro.jpg'
---

## GitLab CI: Deployment & Environments

This post is a success story of one imaginary news portal, and you're the happy
owner, the editor, and the only developer. Luckily, you already host your project
code on GitLab.com and know that you can
[run tests with GitLab CI](https://about.gitlab.com/2016/07/29/the-basics-of-gitlab-ci/#run-our-first-test-inside-ci).
Now you’re curious if it can be used for deployment, and how far can you go with it.

To keep our story technology stack-agnostic, let's assume that the app is just a
set of HTML files. No server-side code, no fancy JS assets compilation.

Destination platform is also simplistic - we will use [Amazon S3](https://aws.amazon.com/s3/).

The goal of the article is not to give you a bunch of copypasteable snippets.
The goal is to show principles and features of GitLab CI so that you could easily apply them to your technology stack.
{: .alert .alert-warning}

Let’s start from the beginning: no CI in our story yet.

<!-- more -->

## A Starting Point

**Deployment**: in your case, it means that a bunch of HTML files should appear on your
S3 bucket (which is already configured for
[static website hosting](http://docs.aws.amazon.com/AmazonS3/latest/dev/HowDoIWebsiteConfiguration.html?shortFooter=true)).

There're a million ways to do it. We’ll use the
[awscli](http://docs.aws.amazon.com/cli/latest/reference/s3/cp.html#examples) library,
provided by Amazon.

The full command looks like this:

```shell
aws s3 cp ./ s3://yourbucket/ --recursive --exclude "*" --include "*.html"
```

![Manual deployment](/images/blogimages/ci-deployment-and-environments/13.jpg){: .illustration}*<small>Pushing code to repository & deploing are separate processes</small>*

**Important detail**: the command
[expects you](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html#config-settings-and-precedence)
to provide `AWS_ACCESS_KEY_ID` and  `AWS_SECRET_ACCESS_KEY` environment
variables. Also you might need to specify `AWS_DEFAULT_REGION`.
{: .alert .alert-info}

Let’s try to automate it using GitLab CI.

## First Automated Deployment

With GitLab, there's no difference on what commands to run.
You can setup GitLab CI according to your needs as if it was your local terminal on your computer. As long as you execute commands there, you can tell
CI to do the same for you in GitLab.
Put your script to `.gitlab-ci.yml` and push your code - that’s it: CI triggers
a _job_ and your commands are executed.


Let's add some context to our story: our website is small, there is 20-30 daily
visitors and the code repository has only one branch: `master`.

Let's start by specifying a _job_ with the command from above in `.gitlab-ci.yml`:

```yaml
deploy:
  script: aws s3 cp ./ s3://yourbucket/ --recursive --exclude "*" --include "*.html"
```

No luck:
![Failed command](/images/blogimages/ci-deployment-and-environments/fail1.png){: .shadow}

It is our _job_ to ensure that there is an `aws` executable.
To install `awscli` we need `pip`, which is a tool for Python packages installation.
Let's specify Docker image with preinstalled Python, which should contain `pip` as well:

```yaml
deploy:
  image: python:latest
  script:
  - pip install awscli
  - aws s3 cp ./ s3://yourbucket/ --recursive --exclude "*" --include "*.html"
```

![Automated deployment](/images/blogimages/ci-deployment-and-environments/14.jpg){: .illustration}*<small>You push your code to GitLab, and it is automatically deployed by CI</small>*

The installation of `awscli` extends the job execution time, but it is not a big
deal for now. If you need to speed up the process, you can always [look for
a Docker image](https://hub.docker.com/explore/) with preinstalled `awscli`,
or create an image by yourself.
{: .alert .alert-warning}

Also, let’s not forget about these environment variables, which you've just grabbed
from [AWS Console](https://console.aws.amazon.com/):

```yaml
variables:
  AWS_ACCESS_KEY_ID: "AKIAIOSFODNN7EXAMPLE"
  AWS_SECRET_ACCESS_KEY: “wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY”
deploy:
  image: python:latest
  script:
  - pip install awscli
  - aws s3 cp ./ s3://yourbucket/ --recursive --exclude "*" --include "*.html"
```

It should work, however keeping secret keys open, even in a private repository,
is not a good idea. Let's see how to deal with it.


### Keeping Secret Things Secret

GitLab has a special place for secret variables: **Settings > Variables**

![Picture of Variables page](/images/blogimages/ci-deployment-and-environments/variables.png){: .shadow}

Whatever you put there will be turned into **environment variables**.
Only an administrator of a project has access to this section.

We could remove `variables` section from our CI configuration. However, let’s use it for another purpose.


### Specifying and Using Non-secret Variables

When your configuration gets bigger, it is convenient to keep some of the
parameters as variables at the beginning of your configuration. Especially if you
use them in multiple places. Although it is not the case in our situation yet,
let's set the S3 bucket name as a [**variable**](http://docs.gitlab.com/ee/ci/variables/README.html), for demonstration purposes:

```yaml
variables:
  S3_BUCKET_NAME: "yourbucket"
deploy:
  image: python:latest
  script:
  - pip install awscli
  - aws s3 cp ./ s3://$S3_BUCKET_NAME/ --recursive --exclude "*" --include "*.html"
```

So far so good:

![Successful build](/images/blogimages/ci-deployment-and-environments/build.png){: .shadow}

Because the audience of your website grew, you've hired a developer to help you.
Now you have a team. Let's see how teamwork changes the workflow.


## Dealing with Teamwork

Now there’s two of you working in the same repository. It is no longer convenient
to use the `master` branch for development. You decide to use separate branches
for both new features and new articles and merge them into `master` when they are ready.

The problem is that your current CI config doesn’t care about branches at all.
Whenever you push anything to GitLab, it will be deployed to S3.

Preventing it is straightforward. Just add `only: master` to your `deploy` job.

![Automated deployment of master branch](/images/blogimages/ci-deployment-and-environments/15.jpg){: .illustration}*<small>You don't want to deploy every branch to the production website</small>*


But it would also be nice to preview your changes from feature-branches somehow.


### Setting Up a Separate Place for Testing

Patrick (the guy you recently hired) reminds you that there is such a thing called
[GitLab Pages](http://pages.gitlab.io). It looks like a perfect candidate for
a place to preview your work in progress.

To [host websites on GitLab Pages](https://about.gitlab.com/2016/04/07/gitlab-pages-setup/) your CI configuration should satisfy these simple rules:

- The _job_ should be named `pages`
- There should be an `artifacts` section with folder `public` in it
- Everything you want to host should be in this `public` folder

The contents of the public folder will be hosted at `http://<username>.gitlab.io/<projectname>/`
{: .alert .alert-info}

After applying the [example config for plain-html websites](https://gitlab.com/pages/plain-html/blob/master/.gitlab-ci.yml), 
the full CI configuration looks like this:

```yaml
variables:
  S3_BUCKET_NAME: "yourbucket"

deploy:
  image: python:latest
  script:
  - pip install awscli
  - aws s3 cp ./ s3://$S3_BUCKET_NAME/ --recursive --exclude "*" --include "*.html"
  only:
  - master

pages:
  image: alpine:latest
  script:
  - mkdir -p ./public
  - cp ./*.html ./public/
  artifacts:
    paths:
    - public
  except:
  - master
```

We specified two jobs. One job deploys the website for your customers to S3 (`deploy`).
The other one (`pages`) deploys the website to GitLab Pages.
We can name them "**Production** environment" and "**Staging** environment", respectively.

![Deployment to two places](/images/blogimages/ci-deployment-and-environments/16.jpg){: .illustration}*<small>All branches, except master, will be deployed to GitLab Pages</small>*

## Introducing Environments

GitLab offers
 [support for environments](http://docs.gitlab.com/ee/ci/environments.html#environments),
 and all you need to do it to specify the corresponding environment for each deployment *job*:

```yaml
variables:
  S3_BUCKET_NAME: "yourbucket"

deploy to production:
  environment: production
  image: python:latest
  script:
  - pip install awscli
  - aws s3 cp ./ s3://$S3_BUCKET_NAME/ --recursive --exclude "*" --include "*.html"
  only:
  - master

pages:
  image: alpine:latest
  environment: staging
  script:
  - mkdir -p ./public
  - cp ./*.html ./public/
  artifacts:
    paths:
    - public
  except:
  - master
```

GitLab keeps track of your deployments, so you always know what is currently being deployed on your servers:

![List of environments](/images/blogimages/ci-deployment-and-environments/environments.png){: .shadow}

GitLab provides full history of your deployments per every environment:

![List of deployments to staging environment](/images/blogimages/ci-deployment-and-environments/staging.png){: .shadow}

![Environments](/images/blogimages/ci-deployment-and-environments/17.jpg){: .illustration}

Now, with everything automated and set up, we’re ready for the new challenges that are just around the corner.


## Deal with Teamwork Part 2

It has just happened again.
You've pushed your feature-branch to preview it on staging; a minute later Patrick pushed
his branch, so the Staging was re-written with his work. Aargh!! It was the third time today!

Idea! <i class="fa fa-lightbulb-o" style="color:#FFD900; font-size:.85em" aria-hidden="true"></i> Let's use Slack to notify us of deployments, so that people will not push their stuff if another one has been just deployed!

### Slack Notifications

Setting up Slack notifications is a [straightforward process](http://docs.gitlab.com/ce/project_services/slack.html).

The whole idea is to take the [Incoming WebHook](https://api.slack.com/incoming-webhooks) URL from Slack...
![Grabbing Incoming WebHook URL in Slack](/images/blogimages/ci-deployment-and-environments/incoming-webhook.png){: .shadow}

...and put it into **Settings > Services > Slack** together with your Slack username:
![Configuring Slack Service in GitLab](/images/blogimages/ci-deployment-and-environments/services-slack.png){: .shadow}

Since the only thing you want to be notified of is deployments, you can uncheck all the checkboxes except the “Build” in the
settings above. That’s it. Now you’re notified for every deployment:

![Deployment notifications in Slack](/images/blogimages/ci-deployment-and-environments/slack.png){: .shadow}

## Teamwork at Scale

As the time passed, your website became really popular, and your team has grown from 2 to 8 people.
People develop in parallel, so the situation when people wait for each other to
preview something on Staging has become pretty common. “Deploy every branch to staging” stopped working.

![Queue of branches for review on Staging](/images/blogimages/ci-deployment-and-environments/queue.jpg)

It's time to modify the process one more time. You and your team agreed that if
someone wants to see his/her changes on the staging
server, he/she should first merge the changes to the “staging” branch.

The change of `.gitlab-ci.yml` is minimal:

```yaml
except:
- master
```

is now changed to

```yaml
only:
- staging
```

![Staging branch](/images/blogimages/ci-deployment-and-environments/18.jpg){: .illustration}*<small>People have to merge their feature branches before preview on Staging</small>*

Of course, it requires additional time and effort for merging, but everybody agreed that it is better than waiting.

### Handling Emergencies

You can't control everything, so sometimes things go wrong. Someone merged branches incorrectly and
pushed the result straight to production exactly when your site was on top of HackerNews.
Thousands of people saw your completely broken layout instead of your shiny main page.

Luckily, someone found the **Rollback** button, so the
website was fixed a minute after the problem was discovered.

![List of environments](/images/blogimages/ci-deployment-and-environments/rollback-arrow.png){: .shadow}*<small>Rollback relaunches the previous job with the previous commit</small>*

Anyway, you felt that you needed to react to the problem and decided to turn off
auto deployment to production and switch to manual deployment.
To do that, you needed to add `when: manual` to your _job_.

As you expected, there will be no automatic deployment to Production after that.
To deploy manually go to **Pipelines > Builds**, and click the button:

![Skipped job is available for manual launch](/images/blogimages/ci-deployment-and-environments/skipped.png){: .shadow}


Finally, your company has turned into a corporation. You have hundreds of people working on the website,
so all the previous compromises are not working anymore.

### Review Apps

The next logical step is to boot up a temporary instance of the application per feature-branch for review.

In our case, we set up another bucket on S3 for that. The only difference that
we copy the contents of our website to a "folder" named by a name of
the development branch, so that the URL looks like this:

`http://<REVIEW_S3_BUCKET_NAME>.s3-website-us-east-1.amazonaws.com/<branchname>/`

Here's the replacement for the `pages` _job_ we used before:

```yaml
review apps:
  variables:
    S3_BUCKET_NAME: "reviewbucket"
  image: python:latest
  environment: review
  script:
  - pip install awscli
  - mkdir -p ./$CI_BUILD_REF_NAME
  - cp ./*.html ./$CI_BUILD_REF_NAME/
  - aws s3 cp ./ s3://$S3_BUCKET_NAME/ --recursive --exclude "*" --include "*.html"
```

The interesting thing is where we got this `$CI_BUILD_REF_NAME` variable from.
GitLab predefines [many environment variables](http://docs.gitlab.com/ce/ci/variables/README.html#predefined-variables-environment-variables) so that you can use them in your jobs.

Note that we defined the `S3_BUCKET_NAME` variable inside the *job*. You can do this to rewrite top-level definitions.
{: .alert .alert-info}

Visual representation of this configuration:
![Review apps](/images/blogimages/ci-deployment-and-environments/19.jpg){: .illustration}

The details of Review Apps implementation depend widely on your real technology
stack and on your deployment process, which is out of the scope of this blog post.

It will not be that straightforward, as it is with our static HTML website.
For example, you had to make these instances temporary, and booting up these instances
with all required software and services automatically on the fly is not a trivial task.
However, it is doable, especially if you use Docker, or at least Chef or Ansible.

We'll cover deployment with Docker in another blog post. To be fair, I feel
a bit guilty for simplifying the deployment process to a simple HTML files copying, and not
adding some hardcore scenarios. If you need some right now, I recommend you to read article ["Building an Elixir Release into a Docker image using GitLab CI"](https://about.gitlab.com/2016/08/11/building-an-elixir-release-into-docker-image-using-gitlab-ci-part-1/)

For now, let's talk about one final thing.

### Deploying to Different Platforms

In real life, we are not limited to S3 and GitLab Pages. We host, and therefore,
deploy our apps and packages to various services.

Moreover, at some point, you could decide to move to a new platform and thus need to rewrite all your deployment scripts.
You can use a gem called `dpl` to minimize the damage.

In the examples above we used `awscli` as a tool to deliver code to an example
service (Amazon S3).
However, no matter what tool and what destination system you use, the principle is the same:
you run a command with some parameters and somehow pass a secret key for authentication purposes.

The `dpl` deployment tool utilizes this principle and provides a
unified interface for [this list of providers](https://github.com/travis-ci/dpl#supported-providers).

Here's how a production deployment _job_ would look if we use `dpl`:

```yaml
variables:
  S3_BUCKET_NAME: "yourbucket"

deploy to production:
  environment: production
  image: ruby:latest
  script:
  - gem install dpl
  - dpl --provider=s3 --bucket=$S3_BUCKET_NAME
  only:
  - master
```

If you deploy to different systems or change destination platform frequently, consider
using `dpl` to make your deployment scripts look uniform.


## Summary

1. Deployment is just a command (or a set of commands) that is regularly executed. Therefore it can run inside GitLab CI
2. Most times you'll need to provide some secret key(s) to the command you execute. Store these secret keys in **Settings > Variables**
3. With GitLab CI, you can flexibly specify which branches to deploy to
4. If you deploy to multiple environments, GitLab will conserve the history of deployments,
which gives you the ability to rollback to any previous version
5. For critical parts of your infrastructure, you can enable manual deployment from GitLab interface, instead of automated deployment 


<style>
img.illustration {
  padding-left: 12%;
  padding-right: 12%;

}
@media (max-width: 760px) {
  img.illustration {
    padding-left: 0px;
    padding-right: 0px;
  }
}
</style>