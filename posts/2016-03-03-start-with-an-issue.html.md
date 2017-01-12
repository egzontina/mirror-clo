---
title: "Always start with an issue"
date: 2016-03-03 10:00
categories: workflow
author: Heather McNamee
author_twitter: nearlythere
image_title: '/images/unsplash/stars.png'
---

“Always start with an issue” says [Job][job], VP of Product here at GitLab.
Before you begin anything else, summarize your ideas in an issue and share it.
It’s such a simple rule, but the impact is huge.

In this post we'll focus on issues for feature proposals specifically,
but the rule applies in any case, no matter what kind of project you're working on.
We say “start” with an issue and not “create” an issue, because one might already exist.
Make sure to search in All issues (open and closed) to see if your idea has been proposed already.

 **Webcast soon!** Find out more about making the most of GitLab to collaborate
 on your projects, join us for our GitLab Intro
 [webcast on GitLab Workflow][webcast], Thursday March 10th.

<!-- more -->

### GitLab is a discussion about software

The benefits of collaboration start at the point of [making an issue][docs-issue].
By making an issue, you get your ideas out there, and this allows your
collaborators to have their say early in the process.

Non-programmers think that programmers are constantly tapping away at their
keyboards on code.
In fact software development is more like a discussion, and it’s a more
collaborative experience than it is a solitary one.

The tools GitLab provides make it easier to manage that discussion,
and keep the flow of conversation moving.

### An example of software as a discussion

Let’s look at an example discussion as it took place around a specific feature
proposal.
Of course not every aspect of collaboration is recorded on GitLab.
We also use text chat and we pop open a quick video chat sometimes.
However, the issue tracker does give us insight into the collaborative experience.

In his recent [blog post about the Todo feature][todo blog], GitLab developer
[Douglas][Douglas] told the story of how the Todo feature came to be in GitLab 8.5.

The [original issue][Todo issue] was posted 6 months before coding began.
The targeted milestone was moved from 8.4 to 8.5 during that time.
The discussion continued for four months until the description was simplified.
One of our designers, Andriy, came up with a second design reflecting the major decisions.
The title changed seven times until finally it’s renamed Todos.
There were 30 participants marked in the issue, but some may have just been
watching, or may have taken other actions such as adding a label.
In total, 13 people added to the discussion.

At one point early on, Job summarized [the next actions to take][next actions] and assigned them:

- formal proposal (Job / Darby / other people)
- mockups (Job)
- design (Andriy)
- implementation (any dev) (*which turned out to be Douglas*)

Implementation is a *final* step.

Let's consider the lifetime of this issue which started 174 days before the final release.

The task was assigned to Douglas only on Feb 2nd, with 20 days left to that milestone.
Douglas spent 11% of lifetime of this issue on implementation.
He didn't create the merge request until 7 days before the release.
That means over the course of the issue from start to close,
*only 4% of the lifetime of the issue was spent "coding".*
Douglas even spent the first week of implementation reading code and writing a
proposal for how he would implement the feature.

It’s in [the merge request][the MR] that Douglas and Douwe worked on refining edge cases.
They worked out how it would get done according to the intention of the original issue.
Each day, Douglas would make a number of commits, and then Douwe would give him feedback.
Again, it's further evidence that the bulk of work is in discussion and communication.

Of course, the Todo issue might be an extreme case, but it does highlight
that software development is a discussion.
Git commits themselves are just one aspect of the work software developers do.
That is why tracking "commits" as evidence of productivity gives an inaccurate
metric of software development productivity.

## What happens if you don’t make an issue first?

There’s a danger with spending a lot of time on work before sharing the idea,
like some kind of [Gollum][gollum], working on your own.
As you develop it, and polish it, you run the risk of becoming precious about it.

When you present your polished prize, you risk spending more time justifying
your decisions, such as why you didn’t do X or didn’t account for Y.

By starting with an issue you also avert a number of risks which can introduce problems later on.

- You may not know everything there is to consider.
- There may be parts of the system you aren’t familiar with.
- There may be limitations or possibilities you’re not aware of.
- There may be factors for users you may not know.
- There may be work going on in a parallel effort which relates your idea.

The issue opens the conversation, and you gain the benefits of collaboration from the start.

## What's contained in the initial issue for a feature proposal?

In the [contribution guide][contribution guide], we call these "feature proposals"
rather than "feature requests".
This is a subtle but important nuance.

A 'request' puts the onus on someone else to "fulfill" a request.
Whereas a 'proposal' puts the onus on the initial person writing the issue.

> Please keep feature proposals as small and simple as possible,
complex ones might be edited to make them small and simple.
> For changes in the interface, it can be helpful to create a mockup first.
> If you want to create something yourself, consider opening an issue
first to discuss whether it is interesting to include this in GitLab.

The Todo issue started with a [long description][original proposal] which was
later marked as "too complex".
Thankfully it was kept and we can compare it.

## Are there times you don’t start with an issue?

Sure! When I’m working on something small, corrections or typo fixes, I don’t make an issue.
Job said he also doesn't always make an issue.
"For super small changes that don’t need to be discussed, for spontaneous outbursts
of code or creativity or when you just can’t be bothered," Job said.
We have to be practical, as with most rules, there are reasonable exceptions.

The [Merge Request (MR)][mr] has everything we need anyway.
MRs have the same collaboration tools as issues.

- Comments
- Labels and Milestone
- Notifications
- References
- Todo notifications

So this means I can still continue the conversation.
Of course, I keep the MR in ["WIP" mode][wip] (work in progress) so it doesn't
accidentally get merged. Then we're free to collaborate.

## GitLab workflow

So you've started with an issue, what happens next?
In our next webcast on March 10th, we'll dig into a typical GitLab workflow.
This will take you through the steps of making an issue, merge requests, and
using tools in GitLab for cross-referencing and keeping your issue tracker
organized with labels and milestones.

- Date: Thursday, March 10, 2016
- Time: 5pm (17:00) UTC; 12pm EST; 9am PST
- [Register here][webcast]

Can't make it? Register anyway, and we'll send you a link to watch it later!

[gollum]: http://www.imdb.com/character/ch0000152/quotes
[docs-issue]: http://doc.gitlab.com/ce/gitlab-basics/create-issue.html
[mr]: http://doc.gitlab.com/ee/gitlab-basics/add-merge-request.html
[todo blog]: https://about.gitlab.com/2016/03/02/gitlab-todos-feature-highlight/
[wip]: http://doc.gitlab.com/ce/workflow/wip_merge_requests.html
[webcast]: http://page.gitlab.com/mar-2016-gitlab-introduction.html
[Job]: https://twitter.com/Jobvo
[Douglas]: https://twitter.com/dbalexandre
[Todo issue]: https://gitlab.com/gitlab-org/gitlab-ce/issues/2425
[the MR]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2817
[original proposal]: https://gitlab.com/gitlab-org/gitlab-ce/issues/2425#old-deprecated-proposal-too-complex
[next actions]: https://gitlab.com/gitlab-org/gitlab-ce/issues/2425#note_2070496
[contribution guide]: https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CONTRIBUTING.md#feature-proposals
