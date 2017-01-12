---
title: "Announcing The GitLab Issue Board"
author: Sid Sijbrandij
author_twitter: sytses
categories: GitLab
image_title: '/images/blogimages/announcing-the-gitlab-issue-board/gitlab-issue-board-cover.png'
description: "Strengthen your Release Management Process: announcing the GitLab Issue Board!"
twitter_image: '/images/tweets/announcing-the-gitlab-issue-board.png'
date: 2016-08-22 10:02
---

Software is eating the world. Reducing the time between having an idea and having the code in production
is a great competitive advantage. Planning what to do next is an essential part of that process. Today we
introduce our Issue Board that will make it faster to plan issues. It is an integrated part of GitLab, ensuring
you don't have to switch tools to get things done.

<!-- more -->

## Release management isn’t perfect

Understanding your team’s challenges is the first step to solving them.
Speaking from our own experiences shipping GitLab, some of the release
challenges we face are:

**Prioritization:** with nearly 4,500 issues in our [CE project][ce] and
our [direction] issues, we are constantly faced with tough decisions of
where to focus our resources.
{: .alert .alert-info .blue}

**Planning:** we release on the 22nd of every month. To hit our release goal,
we have to be incredibly diligent about what we forecast for each release.
{: .alert .alert-info .blue}

**Communication:** with a growing team consisting of 24 developers, 6 frontend
engineers, and 5 UX designers, it has become increasingly more important to
ensure the full team has visibility into the overall release process.
{: .alert .alert-info .blue}

## What the experts had to say

Obviously, we’re not “the experts.” But we’ve summarized their feedback.
The International Journal of Computer Applications [2013 study][2013] has
great insights into effective release management processes.

<i class="fa fa-globe fa-fw font-awesome purple" aria-hidden="true"></i> **1. Create
a single source of truth:** eliminate the natural differences that
occur with large teams working in different time zones, running different
processes, and using different tools.

<i class="fa fa-arrows-alt fa-fw font-awesome orange" aria-hidden="true"></i> **2. Manage
application dependencies:** avoid release failures by ensuring your
testing environments account for version dependencies.

<i class="fa fa-pencil-square-o fa-fw font-awesome purple" aria-hidden="true"></i> **3. Document
everything:** make sure it’s in a common repository and that it’s
easily discoverable.

<i class="fa fa-eye fa-fw font-awesome orange" aria-hidden="true"></i> **4. Make
approvals visible:** you and your team should have agreed upon quality
bars that determine what makes it into each environment.

<i class="fa fa-terminal fa-fw font-awesome purple" aria-hidden="true"></i> **5. Deploy
consistently across environments:** standardize your build, test,
and deploy process by automating as much as you can. The goal is to
remove error and unpredictability.

<i class="fa fa-crosshairs fa-fw font-awesome orange" aria-hidden="true"></i> **6. Make
the release plan easy to consume:** we’re lumping all the
**P**'s (planning, people, process, and policy) together. They all boil up to
the same key ideas. Policies and plans should be centralized. Ownership must
be clear. Finally, a change in plans needs to be visible to the full team.

## GitLab: From idea to production

That list is easier said than done. But it’s where we are all headed.
Modern development teams are optimizing for speed without sacrificing quality.
They are moving away from older process-driven development styles like Waterfall,
Scrum, and Agile and towards continuous delivery and deployment. To
support modern development practices, GitLab has everything you need to get
[from idea to production faster][cd].

There are 10 steps from idea to production in the modern development lifecycle.

![FROM IDEA TO PRODUCTION IN 10 STEPS](/images/blogimages/announcing-the-gitlab-issue-board/10-step-dev-lifecycle-plan.png)

1. Chat conversation &#8594; [Mattermost ships with GitLab][mattermost]
1. Issue creation &#8594; [GitLab Issues][issue]
1. Planning board &#8594; [GitLab Issue Board]
1. IDE &#8594; [Koding + GitLab][koding] Integration
1. Version control &#8594; GitLab Repositories
1. Continuous Integration &#8594; [GitLab CI][ci] and [GitLab Container Registry][container]
1. Code review &#8594; GitLab Merge Requests
1. Continuous Delivery &#8594; [GitLab Deploy][cd]
1. Chatops &#8594; We're planning to ship [Cog]
1. Feedback &#8594; We plan to ship with [Cycle Analytics][cycle]

The 10 steps of the modern development lifecycle will be included directly in
GitLab in the coming months. Today we are announcing the [GitLab Issue Board],
a software project management tool used to **plan**, **organize**, and **visualize** a team’s
feature or product release process.

## Closer look at the GitLab Issue Board

The Issue Board builds on GitLab’s existing issue tracking functionality and now
offers teams the ability project manage their release and deployment process. This
is the first iteration of our Issue Board. Here are a few things you should know about:

### The GitLab Issue Board

<i class="fa fa-check-circle-o fa-fw font-awesome green" aria-hidden="true"></i> It’s
a new way to **manage** your **issues** in GitLab. Your issues appear as **cards** on the Board.

<i class="fa fa-check-circle-o fa-fw font-awesome green" aria-hidden="true"></i> **Lists**
(or columns) represent each step in your development process.

<i class="fa fa-check-circle-o fa-fw font-awesome green" aria-hidden="true"></i> Your
lists are **based on** your **Labels**. Which means it works out of the box with your existing issues.
So if you’ve already labeled things with “Development” and “Production”, the corresponding issues will
appear in the lists as you create them.

![GITLAB ISSUE BOARD](/images/blogimages/announcing-the-gitlab-issue-board/gitlab-issue-board.png){: .shadow}

### Lists

<i class="fa fa-check-circle-o fa-fw font-awesome green" aria-hidden="true"></i> Each
Issue Board starts with two lists: **Backlog** and **Done**. The Backlog will hold all the issues in
your project which don't have any label assigned to a list. Once you label an issue, and create a list for that
label, it will be automatically moved from **Backlog** to the corresponding list. You can create unlimited lists!

<i class="fa fa-check-circle-o fa-fw font-awesome green" aria-hidden="true"></i> You
can drag and drop the lists to organize your Board according to your own workflow:

![drag and drop issue](/images/blogimages/announcing-the-gitlab-issue-board/gif-drag-and-drop-list.gif){: .shadow .center}

### Labels

<i class="fa fa-check-circle-o fa-fw font-awesome green" aria-hidden="true"></i> When
you move issues between lists, the label on the issue is automatically updated, though it doesn't show on the issue card.

<i class="fa fa-check-circle-o fa-fw font-awesome green" aria-hidden="true"></i> This
new label is displayed in the Issue Tracker as well as on the issue itself. So, even if someone on
your team isn’t checking the Issue Board, they’ll still have a record of what step an issue is on.

![drag and drop issue](/images/blogimages/announcing-the-gitlab-issue-board/gif-drag-and-drop.gif){: .shadow .center}

<i class="fa fa-check-circle-o fa-fw font-awesome green" aria-hidden="true"></i> If
you drag and drop the card to the list **Done**, the issue will be automatically closed.

### Functionality

#### Example

<i class="fa fa-check-circle-o fa-fw font-awesome green" aria-hidden="true"></i> By
adding new lists, you can create workflows. For example, you can create a list
based on the label of “Frontend” and one for “Backend”. A designer can start working on
an issue by dragging it from **Backlog** to “Frontend”. That way, everyone knows,
this issue is now being worked on by the frontend engineers.
Then, once they’re done, all they have to do is drag it over to the next list, Backend,
where a backend developer can eventually pick it up. Once they’re done, they move it to
the list **Done**, to close the issue.

Read through the [Issue Board documentation][doc] to know everything you can do with it.

#### Bonus

<i class="fa fa-check-circle-o fa-fw font-awesome green" aria-hidden="true"></i> Using
GitLab’s existing Label functionality also means that you’ll have all the same
filtering and sorting abilities you see across the rest of the product.

### Live demo

To see the GitLab Issue Board in action, take a look at GitLab Developer Advocates
([Amanda] and [Ivan])’s screencast below.

<figure class="video_container">
  <iframe src="https://www.youtube.com/embed/UWsJ8tkHAa8" frameborder="0" allowfullscreen="true"> </iframe>
</figure>

## Join our webcast

On September 1st, we’ll be hosting a webinar to discuss and demo the Issue Board and all of the other
great features in GitLab 8.11. [Register here][webcast].

<!-- identifiers -->

[2013]: http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.403.1791&rep=rep1&type=pdf
[about-gitlab-com]: htpps://about.gitlab.com/
[cd]: https://about.gitlab.com/2016/08/05/continuous-integration-delivery-and-deployment-with-gitlab/
[ce]: https://gitlab.com/gitlab-org/gitlab-ce/issues
[ci]: https://about.gitlab.com/gitlab-ci/
[cog]: https://gitlab.com/gitlab-org/omnibus-gitlab/issues/1412
[container]: https://about.gitlab.com/2016/05/23/gitlab-container-registry/
[cycle]: https://gitlab.com/gitlab-org/gitlab-ce/issues/20975
[direction]: https://about.gitlab.com/direction/
[doc]: http://docs.gitlab.com/ce/user/project/issue_board.html
[GitLab Issue Board]: /solutions/issueboard/
[issue]: https://about.gitlab.com/2016/03/03/start-with-an-issue/
[koding]: https://about.gitlab.com/2016/07/26/koding-and-gitlab-integrated/
[mattermost]: https://about.gitlab.com/2015/08/18/gitlab-loves-mattermost/
[webcast]: https://Page.gitlab.com/IssueBoardWebcast_LandingPage.html
[Amanda]: https://twitter.com/AmbassadorAwsum
[Ivan]: https://twitter.com/inemation

<style>
  .blue {
    color: rgb(49,112,143) !important;
  }
  .center {
    display: block;
    margin-right: auto;
    margin-left: auto;
  }
  .font-awesome {
    font-size:.85em;
  }
  .purple {
    color:rgb(107,79,187);
  }
  .orange {
    color:rgb(252,109,38);
  }
  .green {
    color: rgb(60,118,61);
  }
</style>
