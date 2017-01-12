---
title: "7 Git personalities, which one are you?"
date: 2015-01-27
categories:
author: Job van der Voort
image_title: '/images/git_personalities.jpeg'
---

Working on an open source project, we're so lucky to receive many merge -and
pull requests. Not unlike dating, we see a number of different _git personalities_.
Do you recognize yourself or one of your colleagues in one of them? Let us know in the comments
or tweet about it with #gitlab.

<!-- more -->

## 1. The Build Breaker

> Oh this is a small change, I'll just push it to master..

We all do it. A small change, preferably at the end of the week, it's not
going to hurt anyone..

How wrong you are. You just broke the build for everyone
else. Either you'll have to fix this yourself quickly or you're leaving your
team to clean up your mess.

### Fixing the breaker

Run relevant and fast tests locally, always work with merge requests and only merge when the build
passes.

## 2. The Repeater

> ```
> bf30a5b - cool new feature
> dfd934s - cool new feature
> 98dfjek - cool new feature
> ```

If git history was like actual history, the repeater's history books would only
contain only a single sentence, repeated ad infinitum. The repeater repeats a single
sentence with every commit. To know what a Repeater did, the SHA tells you
as much as the commit message.

### Fixing the broken record

Write clear commit messages that highlight the _intent_ of the commit.
This makes it easy to navigate through git history, to judge commits
and find potential sources of problems.


## 3. The Wipper

You thought you were almost done and created a merge request, but still had to
make a few more changes. Maybe while making those changes, you could refactor
a bit more. And possibly improve the alignment in some other places and before
you know it, your merge request is open for more than a month.

If this sounds like you, you might be a Wipper. The Wipper leaves their merge
requests on WIP forever. Ask yourself:

> Do you believe that your work will ever stop being in progress?

### Merging the Wip

Try to follow test-driven development. Start with high-level tests and go from
there. When those tests pass, you're done. Stop it. Ask someone to review and
merge it and start with something new. Progress is many small steps.

## 4. The Premature committer

> ```
> bf30a5b - add capital
> 9d5550a - add missing period
> 179c001 - remove 'the'
> 983hfk2 - remove trailing space
> ```

Young premature committers save their reports every sentence. Growing up
with the magic of git, they took it one step further and commit every singly
tiny change.

Premature committers and rebasers are natural enemies and are known to
annoy one another. Don't put them in the same team if you can prevent it.

### Squashing the premature committer

Let's be honest, premature committer, you don't really push every commit to
the remote, do you? If not, then you win nothing by committing every single change!

If that doesn't wake you up, you should know that the next remedy is rebasing..

## 5. The Rebaser

Adding a new import utility to an open source project? UI, tests, back-end
all in place? Awesome! In one commit? Not awesome.

You probably mean well, Rebaser. You write beautiful code and you know some
git-fu. But remember that with great power comes great responsibility:
If your feature breaks it'll be more likely to be stripped out in its entirety
as a single commit, rather than having someone go through your history to see
where it went wrong.

### Grounding the Rebaser

You're probably forgiven. Most open source projects welcome you, but
keep your merge requests reasonable. We use git for a reason.

## 6. The Merger

> ```
> 00fd402 - Merge branch 'master' into 'feature_x'
> 34jkdi9 - Merge branch 'master' into 'feature_x'
> svc98u2 - Merge branch 'master' into 'feature_x'
> ```

As the Merger, you worked really hard on that new feature. At night or during
lunch breaks: where everyone is being paid for this, you are not. That comes
with a cost, you start to run behind on changes and the easiest solution?
Just merge in master!

The Merger's merge request will merge, that's for sure, but it's not pretty.

### Cancelling the Merger

Keep your merge requests small and only start on what you can actually finish.
Only merge when needed. Not even before the merge request.
Just make sure it merges cleanly.

## 7. The Denier

The Denier is the evil twin of the Build Breaker.

But really, the tests were all green on your machine! It only broke after
someone else did a commit! Or even worse: the failing test is not related to
your code!

Sure, Denier, sure. We'll see what `git bisect` tells us..

### Admitting being a Denier

You are responsible for more than your contribution. You are responsible for
the healthy continuation of the project. Show you responsibility, be proud
to be solver of problems, not a creator of issues and fix those failing tests.
Everyone will like you a little bit more.
