---
title: "Trends in Version Control Land: Microservices"
categories: concepts
author: Sid Sijbrandij
author_twitter: sytses
description: "The benefits and drawbacks of microservices and how to decide if it is right for your team."
image_title: '/images/blogimages/trends-in-version-control-land-microservices-cover.jpg'
twitter_image: '/images/tweets/trends-in-version-control-land-microservices.png'
---

One trend of the last few years is microservices architecture. In this post we’re
looking at what that is, and what some of the benefits and drawbacks are.

**Note:** This is the third post of our four-post series on **Trends on Version Control Land**. Take a look at the first post on [Innersourcing][post-1] to learn more about common challenges large organizations face and how Innersourcing can solve them. Also check out our second post, [Release Early, Release Often][post-2], to read about how and why GitLab releases monthly.
{: .note}

<!-- more -->

## What are microservices?

[Microservices architecture][micro-arch] is a way of designing software applications as smaller, independent,
cloud-based services rather than one monolithic data center. [Netflix][netflix-micro] is a good example: their
users application, movies application and ratings application are deployed independently.
Netflix has made a lot of the code behind their [microservice architecture open source][netflix-oss]. [Uber][uber-eng], [Soundcloud][soundcloud-micro], [Hailo][hailo-micro], [Amazon][amazon-micro], and [Ebay][ebay-micro]
are a few other companies that [are using microservices][companies-micro] to deliver their applications. Uber shared
a really nice narrative of their [move from monolith to microservices][uber-blog] on their blog.

## Benefits of microservices

**System-wide stability:** Using Nextflix as an example again, since moving to a microservices architecture, they have achieved much greater system-wide stability,
because API service interruptions are restricted to one service.

**Scale teams:** With microservices you can move more quickly because each app can
deploy independently of the others. Teams can operate independently. Since larger teams have more overhead (decisions, training, etc.), being able to split them up per service increases efficiency.

**Diverse technology:** Since each service is independent, you can use the best programming language and database for each respective job.

**Improved architecture:** Splitting up the application in multiple services enforces module boundaries; each application has its own responsibilities. Please note that it only helps with enforcement, in a monolitic application you can also have great module boundaries.

## Drawbacks

**Latency:** Making function calls between different services instead of in an application slows everything down.

**Distributed system:** The [first rule of distributed object design](http://martinfowler.com/bliki/FirstLaw.html) is don't distribute your objects. Distributed systems are harder to debug, reason about, and do transactions in.

**Three-step rollouts:** If you have a change that affects other services you first have to push a new version of your application, then ensure all other services start using that, and finally deprecate the old version. If it was a single application that process could be done in one step.

**The need to accommodate failure modes:** You can only increase system-wide stability if services can deal with other services being down. You will have to program this into your application. For example, if Netflix's recomendations service goes down, they can't just remove recommendations from the console. Instead they'll need to build their application to display generic recommendations instead of personalized ones.

**Infrastructure complexity:** Microservices increase the number of applications you have to deploy, monitor, and throttle. You will need to automate everything to make this work.

**Multiple projects:** Each service will need to be its own project to achieve the necessary independence. Each service will need multiple repositories, CI, CD, and issue trackers.

## GitLab and microservices

A major goal for us at GitLab is to make sure you can do everything you need to do within GitLab, with as few external integrations to deal
with as possible. This way, you don’t have to set up [CI/CD](https://about.gitlab.com/gitlab-ci/), and an issue tracker for each project and spend the time integrating them, they're all already pre-configured to use from one single UI.
You can [move issues](https://about.gitlab.com/2016/04/20/feature-highlight-move-issues/) between the projects of the different services and aggregate them with [group level milestones](http://docs.gitlab.com/ee/workflow/milestones.html).
To ensure the the right people have access to each project you can use [LDAP group sync](https://about.gitlab.com/2014/07/10/feature-highlight-ldap-sync/) and the ability to invite teams from other projects.

## When are microservices right for your team?

We think that microservices are great when your team is spending too much time coordinating.
There is no set number but when you have more than 25 backend developers, coordination becomes more challenging.
For another take on the benefits and drawbacks see [Martin Fowler's take on the trade-offs](http://martinfowler.com/articles/microservice-trade-offs.html).

Watch out for our last post of this series,  we'll share our thoughts on what industries are likely to embrace **Open Source**!

<!-- identifiers -->

[post-1]: https://about.gitlab.com/2016/07/07/trends-version-control-innersourcing/
[post-2]: https://about.gitlab.com/2016/07/21/release-early-release-often/

[amazon-micro]: http://thenewstack.io/led-amazon-microservices-architecture/
[companies-micro]: http://microservices.io/articles/whoisusingmicroservices.html
[ebay-micro]: http://highscalability.com/blog/2015/12/1/deep-lessons-from-google-and-ebay-on-building-ecosystems-of.html
[hailo-micro]: https://sudo.hailoapp.com/services/2015/03/09/journey-into-a-microservice-world-part-2/
[micro-arch]: http://martinfowler.com/articles/microservices.html#MicroservicesAndSoa
[netflix-micro]: http://techblog.netflix.com/2015/02/a-microscope-on-microservices.html
[netflix-oss]: https://netflix.github.io/
[soundcloud-micro]: https://developers.soundcloud.com/blog/building-products-at-soundcloud-part-1-dealing-with-the-monolith
[uber-blog]: https://eng.uber.com/building-tincup/
[uber-eng]: https://eng.uber.com/soa/

<!--
cover image: http://hubblesite.org/newscenter/archive/releases/2016/28/image/a/format/xlarge_web/layout/thumb/
copyright - public domain: http://hubblesite.org/about_us/copyright.php
-->
