---
title: "GitLab Mattermost, an open source on-premises Slack alternative"
date: 2015-08-18
author: Sytse Sijbrandij
author_twitter: sytses
image_title: '/images/unsplash/love-the-sun.jpg'
---

We're very excited to announce that we'll ship GitLab Mattermost, an open source, on-premises messaging app (like Slack) along with GitLab.
GitLab Mattermost will first be included with the Omnibus packages of GitLab 7.14 (due August 22nd).
We think GitLab Mattermost will be a great addition for GitLab users that need all software on-premises.

<!-- more -->

Like many companies in the last year we've switched to using Slack to improve internal communication.
We are a [remote company](https://about.gitlab.com/2014/07/03/how-gitlab-works-remotely/) and great realtime asynchronous communication is very important.
Obviously we use GitLab issues and merge requests extensively, but for some things a chat room can't be beaten.

That is why GitLab used to include a chat feature called the 'wall' for each project.
The wall was a [loved feature in 2012](https://twitter.com/gitlab/status/274128115318550531), but in 2014 people [didn't use it](https://twitter.com/gitlab/status/478990520505888769).
The code had deteriorated and we removed the wall when we [released GitLab 7.0](https://about.gitlab.com/2014/06/22/gitlab-7-dot-0-released/).

Many larger organisations run all software on-premises, often because of security, scale and control.
Since Slack doesn't offer an on-premises version, we searched for other options.
We found Mattermost to be the leading open source Slack-alternative and suggested a collaboration to the Mattermost team.

![Mattermost screenshot](/images/mattermost/mattermost.png)

It turns out that [after the succesful launch of MatterMost on Hacker News](https://news.ycombinator.com/item?id=9770322) there were a lot of requests for an easier way to install Mattermost and to add LDAP features to it.
With Omnibus GitLab we have a great way to install software in 2 minutes on many platforms and GitLab CE and EE contain many LDAP features.
We decided to collaborate and the Mattermost team quickly added PostgreSQL support and OAuth login to Mattermost so it could connect to the [GitLab OAuth provider](http://doc.gitlab.com/ce/integration/oauth_provider.html).

In version 7.14 GitLab Mattermost will be part of the Omnibus package, just like GitLab CI.
Just like GitLab CI it will be disabled by default so it doesn't use any CPU or memory and doesn't enlarge the attack surface.
And just like GitLab CI it takes a one line configuration change to enable it.
Right now Mattermost 0.6 is in alpha state, its security has yet to be externally reviewed, and data migration to future versions might not always work.
But GitLab the company will pay for an external security audit and the Mattermost team is getting closer to a beta version.

Adding the GitLab Mattermost code to the Omnibus packages makes them just 3% larger (from 337MB to 345MB right now) and offers a much easier setup because we can configure the OAuth integration automatically like we do for GitLab CI.
In gitlab.rb you'll configure the FQDN (mattermost.example.com) and the Omnibus package will take care of setting up OAuth credentials. In the future we'll also make it easier to post from GitLab and GitLab CI to GitLab Mattermost.
Releasing it with 7.14 in alpha state will allow more eyes on the project in order to [report Mattermost bugs on GitLab.com](https://gitlab.com/gitlab-org/gitlab-mattermost), [responsibly disclose Mattermost security vulnerabilities](http://www.mattermost.org/responsible-disclosure-policy/) and [report Omnibus package bugs](https://gitlab.com/gitlab-org/omnibus-gitlab/issues).
We hope that with GitLab 8.0 (planned for September 22, following 7.14) we can ship GitLab Mattermost in beta state.
The progess of the work is discussed in [an issue for Omnibus GitLab](https://gitlab.com/gitlab-org/omnibus-gitlab/issues/654).

We have not taken the decision to include an extra component in the Omnibus packages lightly.
We think GitLab Mattermost will be a great addition for GitLab users that need all software on-premises.
We hope that the rest of the community is as exited about this as we are.
We look forward to discussing your ideas and concerns in the comments.
