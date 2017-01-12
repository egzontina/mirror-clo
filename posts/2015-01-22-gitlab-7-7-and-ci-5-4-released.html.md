---
title: "GitLab 7.7 and GitLab CI 5.4 with GitHub importer and OAuth authorization"
date: 2015-01-22
categories: release
author: Job van der Voort
image_title: '/images/7_7/bg.jpeg'
---

GitLab is Version Control on your Server. It's like GitHub but Open Source.

Today we announce the release of a new version of GitLab Community Edition (CE)
and GitLab Enterprise Edition (EE), and GitLab Continuous Integration (CI)
with new features, usability and performance improvements, and bug fixes.

Also we are happy to announce our new **free Continuous Integration (CI) service: [ci.gitlab.com](https://ci.gitlab.com)**.

<!--more-->

# GitLab 7.7

The biggest new features in GitLab Community Edition are the **GitHub importer** and **OAuth support**.
In addition to the updates from Community Edition,
GitLab Enterprise Edition has gained some performance improvements and the ability to change the header logo.

This month's Most Valuable Person ([MVP](https://about.gitlab.com/mvp/)) is Ciro Santilli
for sending over 200 merge requests to improve the GitLab code base.
Thanks Ciro!


## Redesigned navigation

This had been on our minds for a while but we finally decided to
redesign the GitLab navigation! We worked closely with our awesome community
and hope you love it.

Check it out:

[![screenshot](/images/7_7/design.png)](/images/7_7/design.png)

Have a look at the [article](https://about.gitlab.com/2015/01/16/pragmatic-redesign-for-gitlab/)
we wrote about the redesign to get a better understanding of why we did it.

## GitHub importer

You can now super quickly import your GitHub projects, issues and all!
A single click is all it takes:

[![screenshot](/images/7_7/import.png)](/images/7_7/import.png)

Find the importer when creating a new project.

## Mention notification level

Getting too much email? Just select the 'Mention' notification level and you
will only receive notification emails when people mention you.

[![screenshot](/images/7_7/mention.png)](/images/7_7/mention.png)


## OAuth!

Services like Facebook, Twitter, and Google allow you to sign in using
their credentials in 3rd party applications, implemented through [OAuth](http://en.wikipedia.org/wiki/OAuth).

From now on, GitLab is also an OAuth resource server. This means that you can
create 3rd party applications and use your GitLab credentials for authentication!

We can't wait to hear what you'll use it for.

[![screenshot](/images/7_7/oauth.png)](/images/7_7/oauth.png)

## Configure GitLab on the fly through the UI

Finally GitLab admins can change the application settings on the fly
without any downtime through our new settings page:

[![screenshot](/images/7_7/settings.png)](/images/7_7/settings.png)

When you start GitLab 7.7 the first time it will import your settings from gitlab.yml.
After this initial import the settings in gitlab.yml are ignored.

In the future we'll add more settings to this page, making configuring
GitLab even easier.

- - -

# Don't want to run your own? Use GitLab.com!

You'd rather live in the cloud? Use GitLab.com! It's a completely free
GitLab instance hosted and managed by us. It offers (private) repositories,
issue tracking, wiki’s and continuous integration. Free!

You don’t have to install anything, just [sign up for a free account](https://gitlab.com/users/sign_up).

# GitLab CI 5.4

On top of all the new feature for GitLab, we're releasing a bunch more for
GitLab CI. These features will make testing your code more powerful and more
flexible.

## OAuth authorization

With GitLab as OAuth resource server, you can now easily link GitLab CI to
your GitLab instance, so you don't need to authenticate when switching to CI
anymore. Of course, this also works if you've setup LDAP / AD with GitLab.

You can even use this if you authenticated with GitLab through another OAuth
provider, such as Twitter or GitHub. This means that it's now much faster
and easier to use CI.

[![screenshot](/images/ci_5_4/login.png)](/images/ci_5_4/login.png)

## Runners for everyone!

Want to add a Runner that runs your tests and scripts to a project?
Now you don't need to be an admin to do this anymore. Just install
the GitLab Runner package on any machine and use the project token
to register the Runner in your instance.

If only we'd be offering some credits to give this a try...(hint: Keep reading!)

## Labels for Runners and jobs

Now that you can easily add a group of Runners to your CI instance, we thought
it would be very cool to be able to easily run different environments per job.

Now you can add labels to jobs. Only a Runner with that (those) label(s) will pick up
up the matching jobs. This way you can run different environments per job, easily.

Project jobs:

[![screenshot](/images/ci_5_4/ci-job-labels.png)](/images/ci_5_4/ci-job-labels.png)

Project runners:

[![screenshot](/images/ci_5_4/ci-runner-labels.png)](/images/ci_5_4/ci-runner-labels.png)

## Omnibus packages for GitLab Runner

We now [offer Omnibus
packages](https://gitlab.com/gitlab-org/omnibus-gitlab-runner/tree/master/doc/install)
for GitLab Runner. No need to download and compile Ruby anymore each time you
set up a runner!

The installation instructions for the Runner packages only cover Ubuntu 12.04
and 14.04 at the moment. To be continued!

- - -

# Continuous Integration (CI) for free

We are happy to offer free CI for private repositories if you bring your own Runner!

Simply add your projects from GitLab.com on ci.gitlab.com and configure the builds script(s).
You can use the parallel build feature of GitLab CI and
we'll store the build logs and configuration for you.

To run your tests you need to install GitLab Runner on one or more of your instances.
Don't have any instances yet? No problem:

**In total, we're giving away up to $520,000.- in cloud hosting for people to host their Runner!**
This is a collaboration with Google Compute Engine and Digital Ocean, we're very grateful for their offer.
Did you know they both also offer one-click-installs of GitLab?
To claim your credit please see the instructions below.

The credit is a limited time offering but the free CI for private projects on ci.gitlab.com is permanent.

# Claim Google Cloud Platform credit

Google Cloud Platform offers $500 in credit for the first 1000 users.
To get started, follow the three steps below:

1. Go to [http://cloud.google.com/startercredit](http://cloud.google.com/startercredit)
1. Click Apply Now
1. Complete the form with code: gitlab

With Cloud Platform you can access application, compute, storage and big data services.
You’re now building on the same infrastructure that powers Google.

# Claim Digital Ocean credit

DigitalOcean offers $40 in credit for the first 500 users.
This is valid only for new DigitalOcean accounts, not for existing users.
The offer is valid for two weeks and you can claim up to one promo per person.
You need to setup a project on GitLab.com and add it to ci.gitlab.com before you can claim it.

To claim it please fill out [this form](https://docs.google.com/a/gitlab.com/forms/d/1YXTRwDz2C8o4DqNrFCT78UQf_iHnN1Ekrt4p8yv6fd4/viewform) with your name, email or handle and project url.
Once submitted, the GitLab team will email you your unique promo code.
If you have any questions about this promotion, please contact the GitLab support team at support@gitlab.com.

# Custom header logo (EE only)

For GitLab Enterprise Edition Drew Blessing contributed customer header logo support.
There also were fixes for the preview and performance improvements for selectboxes.

# Open sign-up by default

From this version on user self-signup is enabled by default.
You can still disable this behaviour in the new applications settings page.

# Other changes

This release has more improvements, please check out [the Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/7-7-stable/CHANGELOG) to see the all named changes.

# Upgrade barometer

There are migrations in this update but they do not take considerable time and should be quick.

If you don't want users to sign up themselves and you have not setup this in gitlab.yml you must ensure this behaviour stays the same.
You can do it by adding it to gitlab.rb (Omnibus package) or gitlab.yml (source installation) or the easiest way is to use the new application settings page to do this.

After you upgraded and tested GitLab consider removing the settings that are now in the application settings page from gitlab.rb (Omnibus packages) or gitlab.yml (source installation) to prevent confusion.

# Installation

If you are setting up a new GitLab installation please see the [installing GitLab page](https://www.gitlab.com/installation/).

# Updating

Upgrade instructions for omnibus-gitlab packages can be found in [the omnibus-gitlab repository](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/update.md).

If you installed GitLab from source and you have version 6.4.2 or higher you can use the [upgrade script](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/upgrader.md).
You have to update GitLab Shell to 2.4.1 manually, see [point 3 of the upgrade guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/X.x-to-x.x.md#3-update-gitlab-shell-and-its-config).

If you still want to do it manually - see the [Update Guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/7.6-to-7.7.md).

# Enterprise Edition

The mentioned EE only features and things like LDAP group support can be found in GitLab Enterprise Edition.
For a complete overview please have a look at the [feature list of GitLab EE](http://www.gitlab.com/gitlab-ee/).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/pricing/).
No time to upgrade GitLab yourself?
A subscription also entitles you to our upgrade and installation services.

- - -
