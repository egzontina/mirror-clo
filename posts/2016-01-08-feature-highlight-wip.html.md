---
title: "Feature Highlight: WIP"
date: 2016-01-08
author: Job van der Voort
author_twitter: Jobvo
---

At GitLab we'll tell you to make small merge requests, review and merge
often. But in the real world, you have to build a complex feature that
requires weeks and thousands of changes.

How can you still have all the advantages of code review, without actually
merging a half-baked feature? You make it WIP.

<!-- more -->

## WIP First

WIP, short for Work In Progress, is what you prepend to a merge request in
GitLab, preventing your work from being merged.
Next time you're working on a big feature, create a merge request after the
very first commit and give it a title starting with either `WIP` or `[WIP]`.

![WIP merge request in GitLab 8.3](/images/8_3/wip.png)

Mention your colleague for a first review, while you keep on working.
You have all the power of a merge request, including GitLab CI that checks your code
while you work, and no risk of an accidental merge.

## WIP mentality

By opening a merge request at the earliest chance, you use one of
open source's most powerful tools: the opportunity for feedback.

Your colleagues might not be bothered to do a deep review of unfinished code,
but even a glance can catch potential mistakes. Having a second set of eyes
thinking about the problems you're solving always pays off.

I encourage you to extend this mentality to your other work,
projects and pushes. Push something out *early* to receive feedback and
to be steered in the right direction early on.

## At GitLab Inc

At GitLab we prefer people to push things out quickly. We work with WIP merge
requests for complex features, like the [upcoming Elastic Search implementation](https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/109).

Meanwhile, we encourage everyone to make decisions and changes as they think
is appropriate. By sharing early on, collaboration is almost automatic.
