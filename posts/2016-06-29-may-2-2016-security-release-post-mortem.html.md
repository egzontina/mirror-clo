---
title: "May 2, 2016 Security Release Post-Mortem"
author: Stan Hu
author_twitter: stanhu
categories: release, security
date: 2016-06-29
image_title: '/images/default-blog-image.png'
---

On May 2, 2016, we released a [major security
update](https://about.gitlab.com/2016/05/02/cve-2016-4340-patches/), primarily
to fix a critical security issue that allowed a user to gain administrative
access via the "impersonate" feature. Now that some time has passed and most
of our users have had sufficient time to upgrade, we'd like to reflect on what
happened, how it occurred, and what we're doing in the future to improve
security in the GitLab code base.

<!-- more -->

Since May 2, we have released a number of security updates to address certain
vulnerabilities, but none of the updates have addressed a bug as serious as
the one in the "impersonate user" feature, which is now known as
[CVE-2016-4340](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-4340).
We released this feature in November of 2015 in GitLab 8.2. It enables admins
to diagnose issues with their GitLab installation by allowing them to see what
their users see. Since the initial implementation, members from the community
helped improve the code, but nobody noticed there was a security hole in one
of the controller methods.

## Discovering the hole

All that changed on Friday, April 22, 2016, when Douwe Maan, our Backend Lead,
began reviewing the code for the feature. Having reviewed hundreds of merge
requests and handled an influx of [HackerOne](https://hackerone.com) security
reports, Douwe immediately spotted something wrong: a critical authorization
flaw in one of the API endpoints. This flaw would allow a user to gain full
GitLab administrative access. Within an hour, Douwe submitted a fix
internally. Over the weekend, we began strategizing about how best to roll out
this fix to the community.

Our first question: How do we protect GitLab.com against this vulnerability
without disclosing details that might harm users who have their own
installations of GitLab? We first considered applying a hotfix to GitLab.com,
but our infrastructure team had no desire to do this. Applying hotfixes to a
live-running, production system is fraught with perils, and we did not want to
risk causing other issues. Instead, our Infrastucture Lead, Pablo Carranza
proposed blocking the vulnerable route via a HAProxy rule. This would only be
a simple configuration change in one place. The following Tuesday, Pablo
applied the HAProxy rule and verified that it successfuly blocked the route.

With GitLab.com patched with this workaround, we next had to consider: how
much advance notice should we give to our users about a security release?
Since GitLab is open source, releasing an update means the code would be
available for any malicious user to study how to exploit the hole. At first,
we decided on a 3-hour timeline:

1. Send a security announcement on our security mailing list (T-3 hours)
2. Make the GitLab packages online and update GitLab.com (T-1 hour)
3. Announce on the blog (T)

For most zero-day vulnerabilities, vendors simply announce updated packages and
encourage users to update immediately. However, after further discussion, we
felt releasing GitLab in a 3-hour window would not be responsible due to a
number of reasons:

* Most administrators would be caught off-guard without at least 24-hour notice
* The severity and ease-of-exploit of the bug could cause significant problems
* Native package maintainers of GitLab (e.g. Debian, FreeBSD, etc.) would not
have updates in time

## Warning Users

These reasons convinced us to take the unusual step of giving a notice of an
impending release for the following Monday. On Wednesday, April 27 around
5:30 pm UTC, we sent out this announcement to our security mailing list:

> We have discovered a critical security issue in all GitLab CE and EE versions from 8.2 to 8.7.
>
> On Monday May 2, 2016 at 5:00pm PDT, we will publish new GitLab patch releases
> for all affected versions. We strongly recommend that all installations
> running a version mentioned above be upgraded as soon as possible after the
> release. Please forward this alert to the appropriate person at your
> organization and have them subscribe to Security Notices. The following
> versions are affected:
>
> 8.7.0
>
> 8.6.0 through 8.6.7
>
> 8.5.0 through 8.5.11
>
> 8.4.0 through 8.4.9
>
> 8.3.0 through 8.3.8
>
> 8.2.0 through 8.2.4

In addition, we shared patches privately with GitLab package maintainers, who
all appreciated the advanced warning. They immediately began work on updating
their native packages with the changes.

## Early Release?

The next day, Thursday, we completed the long task of incorporating the
patches and building a total of 42 Omnibus packages for all six releases to a
private repository. We updated GitLab.com to 8.7.1, which contained the fix,
and removed the HAProxy workaround.

Some recipients of the e-mail [expressed confusion on Hacker
News](https://news.ycombinator.com/item?id=11582634) because they did not see
a security announcement on our blog. They suspected the e-mail was spam.

After reading the Hacker News post, CEO Sid Sijbrandij pointed out that
announcing the affected versions dramatically reduced the search scope of the
bug. An attacker could see what changed between 8.1 and 8.2 and discover the
vulnerability. If someone exploited the bug over this weekend, customers would
have no way to patch their installations for several days. A discussion ensued
about whether to move up the release earlier. Instead of Monday, what about
Thursday or Friday? We nixed Thursday because the day was over for our
European team; more time was needed to have the packages ready. We considered
moving the release up to Friday, but a number of people on the team argued that
this was not a good idea. Senior Developer Robert Speicher articulated it well:

> We chose the date we did to give people time to prepare. A smart, nefarious
> person *might* figure out the exploit over the weekend, but releasing early
> *will* catch people off-guard and put the exploit into the wild.

We decided to stay with Monday but prepare everything just in case we needed
to release early. In addition, we [belatedly posted a blog entry to match our
security e-mail notice](https://about.gitlab.com/2016/04/28/gitlab-major-security-update-for-cve-2016-4340/),
but this time we omitted the affected versions.

## Releasing to the Public

Monday, May 2, 2016 came without incident, and the day of the rollout went
smoothly. Around 11:59 UTC, we transferred all 42 Omnibus packages from our
private repository to the public one and pushed up new Docker images to Docker
Hub. We published the blog post, code, and disclosed all
previously-confidential issues to the public on GitLab.com. The security
update hit [the front page of Hacker
News](https://news.ycombinator.com/item?id=11617299).

## What Went Right

A number of things went right:

* There were no reported incidents of anyone exploiting this bug prior to our disclosure.
* We were able to reproduce, fix, and test the security vulnerabilities quickly.
* Even though we are a remotely-distributed team, we were able to effectively communicate and
pull together to get the many tasks done for the security update.

## What We Are Doing to Improve

At GitLab, we prioritize security issues and try to address them as soon as
possible. Since this release, we have learned a number of things that have
been put into action:

* We need a better workflow/tools to produce confidential merge requests and packages. [#14567]
* When we send out security notices via e-mail, we should always have an accompanying blog post.
* In the future, if we send an early security notice, we will omit the version
numbers affected to prevent people zeroing in on the vulnerability.
* We need better abstractions for our permission checking [#15450]
* We need to [hire full-time engineers to focus on improving security] and to conduct internal audits of our code
* We need to promote our [bug bounty program] on sites like HackerOne

[#14567]: https://gitlab.com/gitlab-org/gitlab-ce/issues/14567
[#15450]: https://gitlab.com/gitlab-org/gitlab-ce/issues/15450
[bug bounty program]: https://hackerone.com/gitlab
[hire full-time engineers to focus on improving security]: https://about.gitlab.com/jobs/security-engineer/

In general, we received positive responses to this May 2016 security
release. Many of our users understood that giving advance notice for a
security update made sense. We thank the GitLab community for their patience
and understanding. We will continue to be vigilant about security issues
within GitLab.

If you have not already, please sign up on for future [security
notices](https://about.gitlab.com/contact/) on this page.

## Join us on July 27th for our joint webcast with Yubico

We recognize that security is a growing concern for a number of teams. We're partnering with
Yubico again. This time to discuss industry trends and best practices for security. Here's
a quick look at what we'll be talking about.

* Key trends that affect the security of your team
* Real-life examples of how both GitLab and Yubico work to improve security
* Advice on industry best practices

If you're interested in learning more or asking security-related questions, please
join us on July 27th. [Register here.](https://page.gitlab.com/July27WebcastSecurityWebcastwYubico_LandingPage.html)
