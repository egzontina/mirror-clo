---
title: "Track your time in the same tool you do your work"
author: Regis Freyd
author_twitter: djaiss
categories: feature
image_title: '/images/default-blog-image.png'
description: "Announcing Time Tracking in GitLab"
---

In 8.14 we are adding Time Tracking to GitLab Enterprise Edition as a Product to allow teams to stack their project estimates against their time spent. At GitLab, our goal is to build everything software development teams need to collaborate efficiently into one product. With each new release we reduce the number of external tools you need, allowing you to complete the full software development lifecycle within GitLab. Lets take a look at how Time Tracking works.

<!-- more -->

Most teams use external tools to track time, but we wanted to give them a more natural and distraction free way to do this in the same tool they already use for the rest of the the software development lifecycle. Like the rest of GitLab, Time Tracking is simple, efficient and out of the way. All you need is two new Time Tracking **slash commands** accessible from the body of an issue and merge request and in a comment field:

- The `/spend` command will let you record the time you spent working on a task e.g. `/spend 10h 45m`. Multiple spend commands add to the total time spent, visible in the sidebar.
- The `/estimate` command will let you enter a time estimate. Contrary to the `/spend` command, the last `/estimate` entry overrides any previous.

The `/spend` and `/estimate` commands can also be used independently of each other e.g tracking time without a formal estimation stage. With these two simple commands, you and your team have everything you need to get started estimating and track your time, all from within GitLab. You can read more about the exact specification in the [corresponding issue](https://gitlab.com/gitlab-org/gitlab-ee/issues/985), or in the [landing page](https://about.gitlab.com/features/time-tracking/).

![time tracking example](images/blogimages/track-your-time-in-the-same-tool-you-do-your-work/time_tracking.png)

Time tracking will be available with GitLab 8.14 as a Product for GitLab Enterprise Edition customers. Time tracking will be free while it is still in beta. It will also be offered as usual for free to anyone on GitLab.com. We can’t wait to see what you will do with it!
