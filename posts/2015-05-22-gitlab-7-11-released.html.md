---
title: "GitLab 7.11 released with Two-factor Authentication and a publicly viewable Enterprise Edition"
date: 2015-05-22
categories: release
author: Job van der Voort
author_twitter: Jobvo
image_title: /images/7_11/ny.jpg
---

It's the 22nd of the month, so we have a new GitLab release ready!
GitLab 7.11 brings more improvements to the look and feel of GitLab,
two-factor authentication, a version check and more!

Of course we're also releasing GitLab CI 7.11, with a new backup and restore
utility, improvements in the UI and other new features.

This month's MVP is [James Newton](http://jamesnewton.com/) (newton on IRC)!
James is very active on our `#gitlab` IRC channel, often helping people out
with issues or helping people getting started with GitLab. We're very
happy to have James supporting the community and believe that is deserving
of a MVP award!
Thanks James!

<!-- more -->

## Better looking sidebar

We changed the look of the sidebar to reflect its function better and make it look
more pretty:

![The new sidebar in GitLab 7.11](/images/7_11/sidebar.png)

## Clean project dashboard

The project dashboard was a good example of design by committee, one GitLab
contributor noted. We broomed through it and cleaned it up:

![Project Dashboard in GitLab 7.11](/images/7_11/project.png)

## Two-factor authentication

Keep your code more secure and start using two-factor authentication (2FA)!
GitLab has built-in 2FA in both CE and EE now and makes use of the convenient
Google Authenticator.

All you have to do is go to your Profile > Account and scan the QR code using
Google's app.

![two-factor authentication](/images/7_11/2fa.png)

From now on, on login you'll be required to provide the code the app gives you
for GitLab. Two-factor authentication only works with the web-UI for now.

## User roles in comments

Now you know who's who in your favorite project. On comments you will see
the role of the person in that project:

![not an actual conversation](/images/7_11/roles.png)

## Task lists everywhere

Want a task list in the comments? Now you can!

![Task list in comments](/images/7_11/task.png)

## Version Check

GitLab releases a new version _every single month on the 22nd_, so we understand
that people are not always up to date. We wanted to give you some help with
this, so from now on you can quickly see which version of GitLab you have running
by visiting the Help or Admin page. It will show if you are up to date and
if there is a security release you should have installed.

Read more about the version check in our [blog post about it.](https://about.gitlab.com/2015/05/07/version-check/)

You can turn off the version check under Admin > Settings.

## License keys for Enterprise Edition

GitLab Enterprise Edition used to live in a private repository, which was fine up
until now. However, with the addition of our package server, we want
to make it easier to start using GitLab Enterprise Edition.

Rather than locking up the package repository of GitLab EE, we decided to
open up all the code and [packages](https://packages.gitlab.com/gitlab/gitlab-ee) and start using license keys. The code
is still proprietary, but now is [publicly viewable](https://gitlab.com/gitlab-org/gitlab-ee/).

This has several advantages. The installation of GitLab EE becomes as easy as
installing GitLab CE. You no longer needs access to specific repositories,
rather you can download it using the same methods as CE (including AWS/Azure templates, Docker images, etc).

In addition, the code for Enterprise Edition is now becoming open to inspect
for everyone. This will make it easier to send enhancements and makes it easier
to do a trial of Enterprise Edition.

Getting organizations to purchase a subscription after their trial expires or
at renewal time sometimes took a substantial effort from us.
We don't want to raise prices for customers that renew without prompting because
we need to invest more time in unresponsive customers.
Therefore we decided to introduce license keys that prompt customers automatically.
We regret the inconvenience that license keys introduce
but we think it is the best solution to keep prices low.

## True-up model for subscriptions

The worst thing about license keys is that they can be very inflexible.
Most GitLab installations quickly grow in popularity within the organization.
Having to purchase a new license key every time this happens is very inefficient.
Also, we noticed that the majority of our customers didn't have a compliant subscription, for us this indicates that having to renew the subscription multiple times a year is very inconvenient.

Therefore we will switch to a true-up model that allows you to grow now and pay later.
When you get a new license you should get it for your current number of active users.
For users that are added during the year you pay half price when you renew.

So if you have 100 active users today you get a 100 user subscription.
Suppose that when you renew a year from now you have 300 active users.
You pay for a 300 user subscription and pay half a year for the 200 users that you added during the year.

### Getting the license key

If you are currently a GitLab customer, you should have received your license
key already at the email you registered with your payment. You can also email
`sales at gitlab dot com` to request it at any time.

New subscribers will receive their license key automatically.

### Installing the license key

To install the license, vist `/admin/license` in your GitLab instance as an
admin. Here you can upload your `.gitlab-license` file, which will instantly
unlock GitLab Enterprise Edition.

![Installing your license](/images/7_11/license.png)

You can also download and review your current license here.

_Please note that we will release GitLab 7.10.5 soon, that will allow you to
upload the license key to your GitLab instance before upgrading, to avoid
unnecessary downtime._

## Two-Factor Authentication for LDAP / Active Directory (EE-only)

Want to use two-factor authentication together with your LDAP or Active Directory
integration? With GitLab Enterprise Edition you can.

## New GitLab CI Features

With the release of GitLab 7.11, we also updated GitLab CI to 7.11.
Some changes worth mentioning are an improved runners page,
public accessible build and commit pages for public projects
, a new backup/restore utility that will backup your CI database and
HipChat notifications!

## Other awesome changes in GitLab CE

We can never cover all the new stuff in each GitLab release, but these
are worth to have a quick look at as well:

**Quick quote-reply** You can now reply with a quotation by simply selecting text in an issue
or merge request and pressing `r`. It will set the focus to the editing window
and have the quoted text already in it!

**Atom feeds for all!** There is now an atom feed for each project!

**Settings in admin UI** We moved default project and snippet visibility settings
to the admin web interface.

**Improved UI for mobile** GitLab is now better viewable on mobile!

**WIP your MRs!** If you add `WIP` or `[WIP]` (work in progress) to the start of the title of a merge request,
it will be protected from merging now.

![WIP blocking the merge request of this blog post!](/images/7_11/wip.png)

This release has more improvements, including security fixes, please check out [the Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG) to see the all named changes.

## Upgrade barometer

Coming from 7.10, the migrations in 7.11 are pretty fast (under 1 minute), but one of them is tricky:
we rename any existing users with names ending in a period ('.').
This migration updates both the database and the filesystem and previous versions
of this migration have proven to be fragile.

If you have no user namespaces with paths ending in '.' in your database and if you trust your users not to
create any until after you upgrade to GitLab 7.11 you can perform this upgrade online.
If not, we recommend to take downtime (this is what we did for gitlab.com).
You can find the current number of affected database records with the following command:

```
 sudo gitlab-rails runner "puts Namespace.where(type: nil).where(%q{path LIKE '%.'}).count"
```
- - -

## Installation

If you are setting up a new GitLab installation please see the [installing GitLab page](https://www.gitlab.com/installation/).

## Updating

Check out our [update page](https://about.gitlab.com/update/).

Please note that cookbook-omnibus-gitlab, our Chef cookbook that installs/manages GitLab omnibus packages,
does not yet support packages.gitlab.com. See [this issue](https://gitlab.com/gitlab-org/cookbook-omnibus-gitlab/issues/8).

## Enterprise Edition

The mentioned EE-only features and things like LDAP group support can be found in GitLab Enterprise Edition.
For a complete overview please have a look at the [feature list of GitLab EE](http://www.gitlab.com/gitlab-ee/).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/pricing/).
No time to upgrade GitLab yourself?
A subscription also entitles you to our upgrade and installation services.

- - -