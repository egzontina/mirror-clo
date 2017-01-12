---
title: "Feature Preview: Introducing Cycle Analytics"
author: Erica Lindberg
author_twitter: EricaLindberg_
categories: GitLab
image_title: '/images/unsplash/data.png'
description: "Cycle Analytics allows you to measure the time it takes you to move from idea to production!"
twitter_image: '/images/tweets/feature-preview-introducing-cycle-analytics.png'
---

{::options parse_block_html="true" /}

<p  class="alert alert-orange" style="background-color: rgba(252,163,38,.3);
    border-color: rgba(252,163,38,.3); color: rgb(226,67,41) !important; text-align: center;">
    <i class="fa fa-gitlab" style="color:rgb(226,67,41); font-size:.85em" aria-hidden="true"></i>
    &nbsp;&nbsp;
    [Join us for our next release webcast][webcast-registration]{: .purple} on September 29 to
    learn more about Cycle Analytics and our upcoming GitLab 8.12!
    &nbsp;&nbsp;<i class="fa fa-gitlab" style="color:rgb(107,79,187); font-size:.85em" aria-hidden="true"></i>
</p>

Time to market is quickly becoming one of the most important, competitive factors 
for software development companies. However, development teams 
aren't able to track cycle time, largely because there isn't an easy way to do it. 

*Cycle Analytics changes that.* It gives you the ability to measure how much time 
it takes to go [from an idea to production][idea-production] so you can monitor and improve overall cycle time for continuous improvement. 

<div class="panel panel-info">
**What Is Cycle Analytics?**
{: .panel-heading}
<div class="panel-body">
Cycle Analytics measures the time it takes to go from an idea to production for each project you have. 
Not only do we indicate the total time it takes to achieve this, but we break this total time down 
into the multiple stages an idea has to pass through to be shipped. 
</div>
</div>

Cycle Analytics enables you to reduce your cycle time by helping you to identify which steps
in the modern development cycle are slowing down your team. Our [vision][vision] is to bring you all 10 steps of the modern development cycle into one cohesive experience. 
From idea to production, you should be able to monitor the entire process in one place.
[Check out this video][demo] to learn more about our product vision.

![FROM IDEA TO PRODUCTION IN 10 STEPS](/images/blogimages/idea-to-production-10-steps.png)

## How Does Cycle Analytics Help Teams Work Better?##

It's easy to think that you are shipping quickly as a team, but issues can get stuck 
at a specific stage. Without metrics and a high-level 
overview of progress, we just don't know how long it takes to move from stage to stage, making it much harder 
to identify *why* something stalled. 

Cycle Analytics is a way to prevent this from happening by giving you the data you 
need to make better decisions and work better as a team. With metrics to measure 
how long it takes your team to move from idea to production, you can pinpoint areas 
of improvement and more accurately predict your releases. Many teams already measure
a portion of their workflow, such as how long they spend writing code, but Cycle Analytics
allows you to see the entire flow from end-to-end, starting right at the idea stage. 

Reducing cycle time is the competitive advantage of the future. In fact, it's the 
first principle of [Conversational Development][convdev]. Yet, few teams have cycle times of weeks, days, or even hours. 
The goal should be to reach [maximum efficiency][tech-beacon]. The benefit of reducing cycle time is that you can ship quicker, smaller changes. 
This is not only more efficient, but helps teams be more customer-focused by delivering solutions, faster.

![ConvDev Principles](/images/blogimages/feature-preview-introducing-cycle-analytics-convdev-principles.png)

It's not enough to focus on coding speed; what matters is how quickly you 
react to market and customer needs.

## Learn More

The first iteration of GitLab Cycle Analytics will be 
released on September 22, and is part of our [product vision][vision] to help you 
move faster from idea to production. 

Join us on September 29 for our Cycle Analytics webcast and a 8.12 Feature Release demo to learn more. [Register here][webcast-registration].

<!-- cover image: https://unsplash.com/photos/t5BvA-Q_m_Y -->

<!-- identifiers -->

[convdev]: https://about.gitlab.com/2016/09/14/gitlab-live-event-recap/#convdev
[demo]: https://www.youtube.com/watch?v=ZRcWCWatdas
[idea-production]: https://about.gitlab.com/2016/08/05/continuous-integration-delivery-and-deployment-with-gitlab/#from-idea-to-production-with-gitlab
[webcast-registration]: https://Page.gitlab.com/20160922_CycleAnalyticsWebcast.html
[master-plan-recap-post]: https://about.gitlab.com/2016/09/14/gitlab-live-event-recap/
[tech-beacon]: http://techbeacon.com/doing-continuous-delivery-focus-first-reducing-release-cycle-times
[vision]: https://about.gitlab.com/direction/#scope

<style>
.purple {
  color: rgb(107,79,187);
 }
</style>
