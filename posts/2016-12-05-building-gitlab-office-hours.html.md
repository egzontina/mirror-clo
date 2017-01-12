---
title: "Building GitLab Recap & Recording"
author: Erica Lindberg
author_twitter: EricaLindberg_
categories: inside GitLab
image_title: '/images/blogimages/facebook-open-office-hours-webcast.png'
description: "A conversational take on what's new from GitLab 8.14"
twitter_image: ''
---

{::options parse_block_html="true" /}

Following the release of [GitLab 8.14][gitlab-8-14], VP of Product [Job van der Voort][job-twitter]
hosted a YouTube live stream to discuss how our team is working to realize GitLab's vision and
some of the awesome features we just released. Check out the video and highlights below.

<figure class="video_container">
<iframe src="https://www.youtube.com/embed/njP8Wvp45o0" frameborder="0" allowfullscreen="true"> </iframe>
</figure>

## Highlights

### 1:07 GitLab's Vision

"When we [announced our series B round in Septmeber][master-plan], we said, "Ok, what we're going to do is we're going to try
and ship the whole [GitLab flow][gitlab-flow], going from idea all the way to production and we're going to ship it by the end of the year."

### 2:42 What is Review Apps?

"When you do a merge request, let's say you have some change you want to make on the website.
In the past, you would create a merge request and then somebody would check out the code; maybe
you have [continuous integration][ci-post] running automatically to see if those tests past.Now, if
you wanted to actually *see* the changes, and play around with them, you would still have to
checkout the branch for the merge request locally and run it to your local development environment.

With [Review Apps][intro-ra], what happens is that rather than you having to do anything,
on every single merge request we automatically create a new envionment. In that environment,
we run a full, live environment."

### 4:57 Time Tracking Beta released for GitLab Enterprise Edition

"What you can do with GitLab 8.14 Enterprise Edition is you can set - for each issue
that you're working on - an estimate and you can set how you are spent your time.
You don't even need to do this all at once. You can just set an estimate at the beginning,
and as you spend time, you can just type a comment with a slash command for time spent."

### 7:04 Mattmost Chat Commands

"As the whole world started hanging out in chat, we wanted to bridge the gap
from chat to GitLab. In GitLab 8.14, for the first time we released chat slash
commands."

### 8:50 But wait, there's more

"There's a few small feautures that we added that I think are extremely cool."
(Seriously, go find out!)

### 10:23 Ask me anything

10:38 Is there a mobile handbook of GitLab for the Kindle?

11:02 What are your thoughts on the short term possiblities of NLP, chat,
Conversational Development, and local development data sets?

12:38 How do you decide what to work on each release?

15:29 Feature proposal to improve labels and issues

18:40 What kind of data do you receive from on-premise GitLab instances? What kind of
data insights can you obtain from this group of users?

21:22 Are there any downsides of only planning a few months ahead?

## Upcoming Live Streams

![Inside GitLab](/images/blogimages/facebook-inside-gitlab-webcast-ad.png)

## 1. Why We Chose Vue.js

[Watch the recording][vue-js-recording]

A couple of months ago, [Jacob Schatz][jacob-twitter], Front End Lead at GitLab, published a post
detailing [why we chose Vue.js][why-vuejs-post] as our JavaScript framework. Since,
this post has spurred tons of conversation on the topic. To faciliate the conversation
further, GitLab Front End engineer Phil Hughes presented a front end update
and host a Q&A session along with Jacob.

## 2. Monitoring Distributed Systems with Prometheus

[Watch live][infra-webcast] on **December 14 at 9am PT/5pm GMT.** 
[Sign up to receive a reminder and the recording.][infra-lp]

Infrastructure Lead [Pablo Carranza][pablo-twitter] will give a behind-the-scenes
look at GitLab's Prometheus set up, explain how we plan to ship Prometheus with
GitLab CE, and give a tutorial on how you can set up your own dashboard.
A live chat Q&A will follow the presentation. See more details and sign up for
a reminder [here][infra-lp].

For more information on the topic, read Pablo's blog post on [how we knew it was time to leave the cloud][bare-metal-post].

## 3. Designing GitLab's User Experience with UX Lead Allison Whilden

[Watch live][ux-webcast] on **December 15 at 10am PT/6pm GMT.** [Sign up to receive
a reminder and the recording.][ux-lp]

User experience (UX) affects every interaction a user has with a product. Because
of this, it can literally make or break the adoption of a website, or application.
UX designers have a really big job to do as they dig into the who, the what,
the why, and the how of essentially everything that happens within a platform.

How does GitLab's UX team work to solve the challenge of creating an application
that has so many different types of users and releases a new version of its
product every month? Join GitLab's UX Lead, Allison Whilden, and her team, as
they discuss their process, the big challenges they face and how they look to solve them.

<!-- identifiers -->

[bare-metal-post]: https://about.gitlab.com/2016/11/10/why-choose-bare-metal/
[ci-post]: https://about.gitlab.com/gitlab-ci/
[gitlab-8-14]: /2016/11/22/gitlab-8-14-released/
[gitlab-flow]: https://docs.gitlab.com/ce/university/training/topics/gitlab_flow.html
[8-14-webcast]: https://page.gitlab.com/20161124_ReviewAppsWebcast_LandingPage.html
[frontend-webcast]: https://www.youtube.com/watch?v=ioogrvs2Ejc
[infra-webcast]: https://www.youtube.com/watch?v=WzAzm0C15W8
[infra-lp]: https://page.gitlab.com/20161207_PrometheusWebcast_LandingPage.html
[intro-ra]: /2016/11/22/introducing-review-apps/
[jacob-twitter]: https://twitter.com/jakecodes
[job-twitter]: https://twitter.com/Jobvo
[master-plan]: https://about.gitlab.com/2016/09/13/gitlab-master-plan/
[pablo-twitter]: https://twitter.com/psczg
[ux-webcast]: https://www.youtube.com/watch?v=Lxy1jET5pww
[ux-lp]: https://page.gitlab.com/UXLiveStream_LandingPage.html
[why-vuejs-post]: /2016/10/20/why-we-chose-vue/
[vue-js-recording]: https://www.youtube.com/watch?v=ioogrvs2Ejc
