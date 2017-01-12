---
layout: post
title: "Fearless Contribution: A Guide for First-Timers"
date: 2016-06-16
author: Drew Blessing
author_twitter: drewblessing
image_title: '/images/default-blog-image.png'
---

> This post is part of a series [Celebrating 1,000 Contributors][1k-post]

There are clear benefits to contributing to open-source projects. For starters,
you'll solve your own problems more quickly and you will have a positive effect
on your favorite projects.

However, the barrier to entry can be high for first-time contributors. Perhaps
you feel your coding skills are not up to par, or maybe you aren't a programmer
at all. When you do approach a project, you may find the contribution guidelines
are unclear, the maintainers are unresponsive, or you may disagree over
priorities.

I'll give you some practical advice on overcoming these hurdles. We'll also
look at the ways GitLab tries to make contributing easier in our own project.

<!-- more -->

## Ways to contribute

First time contributions can be scary. If you're worried your skills are not
up to par, you're not alone. Many new and seasoned people in the technology
field feel this way at one point or another. The best way to overcome this
feeling is to jump in *somewhere*. No matter how large or small the
contribution, you will gain confidence and feel more comfortable each time.

Some may believe that the only way to contribute to an open-source project is
by writing code - fixing bugs or contributing new features. In reality, there
are more ways to contribute.

### Documentation

As you were learning to use the application or tool, did you notice gaps in the
documentation? This is a great way to start contributing to a project. If you
experienced and overcame a challenge because the documentation was lacking,
it's an opportunity to get involved and help others.

Many projects commit documentation in the same repository as the code. For
example, GitLab stores all documentation in the `doc` directory within a
project. For GitLab CE, you can see documentation source at
[https://gitlab.com/gitlab-org/gitlab-ce/tree/master/doc](https://gitlab.com/gitlab-org/gitlab-ce/tree/master/doc).
If you don't find documentation in repository then you may find a hint on the
doc site. Look for a link near the bottom of the page that points to the source.
On [https://docs.gitlab.com](https://docs.gitlab.com) we have a link at the
bottom of each page pointing to a specific source document. Here is an example
of the doc site footer:

---

![Doc site footer](/images/first_time_contribution/doc_site_footer.png)

---

### Issue Tracker

Get involved in the project's issue tracker. To begin with, you may only create
bug reports for issues you encounter. As you become more comfortable, consider
triaging other bug reports.

Start by picking an existing issue and try to reproduce the problem in your own
system. If you can reproduce it, outline the steps as a comment on the issue.
This will save developer's time when they come to fix the bug later. If you
cannot reproduce the issue, ask the reporter for more information. Triaging
issues has a side-effect of helping you learn more about the project. This will
come in handy as you contribute documentation and/or code in the future.

### Bug Fixes and New Features

If you can write code, consider contributing bug fixes and, eventually, new
features. Chances are you've encountered a bug or two in the course of using
a project. Contribute a fix for one of these bugs first. It's
rewarding when you solve one of your own problems and see the change accepted.

Some projects may have labels to help direct you to easier bug fixes. For
example, GitLab projects contain an `up-for-grabs` label that signifies a
bug that newer contributors may be able to solve. Beyond that, browse the
issue tracker for an interesting problem that you believe you can fix.

## Contribution Guidelines

Many open-source projects have defined guidelines that contributors
are expected to adhere to when submitting issue reports or merge requests. These
guidelines are meant to reduce the amount of time the maintainers spend
repeatedly asking for required details or changes to code style.

Before creating an issue report or merge request, look for a CONTRIBUTING.md
file in the root of the repository. To make finding this guide easier, GitLab
has a link to 'Contribution guide' on project home pages if there is a
CONTRIBUTING.md in the repository.

![GitLab Project Page](/images/first_time_contribution/project_page.png)

Adhering to the guidelines is a great way to prevent your contributions from
being rejected or delayed. Most maintainers don't intend to discredit your
work or be tough on contributors. However, many are busy and are doing this
in their free time.

Scan the [GitLab Community Edition Contribution Guide][contrib-guide]
to see how we handle community contributions. Notice our requirements for
merge request descriptions. There are five headines that we request so we have
all the information we need to understand the purpose of the proposed change.

```
## What does this MR do?

## Are there points in the code the reviewer needs to double check?

## Why was this MR needed?

## What are the relevant issue numbers?

## Screenshots (if relevant)
```

## Conflicting priorities

Sometimes a request will be turned down because of conflicting priorities.
Whether you're requesting a new feature, or providing a fix, remember that the
maintainer has to weigh the contribution. They're the ones that will have to
support this code in the future and resources are often slim. Additionally,
it's important to understand whether a feature will be helpful to the wider
user community. Try not to be discouraged if your feature request or merge
request is turned down. Be open-minded and, if necessary, propose
an alternative idea after hearing their concerns.

## Unresponsive maintainers

This can be a really frustrating part of open-source. When you're experiencing
a bug or waiting on some functionality for your use-case, a lack of response
can be maddening. Remember that some project maintainers are working on projects
in their spare time and aren't paid to do this. In some cases, projects may be
abandoned because the maintainer no longer has the need or interest.

There aren't always good ways to deal with this scenario. Interested and
experienced people may offer to take over maintainership, or the project could
be forked. Often, though, patience is key.

## Start a project

As you become more experienced, consider starting a small project that is
a command line tool or utility. Choose something that will be useful in
your daily tasks so you will be motivated. Don't necessarily be concerned about
competing projects to begin with. The ultimate goal of this endeavor is to
learn.

As an example, 3 years ago I thought it would be useful to have a command line
tool for GitLab. I really wanted to be able to create a snippet by piping
some text to a command. Up until this point I had written very little Ruby
but I tried it anyway. I learned a lot about Ruby, how to organize a project,
and I used this tool successfully for quite a while. I no longer maintain this
project but I'm still happy I created it. For sentimental purposes, you can see
the code at https://github.com/drewblessing/gitlab-cli.

## Get involved in GitLab!

We always welcome new contributors to the GitLab community so jump right in and
work on one of the areas mentioned above. If you can write code, we recently
published a blog post about [Getting Started with GitLab Development Kit][gdk-post].
There are also community-based support channels that are great places to get
involved. See the [Getting Help][getting-help] section of our website for links
to these channels.

## Final Thoughts

I find being part of an open-source community to be a fun and rewarding
experience. In almost every project I've been involved with I started out
knowing next to nothing about the project, or programming language. Start small
and don't underestimate your skills. Over time you will learn a lot through
your involvement and you'll become more confident.

[1k-post]: https://about.gitlab.com/2016/05/24/1k-contributors/
[gdk-post]: https://about.gitlab.com/2016/06/08/getting-started-with-gitlab-development-kit/
[getting-help]: https://about.gitlab.com/getting-help/
[contrib-guide]: https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CONTRIBUTING.md
