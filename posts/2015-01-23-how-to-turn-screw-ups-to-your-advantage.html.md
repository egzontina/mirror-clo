---
title: "How to turn screw-ups to your advantage"
date: 2015-01-23
categories:
author: Marc Radulescu
image_title: '/images/stock/screwup.jpg'
---

We at GitLab believe in providing a good service to all our users, be they customers, or non-paying users.
In our attempt to support our users, we sometimes make mistakes.

In this post, I'll be discussing two instances where we at GitLab dropped the ball.
I'll go through what went wrong and what we did to address our relationship with the affected party.
Then I'll indicate how that affected our standing with that party.
In the end, I'll mention the process we've followed to address our mistakes.

<!-- more -->

## The brownout

GitLab.com is our free SaaS service.
At close to 20k monthly active users, GitLab.com is used by many of our users for production.
We always notify the community of downtimes on its [twitter account](https://twitter.com/gitlabstatus) and offer [paid email support](https://gitlab.recurly.com/subscribe/gitlab-com-bronze-yearly-20) for it.

For years now, we'd been happy to report minimal unplanned downtime on GitLab.com, with planned downtime seldom exceeding one hour.
On the 31st of July 2014 though, GitLab.com went offline for a full 8 hours, affecting the workflow of a serious number of users.

The failure happened in the night between Sunday and Monday in Dutch time, so we only caught wind of the issue in the morning.
Neither the cause nor the solution were evident though.
So despite fervent investigative work, we found ourselves 30 minutes into the call (and 6 hours into the downtime) none the wiser about what had happened.

We decided to openly admit that we did not know why GitLab.com was down, but to be transparent about our actions to figure out what went wrong.
GitLab's CEO, Sytse Sijbrandij, decided to make a [public postmortem](https://docs.google.com/a/gitlab.com/document/d/1ScqXAdb6BjhsDzCo3qdPYbt1uULzgZqPO8zHeHHarS0/edit#heading=h.p95p4f6o0twk) which we've posted on [Hacker News](https://news.ycombinator.com/item?id=8003601).
Quite the number of anonymous users joined our public google doc to get a live feed of our exploration of GitLab, with some even giving feedback on possible actions.

Ultimately, we brought GitLab.com back up, apologized to the community, and updated the postmortem file with all the process improvements we've done to make sure a brownout of this magnitude never happens again.

The Hacker News thread reached the top and kept GitLab in the spotlight for quite the time.
And feedback from the community was [overly positive](https://twitter.com/search?q=gitlab%20postmortem&src=typd) regarding our transparent approach.
We believe GitLab has garnered a lot of trust in being both open about the mistake, and quick to take action.

## Waking up at 5 AM for nothing

One of our lines of business is installing or upgrading GitLab for non-subscribers and basic subscribers.
We do this via scheduled consultancy calls.
One such scheduled consultancy call ended up not being honored on our side (i.e. halfway through the designated timeframe, one of our service engineers candidly asking on Slack if there's anyone handling it.)

Missing a scheduled call is a big deal in itself.
Missing one where the system administrator had woken up at 5 AM just so they make sure the servers are running when devops start work, that's really bad.

As soon as we realized that the customer wasn't being handled we went in, however they had already left the line.
We apologized via email and offered to have the call as soon as possible.
Afterwards, Sytse addressed an official email to them apologizing and offering to have the call for free.
Moreover, he started an internal postmortem to find out what had happened.

The postmortem turned out that some steps in the support process had confused our service engineers and needed improvement.
We wrote a follow-up to our customer detailing not only where the issue was in our process, but also the detailed steps we took to improve it.

Between the CEO apologizing and the detailed description of how we were going to improve our process, the customer - whose basic subscription renewal was due within the month - decided to offer their vote of confidence and upgrade to the standard subscription.

## Why the good vibes?

In both cases we followed the same course of action:
 - be open about the mistake;
 - take swift action to solve the issue;
 - identify what caused the problem;
 - improve internal processes in light of our findings;
 - inform the customer / user about the process improvements.

What the above does not highlight though, is one other point we're abiding to: being disciplined about our process.
After failure, make sure to review the faulty process and revise it. Iterate.
