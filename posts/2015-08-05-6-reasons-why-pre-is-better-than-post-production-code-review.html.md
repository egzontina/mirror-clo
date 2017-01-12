---
title: "6 reasons why pre is better than post production code review"
date: 2015-08-05
author: Job van der Voort
author_twitter: Jobvo
image_title: '/images/code.png'
---

Code review is very important. You don't want to run the risk of [technical debt].
Actually doing code review is another matter. Besides the variety of tools and tricks
for the act of code review, the timing is vital.

[Quora published a great article] about maintaining velocity in projects.
The article is really great but we think that their post production code review
is timed wrong.

<!-- more -->

## Requirements for Early Review

The Quora article mentions two things that can go wrong if you do a pre production
code review:
If you do early code review it has to be fast or it'd undo some of the advantages
and slow down your release cycle. An easy fix for this is to not wait for particular
people, rather just have a number of required reviewers (you can do this with
[merge request approvals] or just agree on something internally).

Second, the big picture has to be in scope for you and your reviewers. It's possible
that a larger piece of code needs refactoring. If this is the case,
do it within the merge request or schedule the refactoring as a separate issue.

Here, we give you six good reasons why you should review code before it's being
deployed / released / merged, rather than doing code review on code that is
in use already.

## 1. It's still fresh

If you get feedback on something that you recently worked on, you're
likely to have the context and structure in mind of that piece of code.

Production code that is reviewed much later on will require you to do another
deep dive into code that you might have not touched in a while. This is inefficient
and sets you up for failure, as the context is never as clear as it was while you
worked on it.

## 2. Less Resistance to Change

When your code is running in production for some time, seemingly doing what it
should, it'll be harder to convince you to change it. You will be more resistant
to changes suggested by your colleagues.

With unproven code the "it works, why change it?" argument is much harder to make.

## 3. Higher Focus on Quality

As you will be less resistant to code that is not running successfully yet,
your reviewers will be more insistent on the functionality and quality of the
code. The code has not proven itself yet, so you can't assume it works,
inspiring more thorough review.

## 4. Catch mistakes before Production

This seems obvious, but if you review before code going live, there will be
much less issues on the live code. In turn, this means your software is more
reliable and you'll fight less with emergency bug-fixes and spend more time
writing new features.

## 5. You Must Review

Skipping code review on already deployed code is easy. You just don't do it.

However, if you use early code review, you can easily set up a workflow
that forces code review. For instance, with [GitLab's Merge Request Approvals],
you can require any N of your colleagues to approve a merge request before it's
merged into the target branch.

This way code review can never be skipped, with all the benefits of that.

## 6. Small Reviews > Large Reviews

We observed that smaller reviews gather much more comments per line of code,
than large reviews.
Typically code that is already in production is reviewed by reviewing piece of
functionality, this tends to be larger than a change.
This means that you can expect a more thorough review
on code that is not merged yet, over code that is already live just by the
line count of the review.

## How do you review?

As we're always looking to improve code review in GitLab, we're very curious
to hear what you do with your code, how you review it in your team and how
we can improve GitLab to support better code review.
Let us know in the comments below.


[technical debt]: https://en.wikipedia.org/wiki/Technical_debt
[merge request approvals]: https://about.gitlab.com/2015/07/29/feature-highlight-merge-request-approvals/
[GitLab's Merge Request Approvals]: https://about.gitlab.com/2015/07/29/feature-highlight-merge-request-approvals/
[Quora published a great article]: http://engineering.quora.com/Moving-Fast-With-High-Code-Quality?share=1
