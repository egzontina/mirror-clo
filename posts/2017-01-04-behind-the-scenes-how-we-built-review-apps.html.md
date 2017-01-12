---
title: "Behind the scenes: How we built Review Apps"
author: Mark Pundsack
author_twitter: MarkPundsack
categories: inside gitlab
image_title: '/images/blogimages/code-gitlab-tanuki.png'
description: "GitLab's Head of Product shares an inside look at iterating on one of our latest features"
---

A bunch of us on the GitLab team have known for a while just how important review apps are. Even though this wasn’t something that a lot of customers asked for, we knew we had to tackle it because of how we'd seen it transform a developer's flow. We also knew that tightly integrating it into GitLab would make it even better. Although our aspirations for the feature started out gigantic and magical, we ultimately constrained them to the practical and concrete. Here's a behind-the-scenes look at how we iterated and shipped [Review Apps](https://about.gitlab.com/features/review-apps/) over the last 3 releases.

<!-- more -->

Full disclosure: I used to work at Heroku on the team that shipped [Heroku Review Apps](https://devcenter.heroku.com/articles/github-integration-review-apps), and some of that work was inspired by a tool called [Fourchette](https://github.com/rainforestapp/fourchette), which was created by the great folks at [Rainforest QA](https://www.rainforestqa.com/). Even outside of my personal bias, our CEO, CI Lead and others had seen things like this elsewhere and saw how transformative it could be.

<figure class="video_container">
  <iframe src="https://www.youtube.com/embed/CteZol_7pxo?start=1713" frameborder="0" allowfullscreen="true"> </iframe>
</figure>

There are a ton of different ways we could have shipped it. We started months ago, mostly discussing asynchronously on GitLab issues, with big ideas that made Review Apps seem kind of daunting. We had ideas for black magic to detect Kubernetes settings, configure all the review app stuff for you, make them work only for merge requests rather than for every branch, etc. It felt like something that might not ship for months, if not years, because of all the complexity and dependencies.

But then a few of us got together to see how we could simplify, starting with a written proposal, then collaborating in a Google Doc, then a live chat over Google Hangouts, and we came up with what we felt would be the smallest thing we could do to enable the functionality. We shared that proposal back on the public issue. After a couple days, we pushed it even further and really cut the scope.

Here are a few links to some of the issues we went through, starting with a large meta issue, down to a concrete proposal and then counterproposal, until finally, the winning proposal emerged:

* [#3286](https://gitlab.com/gitlab-org/gitlab-ce/issues/3286) - [Epic] GitLab Deploy, _opened 1 year ago_
* [#14698](https://gitlab.com/gitlab-org/gitlab-ce/issues/14698) - Container scheduler for 4 use cases, _9 months ago_
* [#20255](https://gitlab.com/gitlab-org/gitlab-ce/issues/20255) - [Meta] Review Apps, _5 months ago_
* [#20054](https://gitlab.com/gitlab-org/gitlab-ce/issues/20054) - Review Apps as Runner job, _5 months ago_
* [#21411](https://gitlab.com/gitlab-org/gitlab-ce/issues/21411) - How do we do deploys, _4 months ago_
* [#21971](https://gitlab.com/gitlab-org/gitlab-ce/issues/21971) - Dynamic environments aka Review Apps, _3 months ago_

## 8.12

We initially offered experimental support for Review Apps in GitLab 8.12. At that point, we had reduced it to just one or two seemingly small changes to the `.gitlab-ci.yml` format. Specifically, we let you specify the URL of an environment in `.gitlab-ci.yml` (rather than just in the web UI), and we let you use variables within the environment name and URL. Trivial, right? One extra keyword and another small change enabled environments to now be “dynamic,” which is the core of Review Apps.

```yaml
review_apps:
  environment:
    name: review/$CI_BUILD_REF_NAME
    url: http://$CI_BUILD_REF_NAME.review.gitlab.com/
```

## 8.13

Then in 8.13 we implemented another key piece: the ability to delete or stop apps. Again, there were all sorts of complex ideas for how to solve this, but we settled on the smallest change possible that enabled the feature. In this case, that was reusing our existing concept of manual actions, or jobs that run in a pipeline only when a user triggers them manually from the web UI. So we said, if you can script how to delete your app, just create a manual action job for it. Then we added a new keyword in `.gitlab-ci.yml` so you could identify which of these jobs stopped the environment, and we displayed a different UI for that - now you get a little square stop button instead of the triangle play button. Again, pretty trivial.

```yaml
review:
  environment:
    name: review/$app
    on_stop: stop_review

stop_review:
  script: echo Delete My App
  when: manual
  environment:
    name: review/$app
    action: stop
```

## 8.14

Most recently, in the 8.14 release, we made it so that we automatically detect when a branch is deleted, and run that manual action automatically for you. We also realized that with tons of Review Apps, your environments list might get unmanageable. To mitigate this, we came up with the convention that if you named your review app starting with a common name and then a slash, we’d treat that like a folder by which to group your apps, so the interface can show a bunch of Review Apps behind a collapsed folder. Once again, these are relatively small changes.

* Auto-stop on branch delete
* Folders in environment list

## Wrap up

Ultimately this really complex, life changing feature was broken down into 3 releases of the minimal viable change.

While we say Review Apps is now complete, it’s not finished. In fact, we have a saying that nothing is ever finished because we’re always looking for the minimal change, and then iterating. By shipping smaller pieces, we not only deliver faster, but we learn from what’s been shipped, and then iterate smarter.

We’ve now got follow-on issues to look at simplifying the `.gitlab-ci.yml` syntax for Review Apps, and even adding back some of that magic we originally envisioned. We’ll continue to iterate, and your feedback is key to us shipping better.

* [#25138](https://gitlab.com/gitlab-org/gitlab-ce/issues/25138) - Simplify `.gitlab-ci.yml` syntax for stopping Review Apps
* [#24197](https://gitlab.com/gitlab-org/gitlab-ce/issues/24197) - Smart deploy
* [#23580](https://gitlab.com/gitlab-org/gitlab-ce/issues/23580) - Auto deploy

_Tweet us [@GitLab](https://twitter.com/gitlab), check out our [job openings](https://about.gitlab.com/jobs/), or add your questions and suggestions to our [issue tracker](https://gitlab.com/gitlab-org/gitlab-ce/issues)!_
