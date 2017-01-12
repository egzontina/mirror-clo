---
title: "GitLab switches to Piwik analytics to free the JavaScript"
date: 2015-11-27
author: Sytse Sijbrandij
author_twitter: sytses
image_title: '/images/unsplash/water.jpg'
---

Back in May of this year, we ensured that our [Enterprise Edition JavaScript was free software](https://about.gitlab.com/2015/05/20/gitlab-gitorious-free-software/).

But GitLab.com still loaded the Google Analytics JavaScript code, which is not free software.

Recently we switched to using the on-premises open source [Piwik software](http://piwik.org/).
This ensures that you only download free software to the client when using GitLab.com.

We want to thank Mike Gerwitz, a [Free Software](https://www.gnu.org/philosophy/free-sw.html) hacker and activist,
and author of [GNU ease.js](https://gnu.org/software/easejs) for helping to make this
happen and for his flexibility in working with us.

Please note that we still use Google Analytics and other tracking code on our static website
[about.gitlab.com](https://about.gitlab.com/).
