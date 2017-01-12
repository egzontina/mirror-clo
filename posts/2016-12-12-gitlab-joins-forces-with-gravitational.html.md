---
title: "GitLab and Gravitational discuss Kubernetes"
author: Rebecca Dodd
author_twitter: Reberoodle
categories: integration
image_title: '/images/blogimages/ship-steering-wheel-kubernetes.jpg'
description: "Is Kubernetes the way forward? We chatted to Ev Kontsevoy, CEO of Gravitational and unofficial Kubernetes cheerleader, to get the lowdown"
---
You never know where a conversation on Hacker News might take you. That's what Ev Kontsevoy learned when he left a comment on a post, sparking a conversation with another reader who turned out to be GitLab CEO, Sid Sijbrandij. Later that day, at a party in San Francisco, Ev spotted another party guest wearing a GitLab T-shirt and approached him to chat. "Turns out it was Sid, again!" Ev says, laughing. "It's like he's everywhere."

<!-- more -->

"So we bumped into each other twice in the same day and when we started chatting. Sid mentioned that right now GitLab is trying to figure out the Kubernetes story: how to work with companies that rely heavily on Kubernetes, and frankly also how to use it internally." [Gravitational](https://gravitational.com/) is a Kubernetes company, so Ev was quick to offer their services, which is how GitLab ended up collaborating with Gravitational.

## What did we work on together?

"One area that we were looking at together is how to run PostgreSQL on Kubernetes really well. It’s definitely a problem that most users will be trying to solve and it’s just one of the things that Gravitational is good at: we help our companies migrate their existing applications to Kubernetes, including databases. We've also been working on a GitLab path towards adopting Kubernetes for SaaS internally, after I bumped into some of your team members at a Kubernetes conference in Seattle."

## Why Kubernetes?

Jacob Vosmaer, GitLab Senior Developer, had some questions for Ev about the partnership: "What does a tool like Kubernetes make easier for an application like GitLab?"

Ev: "You mean, 'Why even bother with Kubernetes at all?'"

Jacob: "I was being polite!"

Ev: "Server costs are a major line item on every company’s budget. When you are a certain size it can actually become more expensive than your engineering salaries. Developing software that utilizes servers effectively is difficult. This is where Kubernetes comes in. Unlike the old technology like virtualisation, which would statically partition your servers into smaller VMs, Kubernetes allows you to do this partitioning on the fly, which means that if your application needs more or less of particular resources as it runs, Kubernetes will be dynamically growing and shrinking different components of your application across the infrastructure that’s available to you. So that's really the benefit of Kubernetes, you save a lot of money on hosting if you utilize it."

## Will Kubernetes become the industry standard?

Ev: "We're probably going to witness something similar to Windows vs Linux, where there will probably be No. 1 and No. 2, and perhaps a very small No. 3. It feels to me that No. 1 and 2 are going to be Kubernetes and DC/OS from Mesosphere, for two reasons: DC/OS is an older product, it’s fairly mature, there are now Fortune 500 companies publicly using it. This kind of success doesn’t appear overnight. Even though technically Mesosphere technology is competing with Kubernetes and with what we do, I wish them the best and I do believe they are going to be noticeable."

>"Kubernetes is an unstoppable force right now"

"In my line, Kubernetes is an unstoppable force right now, simply because there are so many companies with a proven track record of popularizing open source who are behind it. Companies like IBM, Red Hat, Google themselves – with so many backers pushing Kubernetes forward, it’s hard for me to imagine it not leading the platform. Look at what happened with Linux: it’s the exact same companies who keep pushing Linux Kernel forward. They're now joining forces again to promote Kubernetes and to evolve and invest money into it."

"Finally, there's container pioneering company Docker, with their own technology called Docker Swarm, so Docker has enormous mind share with developers. Docker Swarm itself is kind of late out of the gate compared to Kubernetes and DC/OS, and I’m very curious to see what’s going to happen. But those are the three players that I think will be carving out this pie, I don’t really see anyone else challenging that."

In addition to their work with GitLab on Kubernetes, Gravitational also helped us [build a Terminal into GitLab](https://gitlab.com/gitlab-org/gitlab-ce/issues/22864), Ev explains, "to allow developers or any GitLab users to easily jump inside the containers that are running on Kubernetes without leaving the GitLab environment". You can [find out how to use GitLab's built-in terminal here](https://about.gitlab.com/2016/11/14/idea-to-production/). Good news for open source! Thanks for working with us, Gravitational.


Image: "[Take the wheel and drive](https://www.flickr.com/photos/rachaelvoorhees/828353700/)" by [rachaelvoorhees](https://www.flickr.com/photos/rachaelvoorhees/) is licensed under [CC BY 2.0](https://creativecommons.org/licenses/by/2.0/)
