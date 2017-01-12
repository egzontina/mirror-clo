---
title: "Introducing Review Apps"
author: Mark Pundsack
author_twitter: MarkPundsack
categories: GitLab workflow
image_title: '/images/blogimages/review_apps_cover.png'
twitter_image: '/images/tweets/introduce-review-apps.png'
description: Transform your development flow with temporary review apps
---

{::options parse_block_html="true" /}

Let's talk about deploys. When a developer starts out with a new idea for an application, they'll typically start working locally, where running the app is as simple as typing `rails server` or `npm start`. But at some point, you need to deploy that app somewhere so that other people, hopefully paying customers, can use it. An easy place to start is to deploy to Heroku or maybe you're using a massive Kubernetes cluster, but really, there are tons of options out there. This post is not about those options. It's about deployment strategy.

<!-- more -->

## Baby steps

When you start, you have no users so there's very little risk in deploying directly to production. If you're still pitching your ideas to VCs, for example, you want your changes pushed up right away, usually right before a big meeting, so you push directly whenever you're ready. Nobody uses the app when you're not showing it to them, so who cares about "production downtime" or pushing untested code with bugs; nobody is using it! So you'll go ahead and create a production app named the same as your project:

- **tanuki**

But of course, you really hope things don't stop there. You push some code, test it out, then get some real users, and eventually you realize you should have a separate app for testing that doesn't affect your real users. So you create a `staging` version, configured as much like production as possible including a production database, memcache or Redis, New Relic, Papertrail, and everything else you have added to your production app, but maybe scaled down so it doesn't cost as much. :) And if you're using GitLab, you'll probably embrace [continuous delivery](/2016/08/05/continuous-integration-delivery-and-deployment-with-gitlab/#continuous-delivery) and set it up to automatically deploy to `staging` any time `master` is updated (but still require a manual deploy to go all the way to production):

- **tanuki**
- **tanuki-staging**

But what about testing out changes earlier on in development? Say you've got a merge request that you want your coworker to check out to see if you're going in the right direction? Ever tried to review a merge request involving CSS just by looking at the code? Yeah, it's not fun. You really need to see it running to know if it's OK or not. So, you start out by asking your team members to pull down your topic branch (you did create a topic branch for your change, right?) and then run the code locally to see how it looks.

```
git pull origin
git checkout topic-branch
bundle install
rails server # or npm start or whatever
```
That works for a while, especially while your entire company is full of developers, but what happens as you grow and you've got product managers, QA testers, and designers that may not have their development environment set up, or are just too busy to bother pulling down your branch just to see your code run. So you create a new `dev` app to show off your code on a running server:

- **tanuki**
- **tanuki-dev**
- **tanuki-staging**

Then your team grows and one day you're running your topic branch on the dev server and someone else pushes a different branch to test their thing, not realizing you were already using the server. Now you realize you need a separate app for each developer on your team:

- **tanuki**
- **tanuki-grzegorz**
- **tanuki-kamil**
- **tanuki-mark**
- ...
- **tanuki-staging**

This lets developers show off their work to their manager or product manager without getting overwritten by another developer. But at some point, in any fast-moving company, a single developer might have multiple features under development and want to demo them at any time, without having to micromanage their single `dev` app. So, you start creating new apps dedicated to big features.

- ...
- **tanuki-new-interface**
- **tanuki-refactor-signup**
- ...

But apps should be easy to create and destroy, so why not create a new one for every branch?

- **tanuki**
- **tanuki-6-update-logo**
- **tanuki-7-refactor-backend**
- ...
- **tanuki-328-fix-typo**
- **tanuki-grzegorz**
- **tanuki-kamil**
- **tanuki-mark**
- **tanuki-staging**

As you can see, this gets complicated pretty quickly and boy, would that be a lot to manage manually.

Over the last few releases, and culminating in 8.14, GitLab has been working to make this easier.

## Introducing Review Apps

Review Apps are ephemeral app environments that are created dynamically every time you push a new branch up to GitLab, and they're automatically deleted when the branch is deleted. This sounds nice and all, but what good is it? Well, rather than having a single `dev` environment for a project, or even separate `dev` apps for each developer, you get a new app for every topic branch, automatically. This let's you test and demo new features without having to ask in chat "hey, can I deploy to `dev`?" It's even better for the people on the periphery. Product managers can check out exactly what a merge request is going to look like without having to download and run a topic branch. QA and other users can take a look without having a development environment installed on their laptop at all.

![Environments](/images/blogimages/review-app-environments.png)

Once you embrace review apps, you'll find it hard to go back. You'll get rid of all your `dev` apps. You might even move on to full [continuous deployment](/2016/08/05/continuous-integration-delivery-and-deployment-with-gitlab/#continuous-deployment) and get rid of your `staging` app. After all, the feature will have gone through full automated CI testing, and with high fidelity feature-level testing on a review app, `staging` becomes an unnecessary speed bump on your way to full-speed productivity. Once a merge request is approved and merged, have it automatically deployed to `production`!

![Deploy Flow](/images/blogimages/deploy_review_apps.png)

Review Apps aren't just for large teams; they're great even for solo developers. Review Apps mean you have an environment running that contains only the code changes of one merge request. This solves four problems:

1. Having each change go through multiple stages (development, staging and QA stages).
1. Finding a problem in staging or QA and having to research what merge request caused it.
1. Having to add screenshots and videos to your merge request.
1. Looking at a merge request and not being able to test the UX and edge cases.

To [get started with Review Apps](https://docs.gitlab.com/ce/ci/review_apps/), you'll need to figure how to create and deploy a new app using shell scripts, then put that into your `.gitlab-ci.yml` in a special job.

You might use NGINX with subdirectories, like [we do for about.gitlab.com](https://gitlab.com/gitlab-com/www-gitlab-com/blob/master/.gitlab-ci.yml#L33-70). Or use the [Openshift client to create and build new apps](https://gitlab.com/gitlab-examples/review-apps-openshift/blob/master/.gitlab-ci.yml). Either way, you're in full control, creating and deploying temporary review apps on your own private infrastructure. Need them behind a firewall on dedicated PCs? No problem. Want them deployed in the cloud using the latest Docker technology? No problem. If you can script it, we can run it with GitLab CI.

## A simple example

The `.gitlab-ci.yml` syntax is somewhat complex because we prefer being explicit over hiding magic. This example shows two jobs, one to start/update a review app, and the other to stop it. The key is in the declaration of an `environment` that has both its `name` and `url` be dynamic, based on the Git branch name. You can name the environment anything you like, but if you follow the convention of starting it with `review/`, the GitLab UI will group the apps in a `review` folder. The `start_review` job then points to the `stop_review` job using the `on_stop` keyword, which helps signal to GitLab to show the option to "stop" or delete the environment in several places in the GitLab interface. Setting the [`GIT_STRATEGY` to `none`](https://docs.gitlab.com/ce/ci/yaml/README.html#git-strategy) is necessary on the `stop_review` job so that the [GitLab Runner](https://docs.gitlab.com/runner) won't try to checkout the code after the branch is deleted. And of course both jobs only run on branches other than `master`.

```yaml
start_review:
  stage: review
  script:
    - rsync -av --delete public /srv/nginx/pages/$CI_BUILD_REF_NAME
  environment:
    name: review/$CI_BUILD_REF_NAME
    url: http://$CI_BUILD_REF_NAME.$APPS_DOMAIN
    on_stop: stop_review
  only:
    - branches
  except:
    - master

stop_review:
  stage: review
  variables:
    GIT_STRATEGY: none
  script:
    - rm -rf public /srv/nginx/pages/$CI_BUILD_REF_NAME
  when: manual
  environment:
    name: review/$CI_BUILD_REF_NAME
    action: stop
  only:
    - branches
  except:
    - master
```

## Conclusion

Review Apps are about improving the fidelity and speed of review; bringing everyone (product managers, QA, designers, etc.) into the conversation earlier, with higher quality information, so you move faster from idea to production. After you embrace them, you'll look back and wonder how you ever lived without them.

Dynamic environments were first introduced with experimental support in 8.12 and the ability to manually stop dynamic environments was introduced in 8.13. 8.14 adds automatic stopping of environments on branch deletion, as well as environment folders in the UI. With that, Review Apps are no longer considered experimental. Review apps are available now, for free, in GitLab CE, GitLab EE, and on GitLab.com.

## Further reading

- [Review Apps documentation](https://docs.gitlab.com/ce/ci/review_apps/)
- [Environments documentation](https://docs.gitlab.com/ce/ci/environments.html)
- [Review Apps with NGINX example project](https://gitlab.com/gitlab-examples/review-apps-nginx)
- [Review Apps with Openshift example project](https://gitlab.com/gitlab-examples/review-apps-openshift)

---

<i class="fa fa-gitlab" style="color:rgb(107,79,187); font-size:.85em" aria-hidden="true"></i>&nbsp;&nbsp;
Don't miss our upcoming Release Webcast: **GitLab 8.14 with Review Apps and Time Tracking** on November 30. We'll live demo Review Apps and Time Tracking for EE. [Register here](https://page.gitlab.com/20161124_ReviewAppsWebcast_LandingPage.html)!
&nbsp;&nbsp;<i class="fa fa-gitlab" style="color:rgb(107,79,187); font-size:.85em" aria-hidden="true"></i>
{: .alert .alert-webcast}
