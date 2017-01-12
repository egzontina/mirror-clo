---
title: "In 13 minutes from Kubernetes to a complete application development tool"
author: Job van der Voort
author_twitter: Jobvo
image_title: '/images/default-blog-image.png'
description: "How GitLab gets you from idea to production"
---

{::options parse_block_html="true" /}

**We promised to implement our master plan before the end of the year**

When we raised our B-round this September we revealed our [Master Plan](https://about.gitlab.com/2016/09/14/gitlab-live-event-recap/):
the ambition to help the world go faster from idea to production with GitLab.
We showed a [faked demo montage](https://youtu.be/ZRcWCWatdas) of how that
would work. We promised to release this before the end of the year. Today I
want to show you our progress to date.

<!-- more -->

## The 13 minute demo of what would normally take days

In the video below I will install GitLab and deploy a simple application from
idea to production in less than 13 minutes.
The demo video consists of the following steps:

1. Install GitLab, Mattermost and auto-scaling GitLab CI on Openshift _from scratch_
1. Set up a project to use GitLab CI and deploy to Kubernetes
1. Create an issue from Mattermost chat
1. Plan this issue using Issue Boards
1. Use the built-in terminal in GitLab to access the container
1. Commit changes to a new branch and create a merge request
1. Review these changes before merging them into master
1. See the proposed changes live in a Review App
1. Merge the changes into master and see them deployed on staging
1. Deploy staging to production from chat
1. Review the cycle time with Cycle Analytics

Below is the unedited, continuous video over which I recorded audio:

<iframe width="640" height="360" src="https://www.youtube.com/embed/a7OIQfOJO-0" frameborder="0" allowfullscreen></iframe>

<br />

More than half of the demo is spent on the first two steps of installing GitLab
and setting up the project. If you want to skip right to the idea to production
cycle [go to 6:30 in the video](https://www.youtube.com/watch?v=a7OIQfOJO-0&t=6m30s).

## Advantages of an integrated setup

If you need to set up self-hosted tools to do autoscaling CI, chatops,
a container registry, and review apps on Kubernetes without GitLab you're
likely spending days to install and connect the tools and script.
GitLab comes with everything to bring your ideas to production out of the box.
This means you:

- Can install and integrate everything in minutes
- No longer need to maintain separate apps and all their integrations
- Have less time spent managing authentications and authorizations,
for example between CI and the private container registry
- Have everything in one interface
- Have a complete overview from idea to production that allows you to improve your cycle time

## Replicating the demo

To replicate the demo you need a private Openshift origin environment. 
The [demo script](https://about.gitlab.com/handbook/sales/idea-to-production-demo/)
is public (along with the version numbers of OpenShift and Kubernetes we're using!) and the RedHat OpenShift template is linked from our
[installation page](/installation/).

We believe container schedulers such as Kubernetes are the future of
application lifecycle management and are working on Mesosphere support.
We would love it if people would contribute support for other container
schedulers such as Docker Swarm and for other Kubernetes providers such as
Tectonic.

## Move to the left

If you visualize the flow from development to production as something from left
to right there is a trend to 'move to the left'.
This means that what was standard practice later in the flow becomes the new
practice earlier. For example CI used to be run on the machine of the
developer, now most CI is run elsewhere.
We think that developer environments will start to resemble production
environments in that they run on the container scheduler.
GitLab will make sure that we allow easy access to them from
[a terminal](https://gitlab.com/gitlab-org/gitlab-ce/issues/22864) and a
[local editor](https://gitlab.com/gitlab-org/gitlab-ce/issues/22876).

## Christmas is coming

Most functionality shown in the video such as review apps will be available with GitLab 8.14, due Nov. 22nd.

We have a lot we still want to build and improve, see our TODO's in our [demo script](/handbook/sales/idea-to-production-demo/) and the [issues for them](https://gitlab.com/groups/gitlab-org/issues?scope=all&state=opened&utf8=%E2%9C%93&label_name%5B%5D=idea-to-production).

We plan to ship everything including terminal access in GitLab 8.15, due just
before Christmas.
Let's end the year with a bang.

<i class="fa fa-gitlab" style="color:rgb(107,79,187); font-size:.85em" aria-hidden="true"></i>&nbsp;&nbsp;
Have more questions? Join me live on November 23 10am PST/6pm GMT for open office hours. [Watch the live stream](https://www.youtube.com/watch?v=njP8Wvp45o0)!
&nbsp;&nbsp;<i class="fa fa-gitlab" style="color:rgb(107,79,187); font-size:.85em" aria-hidden="true"></i>
{: .alert .alert-webcast}
