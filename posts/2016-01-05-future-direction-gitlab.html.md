---
title: "How to see into the future at GitLab"
date: 2016-01-05
author: Heather McNamee
author_twitter: nearlythere
image_title: /images/unsplash/road.png
---

Happy new year, it's a fresh start! Are you making any resolutions? Any plans? Wouldn't it be great if you could see into the future? With GitLab, you can. Well, okay, you can see into the future of _development_ at GitLab, if nothing else. The plans and progress of feature proposals are developed in the open at GitLab. In this post we'll look at how you can find out about the direction of the project.

<!-- more -->

## About GitLab’s Direction page

GitLab’s [Direction page](https://about.gitlab.com/direction/) page has its own fans.

<blockquote class="twitter-tweet" lang="en"><p lang="en" dir="ltr"><a href="https://twitter.com/hashtag/OpenSource?src=hash">#OpenSource</a> at its finest. Thank you <a href="https://twitter.com/gitlab">@gitlab</a>. &#10;<a href="https://t.co/Zkl9Q4gWP0">https://t.co/Zkl9Q4gWP0</a></p>&mdash; Vasil Sarafov (@v45k0) <a href="https://twitter.com/v45k0/status/677139532215689219">December 16, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

People admire the transparency.

<blockquote class="twitter-tweet" lang="en"><p lang="en" dir="ltr">GitLab keeps impressing me lately. Seems like they get community &amp; transparency in ways others have forgotten-<a href="https://t.co/k8YVLhQCEx">https://t.co/k8YVLhQCEx</a></p>&mdash; Kelly Watkins (@_kcwatkins) <a href="https://twitter.com/_kcwatkins/status/676917197709680640">December 16, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

GitLab’s Direction page is managed by the project leads who define the milestones and objectives which are a priority in each release. The developers on the team focus on these priority tasks, after they have addressed any urgent and important tasks such as security vulnerabilities.

Dmitriy [gave a detailed overview of the release process](https://about.gitlab.com/2015/12/17/gitlab-release-process/), which explains where the objectives fit in. On the Directions page, you see an overview of the current plans; and in the [repository itself](https://gitlab.com/gitlab-org/gitlab-ce/issues), you can see the actual objectives being worked on by the developers.

What’s so radical about this?

Most product companies do their feature development in secret, carefully protecting their plans. People are not used to this level of transparency in a software product. In closed-source projects, new changes might come in and blindside users. Even in the case of open source projects, suspicions can be raised as to the motivations behind certain features. Was this for a client? Was it right for the project?

Meanwhile, the company managing the project, whether developing an open source product or not, is working hard to gain technical competitive advantage by keeping their development roadmaps a secret.

We hold no such storehouse of secret plans. It’s all right out there on the [Directions page](https://about.gitlab.com/direction/) and [the repository itself](https://gitlab.com/gitlab-org/gitlab-ce/issues).

For users this has a huge positive effect of allowing them to know what is planned and when they can expect it. For contributors it’s easy for them to see where to spend their effort for maximum effect.

Here are some tips on finding out what is coming next at GitLab.

## How to find out what's coming in future features

If you want to know what is coming up in future releases, check the [Directions page](https://about.gitlab.com/direction/).

Some highlights for upcoming releases include:

- More options for importing, exporting and migrating
- The capability to search through all repositories on the instance
- A notification center

Highlighted issues are grouped by the release. Links to CE and EE next to the release numbers (example: 8.4 <a href="https://gitlab.com/gitlab-org/gitlab-ce/milestones/19">CE</a>, <a href="https://gitlab.com/gitlab-org/gitlab-ee/milestones/6">EE</a>) will take you to the related milestone so you can see all issues related to that release.

That is a great place to start to see into the future.

## What is the status of a particular issue?

Besides the list on the Direction page, you can see what is coming in future releases right from within GitLab.

Issues that are planned for a specific release are assigned to a milestone, such as 8.5. These assignments are subject to change, however this gives you an idea of priority and plans.

![GitLab issue queue showing milestone](/images/blogimages/blog-future-releases.jpg)

## What’s being included in the upcoming release?

If you want to see what has been happening during the development of the next release, look at the CHANGELOG for a particular project, such as [GitLab CE](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG.md).

The CHANGELOG gets updated throughout the month as new merge requests get merged and new features become available in that release. From a few days before the 22nd, you'll have a more clear idea of what the next release will include.

## Transparency

Some software projects must be private for many legitimate reasons. Of course that is why many of our customers choose GitLab, so they can have full control of their on-premises installations.

For our project, there is no such requirement. In fact it's more important that GitLab demonstrates transparency in all we do. We do this by improving access to our development and continuing to work in a spirit of openness.

I know I've personally had the experience of sending in feature requests to other projects or services, and I'm left feeling like they are going into a black hole. I want something more than an automated reply.

Since we've moved in [feature proposals into the GitLab issue queue itself](https://about.gitlab.com/2015/12/16/improving-open-development-for-everyone/), it's easier for you to find out the status of feature proposals. It's also easier to see where the ideas originate all across the board.

For open source projects, suspicions might be raised about the direction of the project being too swayed by customers. It's a delicate balance we're trying to strike.

Especially as we navigate making GitLab into a viable, self-sustaining project, it means we do have requests coming from customers using our software. In the GitLab project you will come across issues marked "[customer](https://gitlab.com/gitlab-org/gitlab-ce/issues?label_name=customer)" to indicate requests by customers. The identity of the customer is always obscured.

Overall this means it's easier to find out where issues arose from, and later on it is also easier for us to follow up with customers who originated the request.
People are free to comment in the issues to help shape the issue.
People are very welcome to contribute features to ensure everyone has them more quickly.
We believe this level of transparency is helpful for users, and also for encouraging contribution and collaboration.

## Conclusion

Hopefully you've got a better idea of what is coming up in future releases at GitLab and how you can find out what is coming next. Okay, so it’s not a crystal ball, but we think it's pretty fantastic.
