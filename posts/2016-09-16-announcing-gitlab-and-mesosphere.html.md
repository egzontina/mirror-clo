---
title: "Announcing GitLab + Mesosphere: Five Reasons You Should Be Excited About This Integration"
author: Amara Nwaigwe
author_twitter: its_amaracle
categories: integration
image_title: '/images/blogimages/announcing-gitlab-and-mesosphere-cover.png'
description: "GitLab is now available on DC/OS!"
---

Today we're happy to announce our integration with [Mesosphere](https://mesosphere.com/).
Now you can install GitLab in your DC/OS environment in one-click. If you are not already familiar with Mesosphere, this is the 
perfect chance to get acquainted. Built on top of [Apache Mesos](http://mesos.apache.org/),
[DC/OS](https://mesosphere.com/product/) makes it easier to build, run, and scale modern
apps. How? In short, they let you put your workloads into Docker
containers and then manage those containers from a single secure and highly-available platform. We won't say
more than that so we don't spoil the five reasons to be excited.

<!-- more -->

## The Five Reasons

{::options parse_block_html="true" /}

<div class="panel panel-gitlab">
**1. Simplify the Complexities** 
{: .panel-heading}
<div class="panel-body">
DC/OS is an incredible product that has made something that is genuinely complex feel surprisingly simple and intuitive. Most teams run their applications in production environments composed of multiple servers. Using GitLab.com as an example, at any given time, we run anywhere from 60-200 servers. You can read about the full breakdown in [this blog post](https://about.gitlab.com/2016/04/29/look-into-gitlab-infrastructure/). The point is that your infrastructure team is dealing with a lot of complexity. DC/OS simplifies that, offering a single platform to run everything on the same shared infrastructure.
</div>
</div>

<div class="panel panel-success">
**2. Spin up GitLab Instances in Minutes** 
{: .panel-heading}
<div class="panel-body">
If you've ever spent hours or days configuring your tools, you know what a time-consuming pain it can be. In a world where time to market is everything, your team should take advantage of all the time savings they can get. With this integration, you able to spin up a GitLab instance in minutes, taking advantage of the existing infrastructure in your DC/OS environment. 
</div>
</div>

<div class="panel panel-gitlab-purple">
**3. Utilize Resources More Efficiently** 
{: .panel-heading}
<div class="panel-body">
Let's say you have a pool of servers that you've set up a cluster that can act as a shared computing resource. Any of these servers can run your task, while still being able to run other tasks that fit within their remaining resources, allowing you to maximize the capacity of each server. 
</div>
</div>

<div class="panel panel-info">
**4. Maintain Uptime** 
{: .panel-heading}
<div class="panel-body">
DC/OS is fault tolerant. It keeps GitLab runnning through storage primitives in Mesos. If your GitLab instance dies then your server could just recover itself by simply going to another node. Setting up fault tolerance does require some additional configuration but this is a great way to ensure you don't lose anything.
</div>
</div>

<div class="panel panel-danger">
**5. Analytics and Reporting** 
{: .panel-heading}
<div class="panel-body">
DC/OS offers tools to help you monitor and perform health checks on your applications. You can also pull in metrics from other monitoring platforms, such as [DataDog and Graphite](https://mesosphere.com/solutions/container-orchestration/). DC/OS even wraps your analytics into a nice dashboard view. If you're an existing GitLab customer you know how much we value great UI. We spend a lot of time thinking about how to deliver the best UI in our product. It is clear that the team at Mesosphere does the same. The dashboard views in their product are clean and intuitive so you can maintain a pulse of your infrastructure. 
</div>
</div>

## Resources

If you're interested in learning more or want to learn how you can install GitLab on DC/OS take a look at these resources: 

- [GitLab-on-DC/OS tutorial blog post](https://mesosphere.com/blog/2016/09/16/gitlab-dcos/)
- [GitLab & Mesosphere joint solution brief](https://mesosphere.com/resources/mesosphere-gitlab-joint-solution-brief/)
- [GitLab & Mesosphere webcast recording](https://youtu.be/GPtSI_2-lbM) 

<!-- custom styles -->

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
 