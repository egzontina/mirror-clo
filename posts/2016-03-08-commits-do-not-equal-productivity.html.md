---
title: "Commits Do Not Equal Productivity"
date: 2016-03-08
author: Job van der Voort
author_twitter: Jobvo
image_title: '/images/unsplash/racing.png'
---

If you’re interested in an indication of productivity of individual software engineers (programmers), don’t look at commits or other measures of activity. Look at _consistent progress_ instead.
In this post we'll consider some ways people evaluate or represent productivity,
and I ask for your thoughts on what you track and what you think matters.

<!-- more -->

## Commits

Commits are arbitrary changes captured in a single moment in time. Their size and frequency do not correlate with the work needed to achieve that change. At best, commits can be viewed as an indication of activity.

As a general rule, a programmer should consistently be making commits throughout their work. This can be reduced to ‘a programmer should write code’, which is not very enlightening.
The frequency of the commits, nor the size should be compared between programmers. What should be committed is often a matter of personal preference and is subject to debate.

It can be argued that diminishing commits by a single engineer on a single project can be an indicator of lower productivity. However, that engineer might’ve just read a Hacker News thread that argues for squashing smaller commits.

Don’t measure productivity with commits.

## Weights and Points

Are you using an issue tracker with weights or points? That’s a good start. You can now get a sense of the total volume of work planned and delivered by a team.

Typically, you’d sum the total sum of delivered work and call that _velocity_. You now have a good idea how well your _team_ can estimate the effort required to build things versus how much they actually build things.

Estimating issue weights is notoriously hard and is advised to be done in a group, using games like [Planning Poker]. The issue weight should be taken as an abstract idea of the total body of work, not directly related to the amount of time necessary for this task (this is also why people often use the Fibonacci sequence, and as bigger tasks are harder to estimate).

Measuring the productivity of individuals by looking at velocity on an engineer-by-engineer basis would mean they’d be measured against the ability of the group to estimate work load. Worse is that this would encourage engineers to over-estimate or otherwise ‘play the system’.

Don’t measure productivity with velocity.

## Progress

To get an indication of productivity, look at the progress someone is making in their work. In this sense, progress means someone is taking deliberate steps to work towards solving the problem they are working on.

The best way to get an idea of someone’s progress is to look at _both their communication and activity_. An effective engineer will either be making commits to further their progress or communicate in some way about their work. It’s only when you look at both these factors that you can say something about their productivity.

**A productive engineer communicates and commits. At times, only one of the two.**

## How to Gauge Productivity

I argue that an engineer’s productivity should not be judged by their deliverables or direct output, rather it should be measured by progress. Progress as I define it, is hard to measure, but easy to gauge:

> How is your work going?

A productive programmer will tell you to stop distracting them and come back
in an hour. And then they’ll give you a pretty good idea of their productivity.

## How to Measure Productivity

Right now, in GitLab you can see your commit activity in your profile:

![In your profile, view commits per day in GitLab](/images/commitsprod/commits.png)

and get an idea of how everyone in a project is committing on average during
the day:

![View average project commit activity in GitLab](/images/commitsprod/perday.png)

But both of these measures only relate to direct commit activity.
In GitLab Enterprise Edition, you can get a detailed overview of
the activity of everyone in a group with our [Contribution Analytics].
Here, we give a better overview of the total amount of activity of any
developer, but in all fairness doesn't resolve all problems that I've outlined.

In future releases, we're planning to add more analytics to GitLab,
both relating to code (quality) and activity of its users. I hope that by
combining more data in smart ways, we can give better insights into developer
activity.

I'm especially interested to hear what you think we should measure.
Please feel free to leave a comment below or [create an issue] suggesting
how we can improve analytics in GitLab.

## Live tutorial: GitLab workflow

In our next webcast on March 10th, we'll dig into the GitLab workflow.

This will take you through the steps of making an issue, merge requests, and
using tools in GitLab for cross-referencing and keeping your issue tracker
organized with labels and milestones.

- Date: Thursday, March 10, 2016
- Time: 5pm (17:00) UTC; 12pm EST; 9am PST
- [Register here][webcast]

Can't make it? Register anyway, and we'll send you a link to watch it later.

[Planning Poker]: https://www.planningpoker.com
[webcast]: http://page.gitlab.com/mar-2016-gitlab-introduction.html
[Contribution Analytics]: http://doc.gitlab.com/ee/analytics/contribution_analytics.html
[create an issue]: https://gitlab.com/gitlab-org/gitlab-ce/issues/new
