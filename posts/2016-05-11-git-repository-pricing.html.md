---
title: "The future of SaaS hosted Git repository pricing"
author: Sid Sijbrandij
author_twitter: sytses
date: 2016-05-11 16:00
image_title: /images/unsplash/stars.png
---

Today [GitHub announced pricing changes to all of their paid plans on GitHub.com](https://github.com/blog/2164-introducing-unlimited-private-repositories). With these
changes, paid plans on GitHub.com will now include unlimited private repositories. At GitLab,
we were not surprised to hear about these pricing changes. We believe they are inline with
how pricing will move in the future. At GitLab, we think per-user pricing is the best pricing
model because it is more predictable, less restrictive on code, and aligned with value the
organization gets.

<!-- more -->

## Microservices

The rise of microservices, an approach to development in which you structure your software
into smaller individual service-oriented units. Each microservice then runs its own process
and they communicate with each other through APIs. This software development approach is known
to have four primary benefits: agility, efficiency, resiliency, and revenue. With such tangible
business benefits, it is no wonder why Google, Amazon, and Facebook have been using microservice
development practices for over a decade. Matt Miller details the significance of microservices
in his article, [‘Innovate or Die: The Rise of Microservices’](https://www.sequoiacap.com/article/build-us-microservices/) published in January 2016 on Sequoia
Capital’s blog.

## Unlimited repos is table stakes

As more and more developers, teams, and organizations seek out the advantages of microservices,
they’ll need more repositories to support this new code structure. Basically, the more microservices
you have the more repositories you’ll need. That is why it is not surprising that GitHub has announced
free private repositories. With their announcement today, now GitHub.com, Bitbucket.org, and GitLab.com all offer
unlimited private repositories. It does not cost companies much more to host additional repositories for a given user.
You can think of hosting additional repositories like you think about your email. Once you have an
email account, you are usually not asked to pay more to store more. Unlimited repositories have become table stakes for a Git hosting SaaS service.

## Pricing overview

Price for Git repository hosting per month in popular cloud solutions

| 	   | GitHub.com old | GitHub.com new| BitBucket.org | GitLab.com |
| :--- | :---------: | :---------: | :-----------: | :--------: |
| **Personal usage**	| | | |
| 1 private repo    | $7	| $7	| $0	| $0
| 100 private repos	| $200	| $7	| $0	| $0
| **For organizations**	| | | |
| 5 collaborators  | depended on repos | $25 | $0 | $0
| 10 collaborators | depended on repos | $90 | $10 | $0
| 11 collaborators | depended on repos | $99 |$25	| $0
| 100 collaborators | depended on repos | $900 |$100	| $0
| Unlimited	collaborators | | N/A	| $200 | $0

## Unlimited is great

It’s awesome that repositories have become table stakes across the market.
We truly believe it will
lead to better development practices since developers will no longer be constrained with physical
storage or with financial limitations. However, with more repositories, we assume developers will
write more code and seek out more contributors to collaborate on your projects.

## For some this is a price increase

While the news of
GitHub’s pricing is great if you have a lot of repos, it is not so helpful to people who have a lot
of contributors. At GitLab, we strongly believe that
“everyone can contribute.” This message is exemplified not only in how we build our own products but
also in how we price them. On GitLab.com, our free SaaS version, we offer unlimited private repositories,
unlimited contributors, and unlimited CI runners, all for free.

Here are some examples and quote's we've read about how these pricing changes will affect GitHub users.

* For small teams, this announcement is a positive change. Their bill will most likely decrease, similar to [this person](https://news.ycombinator.com/item?id=11674148) who will see a 4X decline in their monthly bill.
* If you are part of a larger team, your price will likely increase. In the case of [the Open edX non-profit](https://news.ycombinator.com/item?id=11674530), their price could potentially increase 10X due to the fact that they have a lot of contributors.
* [This comment on HackerNews](https://news.ycombinator.com/item?id=11674507) sums it up best: "there is an entire category of companies (agencies / software house) where the price is going up dramatically (5x, 10x or more). One example is Ruby on Rails core alumni Thomas Fuchs that will go [from $100 to $1296 per month](https://twitter.com/thomasfuchs/status/730415066399518720) because he has to pay for no longer active users.

## Business models

When it comes to SaaS hosted Git repository pricing models, it seems GitHub is pursuing more of a network
pricing model where users are asked to pay for 3rd party services. Atlassian is leveraging their
expansive product suite to get users to get additional paid services from them, like JIRA and Bamboo. At
GitLab, we offer a free product with free services, for example [unlimited CI Runners](https://about.gitlab.com/2016/04/19/gitlab-partners-with-digitalocean-to-make-continuous-integration-faster-safer-and-more-affordable/).
Our goal is to make our solution include everything you need to go [frictionless from idea to production](https://about.gitlab.com/direction/#scope) at a price where [everyone can contribute](https://about.gitlab.com/strategy/).

## Why is GitLab.com free

Typically, when we are out introducing GitLab at events, or even to friends, they ask, [how is
it all free?](https://news.ycombinator.com/item?id=11673281). We currently have the following offerings:

* GitLab.com: Free SaaS version featuring private repos, contributors, and CI runners (powered by Digital Ocean).
* GitLab Community Edition: Free on-premises version featuring unlimited users and CI.
* GitLab Enterprise Edition: $39/user/year offering an on-premises version with additional enterprise-specific features, security, and support.
* GitHost.io: Paid depending on the server size you want us to host for you.

We detailed our thinking about [why GitLab will be free now and free forever](https://about.gitlab.com/gitlab-com/#why-gitlab-com-will-be-free-forever) in [2015](https://gitlab.com/gitlab-com/www-gitlab-com/commit/e7e2faec2eca5d35629504b4435358615147fbec).
Our goal has always been two-fold: to build an integrated solution that supports the full software
development lifecycle and to make our products accessible so that everyone can contribute. Within our
business model, we make money through our on-premises solution. This is what allows us to offer
completely free products. As more and more people see the benefit of a free solution that supports
coding, testing, and deployment, we are seeing more users on GitLab.com. Due to the rapid
growth, GitLab.com's performance slowed down. We recognize this and we have been working really hard to [make GitLab.com faster](https://gitlab.com/gitlab-com/operations/issues/42). As you explore what solutions are best for you, your team, or your company, we hope
that you’ll consider us. As always, if you have any questions or comments feel free to ask them here or
on [our Twitter](https://twitter.com/gitlab).
