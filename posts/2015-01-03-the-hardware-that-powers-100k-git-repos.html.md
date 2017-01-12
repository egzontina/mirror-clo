---
title: "The hardware that powers 100,000 git repositories"
date: 2015-01-03
author: Job van der Voort
image_title: '/images/stock/hardware.jpg'

---

Want to host your public and private repositories somewhere for free?
You can on GitLab.com, where we have been hosting a single instance of GitLab for a while now.
Almost 20,000 people make active use of this to host their
repositories. The 100,000+ repositories that these people use are served by a single server.

<!-- more -->

## A single server

Before, GitLab.com was hosted on Amazon's largest instance.
But as the amount of users grew, so did our Amazon bill.
On top of that, we were limited in options of vertical scaling and were CPU bound.
We had to explore alternatives to AWS.

100k repositories take up several terabytes, so storage capabilities are important.
Since we use git, the storage needs to be a single filesystem,
rather than object storage (such as S3).
We want to be able to expand storage with ease.
Furthermore, thousands of people pushing and pulling their code will put a strain on the CPU.
Having many CPU cores available can make a big differences in times of high load.

It turns out that using our own servers was by far the cheapest option.
Considering we're bootstrapping GitLab
and as cheap Dutchmen (Sytse, Jacob, Job), this made the choice easy.

![htop on GitLab server](/images/stock/htop.png)

And so,  we currently have two (one active) of these servers running GitLab.com:

- server model: HP DL180 G6 (reconditioned, this model was introduced in 2009)
- processors: 2x X5690 (24 cores in total)
- 32GB RAM
- 12x 2TB HDDs, (2 for root volume in RAID 1, 10 for storage in RAID 10, ext4 filesystem)

We actually started with a total of 16 cores,
but replaced the CPUs to decrease CPU-bound loading.

## Falling and Failing over

Moving away from Amazon meant that we no longer could use AWS' features.
In case a server dies, we need to be able to failover.

We used DRBD to create one primary and one slave server.
One of the servers is active as application server at a time.
If something goes wrong, we tell DRBD to promote the other server to primary.

Our DRBD tooling that we've built for this is made available to our
[subscribers](https://about.gitlab.com/pricing/).

## Scaling further

GitLab.com runs well on its current hardware, but is growing ever faster.
Expanding the current hardware would be expensive and parts are not easy to get by.

In the future, GitLab.com will be hosted on Amazon AWS again.
This will allow us to scale horizontally more easily.
On top of this, Amazon recently announced 10+TB EBS volumes, which will make migrating easy.
