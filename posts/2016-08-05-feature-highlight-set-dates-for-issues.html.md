---
title: "Feature Highlight: Set Due Dates for Issues and Create Milestones"
author: Amanda Folson
author_twitter: AmbassadorAwsum
categories: GitLab
image_title: '/images/blogimages/feature-highlight-set-dates-for-issues/gitlab-milestones-cover.png'
twitter_image: '/images/blogimages/feature-highlight-set-dates-for-issues/feature-highlight-set-dates-for-issues.png'
description: "Feature Highlight: Learn how you can leverage issue due dates and milestones to help manage your projects with GitLab."
date: 2016-08-05 10:00:00
---

GitLab has a powerful issue tracker that completely integrates into the GitLab workflow. Our team uses our issue tracker for almost everything, including projects that contain no code. We believe that if anything is significant enough to work on then [it deserves an issue](/handbook/#gitlab-workflow). Before GitLab 8.7, there was no way to communicate that you needed a specific issue to be completed by a specified time. While we had the ability to add milestones to issues and merge requests, there was no way to say "I am working on X and I need to have it completed by Y date." So in GitLab 8.7 we added the ability to set due dates on an issue.

<!-- more -->

## Due Dates for Issues

If you have a hard deadline, it makes sense to make sure the rest of your team 
has insight into when things are due. It can be hard to manage projects where multiple teams are working on different facets of an application, but as of GitLab 8.7 we've made it easy to set due dates for issues and create milestones that incorporate multiple projects.

Setting due dates for issues is a straightforward process -- simply navigate 
to an issue and assign it a due date from the sidebar.

![Due date for issues in GitLab 8.7](/images/blogimages/feature-highlight-set-dates-for-issues/gitlab-issue-due-date.png){: .shadow}

Now, when you view your open issues you'll see the due date of each specific 
issue at a glance.

![Due date for issues in GitLab 8.7](/images/blogimages/feature-highlight-set-dates-for-issues/gitlab-issue-overview-with-due-dates.png){: .shadow}

Please note that that this change only applies to individual issues and not 
milestones.

## Milestones

Milestones are markers for specific points in a project's timeline. For example, "Launching Version 1" or "MVP" could be milestones for your particular project. Each milestone can be made up of multiple parts or tasks. If you were launching version 1 of your application, you might have several tasks such as "Create website copy" or "Develop page layout." These tasks can be anything you think is valuable for a version 1 launch, but it's likely that several tasks would be involved in your version 1 launch.

But what happens if you have multiple teams working on multiple parts of your app as part of your version 1 launch? How do you track what work is related to which milestone within your group?

Using milestones across multiple projects can help you manage all of the work your team and other teams are doing. Once you've created a group, creating milestones across your project is as simple as navigating to your group's "Milestones" page and adding projects to the list.

![Create a milestone for projects under a group](/images/blogimages/feature-highlight-set-dates-for-issues/gitlab-create-milestone.png){: .shadow}

Once the milestone is created, you can add issues to it from any project. The milestone will also appear under each project's "Milestones" tab as if it were specific to that project. You can then view all issues across projects that are tied to that milestone.

![Create a milestone for projects under a group](/images/blogimages/feature-highlight-set-dates-for-issues/gitlab-issues-for-milestone.png){: .shadow}

At any time, you may also get an overview of a milestone's progress. This overview will show you how many issues are open, how many merge requests are open, and the percent of completion based off of completed tasks.

![Create a milestone for projects under a group](/images/blogimages/feature-highlight-set-dates-for-issues/gitlab-ce-milestones.png){: .shadow}

## At GitLab

Internally, we use issue due dates and milestones in a few different ways. Some teams, such as the Dev and Core teams, use milestones to keep track of issues for upcoming releases. Since we release on the 22nd of every month, all issues that pertain to a release milestone [need to be done by the 11th of the month](https://gitlab.com/gitlab-org/gitlab-ce/issues/20497) so that we have enough time to do quality assurance testing and fix problems.

This makes sense for code-related projects, but what about projects that contain no code? The Marketing team here at GitLab uses issue due dates and milestones to keep track of long-term and short-term projects. For example, when we want to launch a new feature, we know that we need to work backwards from the dev team's due date of the 22nd of the month. We can create a milestone for the feature launch and add issues to it for things like creating ad copy, creating one-pagers, creating landing pages, and so on. Milestones help keep the team working towards the goal of launching the feature, while issue due dates help ensure we have everything we need with plenty of time to spare for last-minute changes.

With these features, you and your team will be able to add more visibility into when projects will be completed and can easily break your scope of work down into more manageable chunks. Enjoy!

## What's coming next?

If you're curious what is coming next in GitLab, you can always visit our
[Direction](https://about.gitlab.com/direction/) page for insight into our
roadmap. We always love your feedback.
