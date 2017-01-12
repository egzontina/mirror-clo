---
layout: post
title: "Trends in Version Control Land: Innersourcing"
categories: concepts
author: Sid Sijbrandij
author_twitter: sytses
image_title: '/images/default-blog-image.png'
---

We’re starting a series of posts that explore existing and growing trends in version control. This week we’re looking at innersourcing.

As a follow-up/update to [a post we did on innersourcing back in 2014][post-2014], we’ll be looking at what innersourcing is, who’s using it, and how it’s solving some of the biggest problems enterprise developers face.

<!-- more -->

## What innersourcing means

Innersourcing is a growing trend in the private sector as more and more commercial companies are starting to adopt open source processes in order to work and collaborate more effectively.
 
In large organizations, developers are often spread out across different departments. These developers may never meet and might not even report to the same boss or have access to the same departmental strategies. However, they have a lot to gain in terms of collaboration and learning from each other.
 
In short, innersourcing is a way of improving developer collaboration within enterprise teams using the workflow models typically associated with open source projects (also composed of developers working at distance, without much communication otherwise).
 
Companies like [PayPal] (a leader in innersourcing) are demonstrating how open source development practices work to make more efficient and profitable businesses, even if the “open” in “open source” really only extends as far as one organization’s team. Other innersourcing pioneers include Bosch, Autodesk, Bloomberg, and SanDisk; these companies are proving that you can run a complex project—and create amazing products for profit—using the same lean and inexpensive system that we use in open source.

## How innersourcing works

When it comes down to the nuts and bolts, large organizations have a lot in common with big open source projects. In both scenarios you’re dealing with a lot of moving parts: a variety of people with different roles, skills and personalities; a variety of tools; a variety of directives and strategies.
 
One of the major differences is in how large organizations run. In the traditional “corporate” model, an organization functions according to the knowledge and instructions of a hierarchy of managers. In part, the efficiency of the organization relies on the ability of people in managerial roles to keep track of large amounts of incoming information.
With so much information funnel up into a managerial bottleneck, it’s not surprising that a number of things may fall through the cracks. As projects get more complex or more people get involved, more things will fall through the cracks.
 
In open source projects, the information related to development is managed through a process of documentation and checks that are designed to avoid anything falling through the cracks.
 
The most important open source workflow practices for enterprises are:

- Visibility
- Forking
- Pull/merge requests
- Testing
- Continuous Integration
- Documentation
- Issue tracker*
 
*Refer back to our [2014 post][post-2014] for more detail on these terms if you’re not familiar.
{: .note}

## Problems innersourcing solves

Here are some of the problems often faced by large organizations that innersourcing could help solve.

| Challenge | Solution |
| --- | --- |
| **Communication.** In big organizations, there usually isn’t one unified team working toward a single goal. Instead, employees tend to be siloed into multiple teams that have their own structures and leadership, and are largely disconnected. Communication norms and terminologies can vary from team to team, and generally speaking, communication is minimal and not very effective between silos. | Open source systems enable participation at a large scale. The lines of communication are direct and visible to everyone in the project. Communication hierarchies are pretty flat, cutting out a lot of the middlemen and thus a lot of the noise.  |
| **Discovery.** A software solution can be created multiple times in different departments, essentially multiplying effort, simply because departments aren’t talking to each other. For example, one department has created a software solution, another department needs that functionality, but there’s no process for checking whether it’s been created already. | The benefit of open source projects is that they’re open. Having access to the project means that you can search to see if someone has already solved the problem that your team is facing. If for some reason you don’t search ahead of starting work on something, there are other people in your project who can see what you’re working on and alert you that your solution already exists. Open source projects increase the discovery of existing solutions and help reduce the duplication of effort. |
| **Red tape.** In most commercial environments, there organizational structures that dictate what you can access. Often times you may be aware that a solution exists but you’d need to request access to a project from an administrator. This takes precious time away from both the developer and the administrator. | With open source projects, if you want to work on a project or see a project, you already have access. This cuts out the administrative work and delays of having to manage request for access, control who can see what, password-protect things, etc. |
| **Making modifications.** In a traditional commercial setting, if you have read-only access to a project, you don’t have the permissions or capability to edit or add a feature you want—you have to ask someone else to do it. If they don’t have time or don’t see the point, you basically have no recourse. The team responsible for the app is tasked with ensuring their app meets deadlines and works, so someone’s job depends on maintaining that application. Even though another team might benefit from this new feature, the request to change the application could interfere with application stability, so granting access is a risk. If a developer can’t get access to make modifications that are needed, this will lead to essentially need to build your own unique codebase or application to solve the problem, and furthermore this might happen multiple times, with multiple people running into the same exact issue. This leads to a lot of apps being built separately to solve the same problem. | If you want to make a change to an open source project, you don’t need to check to make sure it’s okay (and find out it’s not). Instead, you contribute the change you want to see, and let the system test its functionality and validity: first you fork from the codebase, then make your modification. Then you do a merge request, based on which the other developer can verify it, ask questions, test it and so on. The other developer’s work is significantly reduced compared to the proprietary model, because a) they didn’t have to do the extra work themselves, and b) your feature has been tested so they know it works. Everybody wins. There’s the added benefit too that this approach reduces load on the report generator overall, since it only has to support a single codebase instead of eight. |
{: .table-justify}

## Intimidated? Don’t be

Particularly for teams who work collaboratively across distance—which is most teams now—and organizations with multiple departments, innersourcing is a relatively simple way to create a more efficient workflow. It’s a fantastic approach to help your company break down internal communications silos and to encourage more effective collaboration. It can also be used for faster developer onboarding, and it can even set your company up to contribute software back to the open source community. This is great for your company profile and it could even help you to attract top-notch talent to your development team.

## Using GitLab for innersourcing

A growing number of enterprises use GitLab to enable this workflow internally. To make this easier, we’ve introduced a third visibility level for projects: instead of just public projects (visible to the whole world) or private projects (visible only to the participants) you can also mark a project as internal. Internal projects are visible to everyone that is logged into the on-premises GitLab server. This way all employees can reuse software, fork it, and contribute back. This means your code is secure, but you get all the benefits of an open source workflow.

Is your company adopting innersourcing? We’d love to hear how it’s going. Connect with us on Twitter [@GitLab] or leave a comment here.

<!-- Identifiers, in alphabetical order -->

[@GitLab]: https://twitter.com/gitlab
[post-2014]: https://about.gitlab.com/2014/09/05/innersourcing-using-the-open-source-workflow-to-improve-collaboration-within-an-organization/
[PayPal]: http://radar.oreilly.com/2014/07/transparency-and-transformation-at-paypal.html

<style>
	.table-justify {
		text-align: justify;
	}
	.table-justify tr td {
		width: 50%;
	}
	.table-justify tr td:first-child {
	border-right: 2px rgba(107,79,187,.1) solid;
	}
	.table-justify tr:last-child {
	border-bottom: 2px rgba(128,128,128,.2) solid;
	}
</style>
