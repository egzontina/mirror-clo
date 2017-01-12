---
title: "GitLab 8.11 Release Webcast: GitLab Issue Board Launch"
author: Amara Nwaigwe
author_twitter: its_amaracle 
categories: release
image_title: '/images/blogimages/Issue_Board_Full_Screen.png'
twitter_image: '/images/tweets/8-dot-11-issue-board-launch-webcast.png'
description: GitLab 8.11 was our biggest release to date. Hear our vision and watch a demo. 
---

This was an exciting release for GitLab! We appreciate all of the commments from the community
on [GitLab 8.11][8.11] being an "epic release". We couldn’t agree more. 

In addition to the release news, 
we made a point to highlight our vision more prominently. If you’re familiar with GitLab and 
our open culture, you know that our vision has always been listed on [our direction page][gitlab-vision]. However, in this 
release, we made our vision a part of our release story as well. GitLab is an integrated set of tools for 
the software development lifecycle. 

The [launch of the GitLab Issue Board][issue-board-launch] makes it easier for customers to 
plan, organize and visualize their issues. The GitLab Issue Board and the Issue Tracker are a perfectly 
paired project management solution. 

In this webcast, we walk through our vision, demo a couple great 
features of GitLab 8.11, and share what's next on our product roadmap. 

<!-- more -->

## In this webcast: 

- Introduction to GitLab and our vision
- Introduction to the GitLab Issue Board
- GitLab 8.11 Feature Highlights 
- Demo
- What’s next 
- Q&A

## Recording & Slides

<figure class="video_container">
  <iframe src="https://www.youtube.com/embed/Ho-9sPthILc" frameborder="0" allowfullscreen="true"> </iframe>
</figure>

<br>

<figure class="video_container">
<iframe src="https://docs.google.com/presentation/d/11geSLSj4eEaY9PMK_1OUXy7N3kTh1k_J58WTJL4sjjc/embed?start=false&loop=false&delayms=3000" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>
</figure>

## Key Takeaways

{::options parse_block_html="true" /}

In case you don't have time to watch the full video, here are the highlights. 

<div class="panel panel-gitlab">
**GitLab built-in integrations** 
{: .panel-heading}
<div class="panel-body">
GitLab is an integrated set of tools, including repository management, access controls, code review, issue tracker, **Issue Board**, and wiki. GitLab supports the full software development lifecycle through its built-in [Continuous Integration, Continuous Deployment, Continuous Delivery][cd], and [Container Registry][container].
</div>
</div>

<div class="panel panel-success">
**Faster from idea to production**
{: .panel-heading}
<div class="panel-body">
Our goal is to help teams go [faster from idea to production][cd-faster]. To do that, we've built chat, issues, wikis, code review, CI, and CD into a single UI. 
</div>
</div>

<div class="panel panel-gitlab-purple">
**10-Step lifecycle**
{: .panel-heading}
<div class="panel-body">
We will ship this complete lifecycle in 2016.

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
</div>
</div>

<div class="panel panel-info">
**New features**
{: .panel-heading}
<div class="panel-body">
[GitLab Issue Board] and [Resolving Merge Conflicts in the UI][mr-conflicts] are awesome features and you should really check them out. 
</div>
</div>

## Join us on for a special event on September 13th

[Register here][event-page] for our special live event on Tuesday, September 13th at 1pm ET / 5pm GMT.
Our CEO, [Sid Sijbrandij][Sid Sijbrandij], will share a special announcement and walk through the
future plan for GitLab and software development. 

Stick around after the announcement for a Q&A session with [Sid][Sid Sijbrandij], CEO, [Job van der Voort][job], 
VP of Product, [Ashley Smith][ashley], Chief Marketing Officer, and guest MC Community Extraordinaire [Jono Bacon][jono-twitter]. 

<!-- identifiers -->

[8.11]: /2016/08/22/gitlab-8-11-released/
[ashley]: https://twitter.com/ashl3ysm1th
[cd-faster]: /2016/08/05/continuous-integration-delivery-and-deployment-with-gitlab/#from-idea-to-production-with-gitlab
[cd]: /2016/08/05/continuous-integration-delivery-and-deployment-with-gitlab/
[ci]: /gitlab-ci/
[cog]: https://gitlab.com/gitlab-org/omnibus-gitlab/issues/1412
[container]: /2016/05/23/gitlab-container-registry/
[cycle]: https://gitlab.com/gitlab-org/gitlab-ce/issues/20975
[event-page]: https://Page.gitlab.com/20160913_UnveilingMasterPlan_landingpage.html
[GitLab Issue Board]: /solutions/issueboard/
[gitlab-vision]: /direction/#vision
[issue-board-launch]: /2016/08/22/announcing-the-gitlab-issue-board/
[issue]: /2016/03/03/start-with-an-issue/
[job]: https://twitter.com/Jobvo
[jono-twitter]: https://twitter.com/jonobacon
[koding]: /2016/07/26/koding-and-gitlab-integrated/
[mattermost]: /2015/08/18/gitlab-loves-mattermost/
[mr-conflicts]: /2016/09/06/resolving-merge-conflicts-from-the-gitlab-ui/
[Sid Sijbrandij]: https://twitter.com/sytses

<style>
.panel-gitlab {
  border-color: rgba(252,163,38,.3);
}
.panel-gitlab > .panel-heading {
  color: rgb(226,67,41);
  background-color: rgba(252,163,38,.3);
  border-color: rgba(252,163,38,.3);
}
.panel-gitlab-purple {
  border-color: rgba(107,79,187,.3);
}
.panel-gitlab-purple > .panel-heading {
  color: rgb(107,79,187);
  background-color: rgba(107,79,187,.3);
  border-color: rgba(107,79,187,.3);
}
</style>
