---
title: "Tutorial: It's all connected in GitLab"
date: 2016-03-08
categories: tutorial
author: Heather McNamee
author_twitter: nearlythere
image_title: '/images/unsplash/stars.png'
---

In GitLab, everything you do can be cross-linked and referenced.
This improves discoverability and reduces duplicate effort.

GitLab is more than just a Git repository manager.
There are a number of tools to help you collaborate with others, or even
just manage a project yourself.
The best features of GitLab help you link and reference related work.

 **Sign up for our webcast!** Find out more about making the most of GitLab to collaborate
 on your projects, join us for our GitLab Intro
 [webcast on GitLab Workflow][webcast], Thursday March 10th.

<!-- more -->

## Your issue is the Single Source of Truth

As mentioned in my previous post, [always start with an issue][start-issue].

This way you have everything you need to know about the issue in one place.
You can use [GitLab Flavored Markdown] to format content in the issue.

Later, as you make decisions, keep the issue description updated as the "Single
Source of Truth" particularly when you hand off the issue and assign to someone else.
We use this as a [guideline in our own handbook about our workflow][ssot].

> When reassigning an issue, make sure that the issue body contains the
latest information. The issue body should be the single source of truth.

Link directly to other issues and even comments to identify where you have
made decisions. The links will get formatted to be more readable.

![Link to comments](/images/blogimages/connect-commentlink.png)

## Referencing what's related

Add [references] in issue or merge request descriptions or in comments.
This will update the issue with info about anything related.

- To reference an issue: `#123`
- To reference a MR: `!123`
- To reference a snippet `$123`

You can make all the same [references] in comments or merge requests as you can
in an issue description.

The purpose of the [WIP]: (work in progress) merge request is to encourage early code
review, so you can share your work with others.
In this way you can reference related work, and hopefully reduce duplicate effort.

## Labels and milestones at a glance

Add [labels] for categorization.
Labels can have a description and a color.

Add a [milestone] to set a target date. A milestone is often used for releases,
but you can also use milestones to create a simple workflow.

The [milestone view][milestone-mr] lets you see the status of issues at a glance, and you can
see the labels in this view.

![Milestone display of issue](/images/blogimages/connect-milestone.png)

The same goes for the display of merge requests tagged under a milestone.

![Milestone display of MRs](/images/blogimages/connect-milestonemr.png)

You can also view [milestones across an entire group][group-milestones].

## References in Commits and Code review

Similar to references on merge requests, you can add references in commit messages.
Further details are in documentation for [GitLab Flow commit messages][glf-commit].

> `git commit -m "Awesome commit message (Fixes #21 and Closes group/otherproject#22)"`

Your colleague can provide line by line code review.
Commits also have a comment thread available for discussion,
and the rules of referencing apply.
You can also link directly to lines of code in comments.

## @Mention others and assign

GitLab is a platform for collaborating.
You can mention people with @username and ask them to provide feedback in
merge requests or issues.
You can also assign someone to an issue or MR.

In either case, the user will see a notice pop up on their [Todos] list.

![Todos](/images/blogimages/todos-screenshot.jpg)

When issues are assigned in GitLab, it's assumed someone is working on it,
and it appears as "Ongoing", open and assigned.
Make sure to unassign yourself to indicate when you are *not* working on an issue,
and this will make it more likely that the issue will be picked up.

There’s always a single person responsible to work on a MR at one time.
Usually the person who is assigned to the MR is responsible for making any
amendments suggested in review.

We have a feature if you want to approve merge requests in EE, but there's one
person who presses the final merge button.
Hence, only one person can be assigned at a time.

## What will this merge request resolve? Close issues automatically.

In your merge request description add "Closes #123" or "Fixes #123".
When you merge that branch, GitLab will close the issues you
referenced with Fixes #ID or Closes #ID.

![Close when the MR is merged](/images/blogimages/connect-relatedmr.png)

You can use all the collaborative tools we have at the point of a merge request.
So you can add all the same references, categorization, and comments that you
can in issues.
There's a key difference. Merge requests generally resolve issues.
Adding that reference means GitLab can take care of tidying up your issue
tracker when you're done.

[*Merge when build succeeds*][merge-succeeds] is not just a timesaver, it
also helps keep your momentum going.

After merging you may want to turn your mind to the next project.
Or you may simply need a break!
You don't want to come back and have to remember to check and then merge,
and then have to remember to close related issues.
Let GitLab do that for you.

## Live tutorial: GitLab workflow

In our next webcast on March 10th, we'll dig into the GitLab workflow outlined
above, and you can ask questions live about getting the most out of GitLab.
This will take you through the steps of making an issue, merge requests, and
using tools in GitLab for cross-referencing and keeping your issue tracker
organized with labels and milestones.

- Date: Thursday, March 10, 2016
- Time: 5pm (17:00) UTC; 12pm EST; 9am PST
- [Register here][webcast]

Can't make it? Register anyway, and we'll send you a link to watch it later!

[merge-succeeds]: http://doc.gitlab.com/ce/workflow/merge_when_build_succeeds.html
[milestone-mr]: https://gitlab.com/gitlab-org/gitlab-ce/milestones/22
[group-milestones]: https://gitlab.com/groups/gitlab-org/issues?milestone_title=8.6
[our monthly release issue]: http://doc.gitlab.com/ee/release/monthly.html#create-an-overall-issue-and-follow-it
[create-project]: http://doc.gitlab.com/ce/gitlab-basics/create-project.html#how-to-create-a-project-in-gitlab
[ssot]: https://about.gitlab.com/handbook/#gitlab-workflow
[start-issue]: https://about.gitlab.com/2016/03/03/start-with-an-issue/
[webcast]: http://page.gitlab.com/mar-2016-gitlab-introduction.html
[glf-commit]: http://doc.gitlab.com/ee/workflow/gitlab_flow.html#committing-often-and-with-the-right-message
[GitLab Flow]: http://doc.gitlab.com/ee/workflow/gitlab_flow.html
[Patricio-tips]: https://about.gitlab.com/2015/02/19/8-tips-to-help-you-work-better-with-git/
[Todos]: http://doc.gitlab.com/ce/workflow/todos.html
[WIP]: http://doc.gitlab.com/ce/workflow/wip_merge_requests.html
[gitlab-ui]: https://about.gitlab.com/2016/02/10/feature-highlight-create-files-and-directories-from-files-page/
[GitLab Flavored Markdown]: http://doc.gitlab.com/ce/markdown/markdown.html
[task lists]: http://doc.gitlab.com/ce/markdown/markdown.html#task-lists
[labels]: http://doc.gitlab.com/ce/workflow/labels.html#sts=Labels
[milestone]: http://doc.gitlab.com/ce/workflow/milestones.html
[references]: http://doc.gitlab.com/ce/markdown/markdown.html#special-gitlab-references
