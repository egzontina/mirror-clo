---
title: Release Manager - The invisible hero
date: 2015-06-25
author: Marin Jankovski
image_title: '/images/unsplash/rm.jpeg'
author_twitter: maxlazio
---

Real heroes are sometimes unknown and we can only see their accomplishments. In GitLab we have one invisible hero every month, when we have our monthly release. As you may know, we've never failed to release a new GitLab version on the 22nd of every month.

As GitLab grows, the release process becomes more complex and becoming a release manager is a more difficult, but a necessary job.

Eight working days before the next release, and we start the countdown. A new volunteer "hero" is elected by the team.

<!--more-->

## But, why is it such a challenging job?

A release manager is the person who makes sure that everything is ready for the monthly release. They follow up on every single detail and make sure that the new version is working perfectly, including all the improvements and features. They also need to delegate some tasks and make sure that the procedure is being followed.

Consider that right now, GitLab is huge. Our community dishes out around 900 commits a month on GitLab alone. Add Enterprise Edition, GitLab CI and runners, Omnibus-GitLab packages and you get several thousand changes done by hundreds of developers across projects which need to come together (and work) in one day. This is a lot of responsibility for one person.

## So, how do we manage to make it all into a single release every month?

In GitLab we have a [release directory](https://gitlab.com/gitlab-org/release-tools/tree/master/doc) for the release documents. The most powerful document for the release is called [monthly.md](https://gitlab.com/gitlab-org/release-tools/blob/master/doc/monthly.md).

Release manager tasks can be broken down into:

1. Make sure that GitLab CE, EE and GitLab CI repositories have an updated installation and upgraded guides
1. Make sure that the Omnibus-GitLab package will be ready for the release
1. Release the RC version, do QA, deploy on GitLab.com and ci.GitLab.com
1. Follow reported regressions and make sure that developers are aware/working on a fix
1. Decide which fixes can go into the release
1. Coordinate the package building
1. Make sure that the blog post contains all the necessary information
1. Do the final release
1. Decide if there needs to be a patch release
1. Coordinate patch release

A release manager volunteers to work late (or early) to get the packages out or deploy the new version to one of our services. No one is forcing you to do so, but if you don't, it will complicate the following day. This is a weakness in our process, so we need to work on improving this situation.

## History

I don't know the exact date when the release manager duty was thought off but it was [around version 6.4](https://gitlab.com/gitlab-org/gitlab-ce/commit/223070b3fe9cb302d3d47ba5a616d90bab8910fd).

At that time, we had a couple of other things that were the release manager tasks: Notify everyone of the code-freeze (nothing was merged to master during this time), enforce it and build the packages *manually*. Yes, manually. This meant connecting to all machines separately and doing few commands to initiate package building. GitLab.com had a separate repository with some custom code, so the deploy needed to be done manually too. I still have nightmares as a result of these 2 things.

As you can imagine, this made the release manager tasks very undesirable and limited to a few people. Even with all the improvements that followed, this job is still not popular.

## Improvements

Since the painful beginings of the release manager tasks, we've done number of improvements. We did a massive change to the process and made it even more continuous integration oriented than it was before. There are risks to it, but also massive gains:

1. Code freeze was removed so there is no need to watch over anyone's shoulders

1. Keeping X git repos in sync. Syncing repositories is now a one-line script where the argument is the version that is being released

1. Automatizing our release process. Omnibus-gitlab packages infrastructure got built, so only supplying the shas of the release version is enough to kick off the automatic builds on all platforms and machines

1. Infrastructure for deploying GitLab.com and ci.gitlab.com got created and they are being updated by using a few lines of commands and packages

1. The release documentation has been updated so many times that room for error is minimal (if you follow the steps closely)

You would expect that all these improvements would make the Release manager job more appealing since you get to:

* Boss around over *all* of your colleagues. This includes the project lead and the CEO. It is especially sweet when you can say NO to an unreasonable request. After all, all requests are unreasonable but your own and now you get to push that through
* You decide at your leasure when something will be included and pushed
* You are *the* boss of everything (for a period of time) because everyone says: "Hey, you are the release manager, your call"

## With all the hard work, how do we choose a volunteer release manager?

Choosing the release manager is probably one of the hardest tasks.

During our team call, the release manager for the previous release mentions the subject of selecting a new release manager.

At that exact moment, there's silence, cameras and mics start breaking down, people forget the whole English language, there is always someone at the door so you need to open it and lots of faces are just looking around the room.

After a few minutes of silence, decision is made, but mostly because we are all friends and we don't want to see a colleague suffer for another month.

We've tried improving the desirablity of this task by making procedures easier, but that is still a challenge.

At some point I've asked what kind of reward we could put forward to make people happy to volunteer, but there are no good ideas yet.

My ideas where limited to:

* Material reward: a gift might be OK for some people, but others have no need for things. In this case we could publicly thank them and acknowledge their work.

* "Spiritual" reward: We do say "thank you" to the RM a lot, but this gets spent. Tweeting the name of the release manager might work as a recongnition for some, but I am afraid that it won't work for introverts in our team. Being more public might also yield more work for them.

* Buying a beer or cocktail: This feels like something that would be appreciated, but it would only work for a few employees, since we are a *very* remote company. Maybe a beer voucher could be sent.

With that I was out of ideas. This blog post is an attempt to say a thank you to all the release managers. You know who you are and you are a true invisible hero for accomplishing the tasks to make everything go out on schedule.

Do you have any ideas?

### Release manager - my hero.
