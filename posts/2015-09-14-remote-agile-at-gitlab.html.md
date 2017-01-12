---
title: "Remote Agile at GitLab"
date: 2015-09-14
author: Job van der Voort
author_twitter: Jobvo
image_title: '/images/unsplash/agile.jpeg'
---

Every month on the 22nd a new version of GitLab is released. It always
includes major changes, with features, bug fixes and performance improvements.
We haven't missed a single month since our inception.

We are completely remote, save for the office in San Francisco that not a single
developer frequents (a 10,000km commute is a bit much for most). We do not have
predefined teams and almost everyone works independently (i.e. without someone telling
them what to do).

We do not practice any specific agile methodology, but meet the principles
of the [agile manifesto](http://www.agilemanifesto.org/iso/en/principles.html) quite well.

This is a start in describing the workflow that we've established over
the past year at GitLab, as it seems to work for us and might for you. It's
lightweight and self organizing. It might or might not scale.

<!-- more -->

## Incoming issues

A large part of everything we build in terms of features is based on feedback from the
community and customers.

When a request comes in from a customer (through support or sales usually),
the person receiving this request creates an issue to discuss it.
They are responsible for mentioning relevant parties. For most features that
is the product manager, CTO, and any developers or other people that might be
interested in this feature.

Next, anyone with an opinion responds to the issue. This is often done in direct
response to others, including more people in the discussion if necessary. The
point is to reach some form of consensus. Once this has been reached, the issue
is scheduled for an upcoming release (e.g. 8.1 or 8.2). Anyone can do this based
on the information in the issue and on how full the upcoming releases are versus
how important this is.

Everyone that has participated in the conversation will be updated with any status
change. Therefore anyone can freely schedule things. If someone disagrees, they'll
speak up.

### Known issues

It's very hard to schedule things. We simply do not have a good way to estimate
whether something will be doable, besides estimating based on previous releases.
However, we prefer the scheduling to be hard over adding overhead with estimating
weights and velocity for the team. We might change our minds on this.

## Working and Prioritizing

A developer can pick up any issue at any time they're working.
They simply assign themselves, marking it as "Ongoing" in [GitLab's Milestone
View](https://gitlab.com/gitlab-org/gitlab-ce/milestones/13).

Some issues have a clear owner in terms of knowledge and ownership of that part
of the code. Usually this developer has already been active in the issue. The
developer likely picks these issues. This is a self-organizing process.

A small part of the issues is promised to a customer. This means that we told the
customer: "Feature X will be done in release Y". We always intend to keep our
promise, so these issues get prioritized by everyone.

There is also a general guideline to prioritization of work. This does not
work as a hard rule and also depends on your skills and responsibilities:

1. Emergency issues
1. Security issues
1. Data integrity (not losing data)
1. Availability of GitLab.com
1. Subscriber questions
1. Regression issues
1. Consultancy work
1. Promised features
1. Growth efforts
1. Other work

Find this [in our handbook](https://about.gitlab.com/handbook/#gitlab-workflow).

### Known issues

People can choose their own issues, which can result in a situation where
issues that are not 'fun' are not being picked up. This can be solved with
proper handling of overflow issues, as described below.

## Overflow

Overflow of issues is something that happens every month. Meaning, not all issues
assigned to a release get completed or worked on.

In the past, we would simply move everything to the next milestone. This 'waterfall'
workflow didn't work, as unpopular things would get dragged on for many releases.
Nowadays, we (I) go through all leftover issues and investigate why they didn't get
done and what we can do with them.
This often results in dropping the issue as it's no longer relevant or moving it
up to a future release and pinging a developer to take ownership of it.

Managing overflow issues is a very hard balance between capacity and process.
Mostly we blame a lack of developer capacity with overflow issues
([we're hiring!](https://about.gitlab.com/jobs/)).
With every release, we try to reflect on what could have been done better.

For example, most recently Douwe and I proposed a different model to schedule
issues to prevent too many promised issues. Most developers had strong opinions
on this, which spawned this article. We ended up not making changes, choosing
speed and flexibility over process, but gained insight into how people feel about
the status quo.

## Openness, Independence and Responsibility

As a developer you're required to operate independently and make decisions.
By making your own decisions, it reduces process overhead and unnecessary
communication.

It's your responsibility to report those decisions in the issue that you're working
from. This is the core of our workflow. People that were previously active in the
same issue, will receive your updates and thoughts without disturbing one another.
If there is an issue, they will respond in the issue. The whole process is asynchronous
and self-organizing.

Lastly, [we're open](https://about.gitlab.com/2015/08/03/almost-everything-we-do-is-now-open/).
This is something that runs deep within GitLab. To be able to work with the community,
with our customers, we have to work in a way that everyone can contribute equally.

We think this works well for everyone, but are always looking to improve things.
As we're growing very fast, we're not sure whether this will scale.

How does your workflow look and why does it work for you?

## Related Reads

- [How we use GitLab to build GitLab](https://about.gitlab.com/2015/07/07/how-we-use-gitlab-to-build-gitlab/)
- [The Release Manager](https://about.gitlab.com/2015/06/25/release-manager-the-invisible-hero/)
- [The Remote Manifesto](https://about.gitlab.com/2015/04/08/the-remote-manifesto/)
