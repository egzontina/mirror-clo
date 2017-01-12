---
title: "GitLab is open core, GitHub is closed source"
author: Sid Sijbrandij
author_twitter: sytses
categories: press
image_title: '/images/unsplash/sailing-5.jpg'
---

Disclosure: I'm the CEO of GitLab and we compete with GitHub.

We think of ourselves as an open source company. But today paxcoder on Hacker News rightly [remarked that calling it an open core company is more accurate](https://news.ycombinator.com/item?id=12129626).

We ship GitLab CE which is open source and GitLab EE that is closed source. We try to be [a good steward of the open source project](https://about.gitlab.com/about/#stewardship). GitLab EE is proprietary, closed source code but we try to work in a way similar to GitLab CE: the [issue tracker](https://gitlab.com/gitlab-org/gitlab-ee/issues) is publicly viewable and the [EE license](https://gitlab.com/gitlab-org/gitlab-ee/blob/master/LICENSE) allows modifications.

When we mention that GitLab is available in an open source edition people frequently ask ["Isn't GitHub open source?"](http://stackoverflow.com/questions/24254324/is-github-com-source-code-open-source). I understand the confusion between open source hosting and open source software. The hosted service [GitHub.com](https://github.com/) is free for open source projects and it has fundamentally improved open source collaboration. But the software GitHub's service is based on is closed source.

<!-- more -->

At the end of [a presentation in Spanish](https://vimeo.com/62219734) at RubyConf Argentina in 2012 ([our English translation](https://gitlab.com/snippets/22853)) you see someone in the audience ask why GitHub isn't open source. The presenter's answer is that this would hurt their business. Also mentioned in the presentation is that GitHub encrypts their source code with [Ruby Encoder](https://www.rubyencoder.com/) and they have text in [the license](https://enterprise.github.com/license) that forbids customers from using GitHub Enterprise to compete with GitHub.com.

Of course, GitHub has every right to close and encrypt their source code. GitHub [very actively contributes to open source](http://tom.preston-werner.com/2011/11/22/open-source-everything.html) themselves, including many contributions to Git and Ruby on Rails, and releasing libraries and applications like libgit2, [Atom](https://atom.io/), and Hubot. Also note that we build GitLab with software that GitHub open sourced such as libgit2.

In conclusion (TLDR), GitLab has an open core business model and ships both open and closed source software. GitHub hosts most open source projects but ships closed source software.
