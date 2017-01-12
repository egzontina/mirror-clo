---
title: "Open Source Stewardship"
date: 2016-01-11
author: Sytse Sijbrandij
author_twitter: sytses
image_title: '/images/unsplash/sailing-5.jpg'
---

We've recently [detailed our policy and commitment to open source](https://gitlab.com/gitlab-com/www-gitlab-com/merge_requests/1106). We need to think in the interests of the project, while tending to the realities of running a business to support it. I wanted to share some of our thoughts around the decisions behind the policy.

<!-- more -->

## The challenge of being an open source steward

On Opensource.com, Matthias Stürmer identified [four types of open source communities](http://opensource.com/business/13/6/four-types-organizational-structures-within-open-source-communities):

- single-vendor open source projects
- development communities
- user communities
- open source competence centers

We could think of the last three types as marked by distributed development. Sometimes they are managed by community-organized foundations or associations but they have no singular point of commercial support. Examples include Apache, Rails and Linux.

The first type, “single vendor open source projects” is marked by support from a distinct commercial entity which mainly controls the direction and development of the project and financially supports a majority of core developers. Examples of this type of project include Wordpress and Automattic; Hadoop and Cloudera; or Elasticsearch and Elastic.

Every time you have a company in control of an open source project, people will have questions about how the company will behave. The supporting company must balance the practical needs of running the business, supporting the development, and keeping the lights on. The company has to generate revenue, and the community and software project are reliant on the company to sustain. However, compared to closed-source or proprietary software, being open source ensures that the project can be forked and live even beyond the company.

## For us, open source is an ethos not just a license

Open Source arose from the Free Software movement. In the late 90s [when the term ‘open source’ was devised](https://en.wikipedia.org/wiki/Open_source#The_emergence_of_the_.22open_source.22_term), it helped to emphasize the fact that the code was viewable or modifiable. The term open source also downplayed the idea that the software was “free as in beer” which denoted poor-quality. At the same time the term laid the groundwork for commercial ventures to support these kinds of projects. Since 1998 open source has become a de-facto standard, a mark of quality, and an assurance against vendor lock-in.

However, the term open source has somewhat muted the activist origins of the Free Software movement: “free as in freedom.” At the heart of open source is collaboration, which requires trust and safety. When commercial companies supporting open source projects disregard these ethical issues it will serve to erode trust, which is essential for open source to work.

Any companies who "open source" code to gain competitive advantage must address the ethical issues involved. Open Source is more than just a license, it’s also an ethos and commitment. Now, we have encoded our commitment by detailing our policy on being a good steward for the open source project.

## What does it mean to be a good open source steward?

I was hesitant to create a policy until we were sure about the circumstances and context for our project and company. Now that we have a few years of experience, we know better what is required.

First, we need to think in the interests of the project, while tending to the realities of running a business to support it. We’ve outlined our commitment by looking at other communities and projects which have struggled with these issues. Typical criticisms of open source companies include:

- Transparent decision making about the direction of the project.
- Company involvement in or support of open communication channels.
- Putting the company’s interests before the project.

Each of those aspects must be addressed to ensure the project, code, and community of users are supported.

We can’t just tend to the needs of the open source project without tending to the commercial requirements. After all, we know that to sustain the project, we need to make it commercially viable.

Our experienced sales team have helped us understand their struggles. Why should the software be completely free no matter who is using it? They ask “Why do I have users who are running with over 10,000 developers and not paying us a dime?” When selling proprietary services salespeople can set artificial limits which give them leverage. They've asked “Can’t we have some limit, such as if you have over 1000 developers that you need the enterprise edition?” This does make sense from a sales point of view, but it doesn’t make sense in the open source context.

Open source is not a freemium model we can just turn off after 30 days. We can’t say “The first one is free!” It’s all free. Forever.

We’re not the only ones dealing with these issues. “We’ve played with various mixes of what features go in to which offering, with how to balance our need to thrive as a commercial business with our core belief that Open Source is the future of infrastructure,” [wrote Adam Jacob of Chef](https://www.chef.io/blog/2014/09/08/there-is-one-chef-server-and-it-is-open-source/). That was one year ago, and now Chef has come a long way in the stewardship of that project.

Nathen Harvey, now VP of Community Development at Chef said "The intersection of open source and commercial interests raises questions about authority, authenticity, and culture" in [an article on open governance](http://www.informationweek.com/strategic-cio/it-strategy/three-pillars-of-open-source-governance/a/d-id/1318585). Will commercial interests trump what is best for the project? This is a very important question which each single-vendor open source project needs to consider. Nathen's first principle that "Transparency is key" is one we take very seriously.

## What is our policy?

Our beliefs about open source are not only enshrined in our policy, but also in every aspect of how we work. We don't feel any competitive advantage is gained by working in a closed manner. Instead we aim to keep the levels of communication and collaboration with the community of users very high.

- *[Development in the open.](https://about.gitlab.com/2015/12/16/improving-open-development-for-everyone/)* You can submit issues in a public issue tracker. This is not a read-only interface.
- *[Business in the open.](https://about.gitlab.com/2015/08/03/almost-everything-we-do-is-now-open/)* Our company handbook and policies are in the open.
- *[Clear Direction.](/direction/)* Our Direction document clarifies the current project priorities and what is possible in the upcoming releases.

This level of transparency is unheard of in proprietary software, rare even in single-vendor open source software, and unusual even among other repository management platforms (open source or not.) In fact, the history of source code management and communities is rife with obfuscation and abuses of trust. For this reason, we feel that having GitLab as a home for safe, open, collaborative development requires being an open source platform itself.

In our policy, we focused on all of the things we have promised we won’t do. We've addressed the relationship of our CE (Community Edition) and EE (Enterprise Edition), and we've accounted for the requirements of the community by detailing our responsibilities.

We invite members of the community to read the policy. With this policy published, they will be able to hold us accountable.

Please read [“Our stewardship of GitLab CE”](/about/#stewardship).
