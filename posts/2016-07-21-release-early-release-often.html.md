---
title: "Release Early, Release Often"
categories: concepts
author: Sid Sijbrandij
author_twitter: sytses
image_title: '/images/blogimages/release-early-release-often-cover.jpg'
twitter_image: '/images/tweets/release-early-release-often.png'
description: "Let’s explore the rise of releasing early and often!"
---

Another trend that keeps popping onto the radar is a continuing **reduction in time between deploys**. In this post we’re looking at what that means and why it’s happened.

**Note:** this post is the second of the series on _Trends in Version Control_. The first one explored _[Innersourcing][part-1]_.
{: .note}

<!-- more -->

Software development has changed a lot over the decades. Development practices have shifted from traditional waterfall to agile development and now to even faster deployments. Applications used to be deployed every 6 months. There would be one big deploy. Teams would be briefed in advance. Then on release day it’s all hands on deck to ensure the release goes as planned. While two releases a year seems frequent compared to the days when we used to wait several years for new product and operating systems, people are still moving away from biannual releases and opting for more frequent release cycles.

## The logic behind deploying early and often

One of the biggest issues with carrying out a large deployment once or twice a year is that it creates a bottleneck and you end up with a coordination problem between all the features you want to release. If everything is ready to go but one small feature is delayed, then everything is delayed. Also let’s say that there is a very real off chance that there is a bug in the deployment that you’ve spent 6 months working on. You deploy it and realize there is a bug; however, your deployment contains so many lines of code that it won’t be easy to spot the exact thing that caused the bug.
 
Everything will not be perfect when it’s sent out the door the first time. The early-and-often deployment mindset is about shifting away from full-featured perfection to smaller slices of customer value. Everything is thought of in terms of iterations, or drafts; basically, it is a permanent work in progress, always getting better.
 
If there’s a bug, it’s not nearly as a big of a deal as in the days of the annual or biannual deployment, because it’s much easier to isolate what caused it and to fix it, and you can release a fix almost immediately. If a particular feature isn’t ready, that won’t hold up the release; that feature can just be released next month.

## Moving to time-based releases

To make releasing early and often possible, teams have started using [time-based releases] versus feature-based releases. Moving to time-based releases means no more waiting for features to be ready; instead you only merge features that are ready at the time of your release. At GitLab, we stick to time-based releases, also does  [Docker], [Ubuntu] and [GNOME]. Some may even say we’ve taken them to the extreme. Since 2011, we always ship on the 22nd of every month. Then any patches are released when they are ready. When we first started doing time-based releases, it was difficult to stick to them. Here’s some advice on how you make the move.

- Decouple features so you don’t have to hold the deploy for one feature
- Focus on getting smaller features out the door when the first iteration is usable 
- Adopt time-based releases and ship on that date 
- Patches can be released when they are ready
- Reduce the time between releases by getting from issue to deploy quicker

## Key takeaway

The longer you wait between releases, the more attractive it can be to hold your release to wait for the next feature. However, you should stick to time-based release. Keep in mind with time-based releases you also have to shorten the time between releases too. The reality is that the idea of the perfect software release is now obsolete, because technology advances too quickly for that to ever be possible, and that’s a good thing. Perfection is no longer the point: usability, fast turnaround, and overall development efficiency are far more important.

Want to read up on more trends? Check out our last post on [Innersourcing][part-1].

<!-- cover image: https://unsplash.com/photos/r-EecLdRRww - resized and compressed -->

<!-- Identifiers, in alphabetical order -->

[DOCKER]: https://github.com/docker/docker/wiki
[GNOME]: https://wiki.gnome.org/ReleasePlanning/TimeBased
[part-1]: /2016/07/07/trends-version-control-innersourcing/
[time-based releases]: http://www.infoworld.com/article/2638146/open-source-software/time-based-release-methodologies-and-open-source-communities.html
[Ubuntu]: https://wiki.ubuntu.com/TimeBasedReleases
