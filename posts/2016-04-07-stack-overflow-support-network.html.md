---
title: "Customer Story: Stack Overflow"
date: 2016-04-07 16:30
categories: customer
author: GitLab
author_twitter: gitlab
image_title: '/images/unsplash/stack.jpg'
---

In this post we'll look at how [Stack Overflow] uses GitLab.

<!-- more -->

- **Industry:** Support network for programming community
- **Company Size:** 254
- **Development Team:** 30
- **Location:** Global. Stack Overflow HQ is in New York, but most developers
work remotely.

## Background Info

[Stack Overflow] is a question and answer site run by and for programmers.
It is part of the Stack Exchange network of Q&A sites.
Unlike discussion forums, this platform is all about getting answers.
The concept is simple: good answers get up-voted by the community and rise to
the top so they can be easily viewed. Users who receive positive feedback
receive privileges including the ability to vote, comment on, and edit posts.

All questions get tagged with their subject areas. Users can click on the tag
list to see if their question has already been asked by a member of the community.
Over time, users are building a library of detailed answers to programming questions.

## Getting It Right

When the team of developers at Stack Overflow set up their service for
programmers, they knew they had to get the right source control solution.
Get it right, and users would flock to the support resource; get it wrong, and
the response wouldn’t be so positive.

Stack Overflow senior developer Geoff Dalgas explains that when the team was
looking around for the best possible solution, it became clear that GitLab fit
the bill. Their initial choices of Git-web and Kiln were superseded by the
continued development and improvements in performance offered by GitLab.

Stack Overflow adopted GitLab as their primary source control. It is used
on-premises and is currently self-hosted. They have opted to use a self-hosted
chat system, as none of their preferences are integrating with GitLab at present.
As basic GitLab users, the platform does not use the integrated CI into GitLab
– they have opted for Team City.

As a Q&A network that is itself constantly growing and developing, it is
essential that it has a solution on board that enables its users to build a
library of detailed, trustworthy answers to the questions posed by professional
and amateur programmers. When asked to describe the special considerations for
software that the Stack Overflow development team must consider, Geoff Dalgas
answers succinctly: “Maintenance, reliability, and maintainability.”

## Being Part of On-Going Developments

Given that fit, function and speed are essential for the programming industry,
GitLab has become ingrained in the Stack Overflow culture. As early adopters,
Geoff’s team has been part of the ongoing developments of GitLab.
He describes the increased development time, quicker code review and easier
collaboration as being the main changes that he has witnessed.

As active contributors to open source, Geoff and his colleagues have also seen
an increase in the use of merge requests.

The developers at Stack Overflow use [LDAP integration](http://doc.gitlab.com/ee/integration/ldap.html#gitlab-ldap-integration).
The team have recently made the decision to implement [GitLab Geo](https://about.gitlab.com/2016/02/22/gitlab-8-5-released/).
They are hoping that it could be a solution to their multi datacenter
replication, but Geoff reports that analysis is ongoing and it’s too soon to
tell for sure. His colleagues feel that an improved search experience would be
a huge benefit to their work.

## Tell us your story

Is your team using Gitlab? We’d love to hear from you.
Email us at community@gitlab.com if you’re interested in sharing.

[Stack Overflow]: https://stackoverflow.com/
