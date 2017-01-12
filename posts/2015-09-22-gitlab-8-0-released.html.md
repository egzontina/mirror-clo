---
title: "GitLab 8.0 released with new looks and integrated CI!"
date: 2015-09-22
categories: release
author: Job van der Voort
author_twitter: jobvo
image_title: /images/8_0/sf.jpeg
---

Fifteen months ago we [released](https://about.gitlab.com/2014/06/22/gitlab-7-dot-0-released/)
GitLab 7.0. Since then we've vastly improved the performance of GitLab,
made GitLab work in any Enterprise through deep LDAP integration and
made it possible to [work with large files in Git](http://doc.gitlab.com/ee/workflow/git_annex.html).
On top of that, the UI has been reworked and improved with every release,
GitLab CI has become a very powerful tool and we've made [hundreds of other improvements](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG).

We built this all as a community and by being [more](https://about.gitlab.com/2015/05/22/gitlab-7-11-released/)
and [more](https://about.gitlab.com/2015/08/03/almost-everything-we-do-is-now-open/) open.

Today, GitLab's next major version is here. We're very excited that GitLab 8.0 allows for a faster,
more beautiful way for people to create, review and deploy code together.

GitLab now comes with continuous integration ([GitLab CI](https://about.gitlab.com/gitlab-ci/))
fully integrated.
But that's not all! Almost every element in the interface has been reworked
and GitLab will take up to 50% less disk space.

This month's Most Valuable Person ([MVP](https://about.gitlab.com/mvp/)) is
**Kirill Zaitsev** for the awesome Drone CI integration and work on the service API.
Thanks Kirill!

<!--more-->

## Continuous Integration in GitLab

Code lives in GitLab: It's made, reviewed, and merged in GitLab. Now it gets
tested, packaged, and deployed in GitLab as well.

With GitLab 8.0, we've integrated GitLab CI directly into GitLab itself. This
means that you no longer have to visit a separate application to see the status
of your projects.
You can see all of your tests, deployments, and packaging that
you would normally see in your CI, right in GitLab.

If you were using GitLab CI before, please see the notes on migrating at the
end of this post.

Simply visit 'Continuous Integration' from the Dashboard:

![Continuous Integration in GitLab on the Dashboard](/images/8_0/ci_dash.png)

Or through one of your projects:

![Continuous Integration in GitLab in your project](/images/8_0/ci_proj.png)
![Continuous Integration in GitLab: project view](/images/8_0/ci_proj2.png)

There are [advantages and disadvantages](https://gitlab.com/gitlab-org/gitlab-ce/issues/2164#note_1902301) to this integration.
We feel confident that the benefits outweigh the drawbacks.

In GitLab versions following 8.0, the impact of this integration will become
more visible. The integration is a big step that we had to do first and we have
a policy of iterative improvements.

GitLab 8.1 will [integrate CI into the menu structure](https://gitlab.com/gitlab-org/gitlab-ce/issues/2594)
and add a [commit status API](https://gitlab.com/gitlab-org/gitlab-ce/issues/2595),
which will make it easier for third party CI services to integrate with GitLab.

## Fresh Design

GitLab 8.0 comes with a completely new look and feel.
This is not just a small iteration, but a major revision of almost every
UI element in GitLab.

We fixed the width of certain views to make it easier to view text. We also improved
that text with a pretty new typeface. In addition, contrast is reduced for elements that are less important,
increased for elements that are more important and some soft lines were added for clarity.

Take a look for yourself at our clean, new design:

![GitLab 8.0 Dashboard](/images/8_0/dashboard.png)
![GitLab 8.0 project](/images/8_0/project.png)
![GitLab 8.0 Merge Request](/images/8_0/mr.png)

## Turbo Merges (Vroom Vroom)

Merging a merge request is now faster!
Rather than working in local copies of repositories (satellites),
we now work directly in them. This makes many git operations, like
merges, much faster and more reliable.

## 50% less space used

By removing satellites in GitLab, we free up the space left behind.
Project size in GitLab is cut in half reducing disk usage up to 50%.
When you upgrade to GitLab 8.1 next month the satellites will automatically be
removed. If you need to remove them before that time you can do so manually.

## Reply by Email

Want to quickly reply to your colleagues in GitLab while on the go or when
going through your email? Now you can.
You can now simply reply to any notification email to comment in the issue
or merge request. This brings GitLab to any app that can use email;
we're already looking forward to comments from your smart watches!

* See [the documentation on reply by email](http://doc.gitlab.com/ce/incoming_email/README.html)
to set it up

![Reply by Email!](/images/8_0/rbe.png)

## Quick open in Gmail

Still want to get the full view of the issue or merge request while in Gmail?
Use the new quick links. In Gmail and in Inbox you will see a direct link
to the referenced issue of a notification you got from your GitLab instance.
If you use Google Inbox on your phone, you'll see the links there as well!

_Note that you need to go through an involved approval process of Google to enable this.
We already did this for GitLab.com._

* For the approval process steps please see the [documentation on Gmail action buttons](http://doc.gitlab.com/ce/integration/gmail_action_buttons_for_gitlab.html)

![Gmail Action Buttons](/images/8_0/gmail.png)

## Easily Upload files in GitLab

To make it much easier to upload files to your repository, you can now do this
directly through GitLab's interface!

![Quick Upload into your repository](/images/8_0/upload.png)

Yakun Li and Stan Hu deserve special recognition for being
patient and persistent while adding this feature, which had a [pull request with
250 comments](https://github.com/gitlabhq/gitlabhq/pull/9138)! Awesome work!

## Better HTTP Support

We've replaced Grack in GitLab to handle HTTP clones and pushes and are now using our
own hip Go daemon, [gitlab-git-http-server](https://gitlab.com/gitlab-org/gitlab-git-http-server).
This means large clones and pushes over HTTP are now less likely to time out!
It also ensures the Unicorn workers are freed from these long running requests, making GitLab faster for users.

## Mattermost Improvements

We're shipping [Mattermost Beta1](http://www.mattermost.org/mattermost-beta1-now-available/)
with GitLab 8.0!

You can now make use of GitLab Single Sign On to authenticate with Mattermost,
making the shared experience much more fluid.

On top of that, the Mattermost team has added File and Image sharing, a way
to import Slack data and a host of other improvements and fixes!

![Mattermost Beta1!](/images/8_0/mattermost.png)

The team at Rocket Chat encountered a
[few temporary road blocks](https://github.com/RocketChat/Rocket.Chat/issues/533#issuecomment-140627021)
in adding PostgreSQL compatibility.
How quickly these are solved will determine if GitLab 8.1 will ship
with Rocket Chat or whether it will be delayed.

## SSL Verification for Web Hooks

We've now enabled SSL verification for web hooks by default.
This makes web hooks safer to use and helps mitigate man-in-the-middle attacks.

You can turn this off in the web hook settings of a project.

![Configure SSL verification of Web Hooks](/images/8_0/webhooks.png)

* [View the documentation for Web Hooks](http://doc.gitlab.com/ce/web_hooks/web_hooks.html)

## Public User Profile and Group Pages

In GitLab 8.0 all users and groups will have a publicly visible profile page.
This removes some complexity and makes it clear why you can't claim a name
(which previously allowed you to find out what names existed).
Private and internal projects will not be shown on these profile pages unless
you're allowed to see them.

## Notification Settings within the Project's main page

With GitLab 8.0 you will be able to set the project notifications setting
right from the project's dashboard. You can now quickly control how much
information you'll get from each project.

![Project Notifications](/images/8_0/notifications.png)

## Other changes

This release has more improvements, including security fixes.
Please check out [the Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG)
to see all of the named changes.

## Upgrade barometer

GitLab 8.0 can be upgraded online. Do note that if you are using GitLab CI,
you will have to perform a manual migration, see below. In addition,
there is a small change of behavior in GitLab CI, described directly below.

If you installed GitLab from source, or if you disabled the built-in
NGINX in the Omnibus packages, then you need to manually update
your web server configuration to make it use gitlab-git-http-server.

### .gitlab-ci.yml usage in GitLab CI

In GitLab 7.12 .gitlab-ci.yml files were introduced to specify build configurations.
If there was no file yet CI would fall back to the legacy build script,
which was stored in the database.

With GitLab 8.0, CI will not pick up any builds from projects / branches without
a `.gitlab-ci.yml` file present. Configuring a `.gitlab-ci.yml` is not difficult.

* [Documentation on configuring a `.gitlab-ci.yml` file](http://doc.gitlab.com/ci/yaml/README.html)

### GitLab CI Migration

GitLab 8.0 integrates GitLab CI in GitLab. Depending on your current usage of
GitLab CI, this could mean you have to perform a migration that merges your
GitLab CI data into GitLab.

If you're currently not using GitLab CI
you do not have to do anything in regards to GitLab CI.

If you have an active GitLab CI instance, you will need to follow our
[CI migration guide](http://doc.gitlab.com/ce/migrate_ci_to_ce/README.html)
to persist your data and registered runners. It is *necessary* to go to 8.0 first,
or you will lose all your build history. Once 8.1 and above have been released,
you can force the installation of 8.0 with the following commands, depending on
your operating system:

```
sudo apt-get install gitlab-ee=8.0.5-ee.0

sudo yum install gitlab-ee-8.0.5-ee.0.el6.x86_64

sudo yum install gitlab-ee-8.0.5-ee.0.el7.x86_64
```

This is an involved migration, especially if GitLab CI is running on a separate
server. It can be performed while GitLab is online, but GitLab CI will have
downtime.

Note that even if you do not care about persisting your CI data through the
migration, there is a chance that you have to perform some cleanup.
Please read [the migration document](http://doc.gitlab.com/ce/migrate_ci_to_ce/README.html).


<span id="reverse-proxy-settings"></span>
### Non-omnibus web servers and gitlab-git-http-server

All GitLab installations use a reverse proxy server to shield the
main Ruby application server (Unicorn) from handling requests it
is not 'good at'. The recommended reverse proxy for GitLab is NGINX,
but some people also use Apache. Because GitLab 8.0 uses
gitlab-git-http-server upgrading to 8.0 requires changes in the
reverse proxy configuration. If you are using Omnibus packages with
the built-in NGINX server (which is the default) then these reverse
proxy changes happen automatically when you upgrade to 8.0 and you
can stop reading this section.

If you have an installation from source, or if you use the Omnibus
packages with your own reverse proxy (be it NGINX or Apache) then
you must upgrade your reverse proxy settings to direct Git HTTP
requests to gitlab-git-http-server instead of Unicorn. If you do
not do this, all Git push/pull requests to your GitLab 8.0 server
will either fail or return empty repositories.

If you use an installtion from source you also need to update your
GitLab init script so that it will start/stop gitlab-git-http-server
along with other GitLab services.

Please see the [7.14 to 8.0 update
guide](http://doc.gitlab.com/ce/update/7.14-to-8.0.html) for more
information on the new reverse proxy settings.
### Default upgrade behavior

Please be aware that by default the Omnibus packages will stop, run
migrations, and start again, no matter how 'big' or 'small' the
upgrade is. The behaviour can be changed by adding a
[/etc/gitlab/skip-auto-migrations
file](http://doc.gitlab.com/omnibus/update/README.html).

### Community Jenkins integration

One of the biggest improvements of GitLab 8.0 is integrated GitLab CI.
Doing that required large amount of changes, including rebuild of the GitLab CI Service in GitLab.
With all these changes we removed the GitLabCiService. This change broke the Jenkins [gitlab-plugin](https://github.com/jenkinsci/gitlab-plugin) that allowed Jenkins to act as an external GitLab CI in front of GitLab.

You can still use [mentioned plugin](https://github.com/jenkinsci/gitlab-plugin) with GitLab. For all Web Hooks that you added you need to enable not only *Merge Request Events*, but also *Push and Tag Events*. By doing that GitLab will properly notify Jenkins when you do **git push**. This doesn't resolve missing build status for Jenkins builds in GitLab interface. We are working hard to bring the Commit Status API that will allow any external service to post the build status back to GitLab. When this gets implemented by the maintainer of this plugin it will make the integration much better then it was in versions prior to 8.0.

- - -

## Installation

If you are setting up a new GitLab installation please see the
[download GitLab page](https://about.gitlab.com/installation/).

## Updating

Check out our [update page](https://about.gitlab.com/update/).

## Enterprise Edition

GitLab Enterprise Edition offers additional features for organisations.
For a complete overview please have a look at the [feature list of GitLab EE](http://www.gitlab.com/gitlab-ee/).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/pricing/).
No time to upgrade GitLab yourself?
A subscription also entitles you to our upgrade and installation services.

- - -
