---
title: "Why move to a single code collaboration tool?"
date: 2015-02-6
categories:
author: Marc Radulescu
image_title: '/images/stock/one_instance.jpg'
---

Say your department has five teams, and each team is running its own code collaboration tool.
One of the teams is still using SVN.
Other teams have moved on to a Distributed Version Control Solution (DVCS), but the teams all use different solutions.

All the developers are happy at this time. 
They get to use their own workflow, the one they prefer.
The team leads get to manage tools that they are already comfortable with.
You don't have to deal with people complaining that their tool sucks.

But underneath all that happiness, trouble slowly brews.

<!-- more -->

## Is there anything actually wrong?

The only reason why your teams are happy, is that someone is putting extra effort in keeping your setup together.

First of all, the teams are having trouble collaborating.
When one develper gets involved in another team's project, they need to accommodate their workflow, familiarize themselves with the tool and have all their credentials set-up.
Your admins are spending time facilitating this.

Second, code security is complicated. 
You've got five systems to patch for security updates and five permission schemas to enforce.
Your admins are spending time updating five installations in a timely manner.

Third, integrating these tools into your tool stack always needs extra work.
There's five plugins, or APIs, or services to maintain.
Your admins spend time keeping the integration with the tool stack working.

Fourth, is anyone paying for support over these installations?
If so, that's five agreements to maintain and bother with, and five vendors to maintain a relationship with.

## You can free up resources by consolidating to a single tool.

This way, you're improving collaboration between teams.
With GitLab Enterprise Edition for instance, all the project master needs to do is press two buttons, and their project is shared with another team.
For a front-facing instance, just [switch](http://doc.gitlab.com/ce/public_access/public_access.html) to "internal" privacy and your project is now [innersourced](https://about.gitlab.com/2014/09/05/innersourcing-using-the-open-source-workflow-to-improve-collaboration-within-an-organization/)

Keep security management high level.
One installation to patch, [one permissions schema](http://doc.gitlab.com/ce/permissions/permissions.html).

You're also freeing up your admins from maintaining five different installations.
They don't need to schedule downtime five times anymore.

Lastly, keep the overhead low on the commercial side.
Once point of contact for your questions, one contract to bother legal with, one company to address when you want a new feature.

## There are some caveats, but they can be addressed.

Sure, there might be caveats.

You now have a single solution.
However, that solution is [scalable](https://about.gitlab.com/high-availability/) and you can set-up disaster recovery if you want.

You might think that one tool restricts you to just one workflow.
However, Git allows for a number of different workflows for your teams to choose from.
And if they are not comfortable with any, feel free to recommend them the [GitLab flow](https://about.gitlab.com/2014/09/29/gitlab-flow/).

## There are several next steps to consider.

Start by taking a look at what GitLab has to offer.

With a subscription, you will give you access to a [feature-rich](https://about.gitlab.com/features/#compare) self-hosted solution capable of scaling to thousands of projects and users.

We can help you migrate your projects from other tools such as [SVN](http://doc.gitlab.com/ce/workflow/migrating_from_svn.html) or [GitHub](http://doc.gitlab.com/ce/workflow/import_projects_from_github.html) with ur built-in GitHub importer.
We will help you set a GitLab instance up.

For any further questions, email us at sales@gitlab.com, or [request a quote](https://about.gitlab.com/subscription/form.html) and give us details on your current layout.
