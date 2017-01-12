---
title: "GitLab Infrastructure Update"
author: Pablo Carranza
author_twitter: psczg
categories: gitlab
image_title: '/images/blogimages/infrastructure.jpeg'
description: "Hear how we're working through infrastructure challenges as we scale."
twitter_image: '/images/tweets/infrastructure-update.png'
---


As Infrastructure Lead, my job is to make [GitLab.com][gitlab] fast and highly available. 

Lately, it's been a challenge. Why? We are hitting our threshold where scale starts to matter. For example, over 2,000 new repos
are being created during peak hours, and CI runners are requesting new builds 3,000,000 times per hour.
It's an interesting problem to have. We have to store this information somewhere and make sure that 
while we're gaining data and users, GitLab.com keeps working fine. 

A large part of the issue we're running into as we scale is that there is little or no documentation 
on how to tackle this kind of problem. While there are companies that have written high-level posts, almost none of them
have shared **how** they arrived at their solutions.

One of our main issues in the past six months has been around storage. We built a CephFS cluster to tackle both the capacity and
performance issues of using NFS appliances. Another more recent issue is around PostgreSQL vacuuming and how it affects performance locking up the database
given the right kind of load. 

As [outlined in our values][values], we believe we have a 
responsibility to document this so other companies know what to do when they reach this point.
Last Thursday, I gave a GitLab.com infrastructure status report during our [daily team call][team-call]. 
Watch the recording or download the slides to see how we're working through our challenges with scaling. 

<!-- more -->

## Recording & Slides

### Recording 

<figure class="video_container">
  <iframe src="https://www.youtube.com/embed/kN-HcObb9zo" frameborder="0" allowfullscreen></iframe>
</figure>

<br>

### Slides

<figure class="video_container">
  <iframe src="https://docs.google.com/presentation/d/11rCsJM41WAETPWqtWgfIxgfPRBQB4m037aZpgsGpzkk/embed?start=false&loop=false&delayms=5000" frameborder="0" width="1280" height="749" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>
</figure>

<br>

<!-- identifiers --> 
[gitlab]: https://gitlab.com/
[team-call]: https://about.gitlab.com/handbook/#team-call
[values]: https://about.gitlab.com/handbook/#values

