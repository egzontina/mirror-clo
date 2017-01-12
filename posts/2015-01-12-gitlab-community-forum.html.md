---
title: "GitLab Community Forum"
date: 2015-01-12
categories:
  - community
author: Achilleas Pipinellis
image_title: '/images/forum/community.png'
---

GitLab is growing fast. Day by day, more and more people interact with it.
Over the past two years, the community around GitLab has thrived and new
contributors appear every day.

Although there are a lot of ways to [communicate][help] with each other, we
lack a central place to discuss, without relying on third party applications.

Today we present you the [GitLab Community Forum][forum]. A new home to share,
ask and discuss everything related to GitLab!

<!-- more -->

The forum is run by community members whereas the hosting is gracefully donated
by GitLab B.V.. Remember that this is _not_ the place to expect any professional
[help][] by GitLab developers, but to interact with the rest of the community.

## The platform

The platform that the forum is built on, is the well known open source project
[Discourse][], a Rails + Emberjs application. It is a powerful app that is
used by many other communities, like Docker, Twitter, NewRelic and Mozilla.

For the moment, you can sign up with a new account or use
[Mozilla persona][persona] to sign in. In the future more OAuth providers will
be supported, including gitlab.com which comes in GitLab 7.7.

### Features

Discourse has this nice feature to use topics as wikis. As such, we migrated
the troubleshooting public wiki from [GitHub][] to [this topic][discoursetr].
Any registered member can edit it and add new troubleshooting tips. Having this
guide in the forum gives us the power to leave replies under that topic and
discuss possible additions/deletions.

The search function is also very powerful. Μake sure to use it any time you
have a question or stumbled upon something; someone else might already have
posted the solution. For example, searching for `reset admin`, reveals that
there is a reference in the Troubleshooting wiki.

[![screenshot](/images/forum/forum_search_admin.png)](/images/forum/forum_search_admin.png)

## Forum structure

For better organization, we have added some [categories][] which you can choose
from when starting a topic. If you feel your post falls under a category that
doesn't exist yet, you can report it [here][catreport].

When posting, you can use either bbcode or the well known markdown to format
your reply.

If you wrote a blog post about GitLab or found out an interesting tutorial that
helped you and you think it might help others, do share it in the [HowTo][]
category. Did you know that you can install GitLab on [Mac OSX][] or [FreeBSD][]
or even [Windows][]?
The HowTo section can also include little tips, like how to give admin access
to a person via the Rails console.

The [Use Cases][] category sums up success stories of versatile setups.
It is always interesting to read how GitLab is deployed and used in enterprise
environments.

Manually updating, deploying or even building GitLab can be a tedious task. For
those who are passionate about configuration management setups,we have created
the [Configuration Management][] section.

If you just began learning Ruby on Rails or any other technologies that come
with GitLab and want to get your hands dirty, head over the [Development][]
section and open a topic. A good start is to search through the
[feature request tracker][features], find something you would like to
implement and work on that. The GitLab community has some prominent and
experienced developers that can help you get started.

If you have made a fan art about GitLab, share it in the [Fan art][] category.

We also have an [ARM devices][armcat] category for any relevant information
about GitLab running on small devices.

---

We are hoping for many contributions in this early stage, so spread the word
and let the forum be the place where we bond as community.

Happy posting!

<sub>*Creative Commons image by [pixabay.com][img].*</sub>

[forum]: https://forum.gitlab.com "GitLab Community Forum"
[Discourse]: https://www.discourse.org "Discourse home page"
[categories]: https://forum.gitlab.com/categories "GitLab forum categories"
[catreport]: https://forum.gitlab.com/t/missing-categories-report-here/18
[ggroups]: https://groups.google.com/forum/#!forum/gitlabhq "GitLab google group"
[stackoverflow]: http://stackoverflow.com/questions/tagged/gitlab "GitLab on stackoverflow"
[irc]: http://webchat.freenode.net/?channels=gitlab "GitLab on freenode"
[GitHub]: https://github.com/gitlabhq/gitlab-public-wiki/wiki/Trouble-Shooting-Guide "Deprecated Troubleshooting guide on GitHub"
[discoursetr]: https://forum.gitlab.com/t/troubleshooting-guide-wiki/31 "Troubleshooting Guide Wiki"
[Mac OSX]: https://github.com/WebEntity/Installation-guide-for-GitLab-on-OS-X
[FreeBSD]: https://github.com/chadliu23/Installation-guide-for-GitLab6-on-Freebsd
[Windows]: https://forum.gitlab.com/t/how-to-install-gitlab-on-windows/32
[armcat]: https://forum.gitlab.com/c/arm-devices "ARM devices category"
[HowTo]: https://forum.gitlab.com/c/howto "HowTo category"
[img]: http://pixabay.com/en/circle-hands-teamwork-community-312343/
[features]: http://feedback.gitlab.com/forums/176466-general "Feature requests"
[Use Cases]: https://forum.gitlab.com/c/use-cases "Use Cases category"
[Configuration Management]: https://forum.gitlab.com/c/configuration-management "Configuration Management category"
[Development]: https://forum.gitlab.com/c/development "Development category"
[Fan art]: https://forum.gitlab.com/c/fan-art "Fan Art category"
[help]: /getting-help "Getting help for GitLab"
[persona]: https://login.persona.org/about "Mozilla persona"
