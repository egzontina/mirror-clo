---
title: "Feature Highlight: Confidential issues"
date: 2016-03-31 08:00
author: Douglas Alexandre
author_twitter: dbalexandre
image_title: '/images/unsplash/door.jpg'
---

Since GitLab 8.6, in both Community and Enterprise edition, there is a small
checkbox available when you create or edit an issue, allowing you to mark an
issue as confidential.

In some ways it’s a simple feature, but there are complex considerations.
The main point is to keep the confidential issues secure.
However, taking care of those considerations caused some problems during
development which are typical when you develop a feature for a relatively
long time (in this case two weeks). We'll look at that in this feature highlight.

<!-- more -->

## About Confidential Issues

In the course of maintaining a project, it may be necessary to keep some
information from public view. A typical use case for confidential issues would
be a security report. Different projects support different ways to report
security issues, so if someone needed to report a security issue, they would
have to:

- Follow the instructions for security vulnerabilities, if there are any.
- File an issue with their findings and a request to get in contact with the
  project maintainer.
- Find other means to contact the maintainer.

In general, most of the projects advise to not use the issue tracker, and
instead send an email to a specific email address. As you might imagine before
this release we, as an open source project, advised the same
[security vulnerability disclosure][disclosure] in our contributing guide:

> Please report suspected security vulnerabilities in private to
support@gitlab.com, also see the disclosure section on the GitLab.com website.
Please do NOT create publicly viewable issues for suspected security
vulnerabilities.

This generated a lot of overhead.

Behind the scenes, when we got a security report email, we would immediately
create an issue in our internal issue tracker to discuss possible fixes. So in
that case, we needed to keep in track two issues trackers: a public one on
GitLab.com and another private. In addition, the process to report a security
issue would be more complex than it is now. First, you need to discover how to
report the issue, and then report the issue itself.

Now, with Confidential Issues, the reporter can mark an issue as confidential
when creating or editing an issue, and only project members can see the issue,
as well as those who are assigned to it. As it turns out, the process is
considerably easier, since reporters don't need to find how to report security
issues anymore, and we don't need to work on two different issue trackers for
the vulnerability disclosures.

When an issue is marked as confidential, it is only visible to the team members.
It will be hidden from the public view, which means the issue tracker, the
activity feed, the milestone views, the auto-complete options, etc. Even if you
get a `@mention`, and you don’t have explicit access to the project, you won't
receive any kind of notification (in this case emails, and todos).

## Behind the scenes: Resolving merge conflicts as you go

While this is a simple feature, it created an interesting problem, and I'm not
talking code-wise.

Because it causes lots of concern about security, we needed to very careful
with this. I had the branch open for a relatively long time (about two weeks),
and over time, I was running into merge conflicts almost daily. My work was
affected by other features being developed at the same time, for example
subscribe to labels. This happens very often if you have a merge request open
for a long time.

I do try and avoid this when I can. I check everyday if my merge request has
conflicts and I resolve these as I work, that is, instead of waiting until
the final release to merge.

It also helps a lot to do development with automated tests. As you work in
parallel with other developers and constantly update the feature, you can tell
if something is going to break.

Normally, you don’t work a long time on issues like this but in this case it
was unavoidable due to the security nature of the feature. Again, using tests
made this a lot easier.

## More about GitLab 8.6

This *confidential issues* feature is just one of the many recent changes in GitLab.
Find out more [about our latest release, 8.6][release] with new improvements
and features.


[disclosure]: https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CONTRIBUTING.md#security-vulnerability-disclosure
[release]: https://about.gitlab.com/2016/03/22/gitlab-8-6-released/