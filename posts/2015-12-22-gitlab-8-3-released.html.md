---
title: "GitLab 8.3 released with Auto-merge and GitLab Pages"
date: 2015-12-22
categories: release
author: Job van der Voort
author_twitter: jobvo
image_title: /images/unsplash/building.jpg
---

We're closing this fantastic year for GitLab with its 49th consecutive monthly
release, GitLab 8.3.

We're very grateful for all the people that have contributed to this release.
You can now merge automatically after a build has passed, we're introducing
GitLab Pages for Enterprise Edition, and issues have new powers in both CE and
EE!

Once again we've received some amazing contributions from our volunteers. This
month's Most Valuable Person ([MVP](https://about.gitlab.com/mvp/)) is Greg
Smethells. Greg made the proposal for and [subsequently implemented](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/1991)
the new references in issues and merge requests. He communicated his every move
and worked together closely with many other people from the community.

Thanks, Greg!

<!--more-->

## GitLab Pages (EE only)

GitLab Pages allows you to host a static website on your GitLab instance,
that is automatically deployed and updated, all from a normal GitLab project.

With [the last release of GitLab](https://about.gitlab.com/2015/11/22/gitlab-8-2-released/)
we shipped Build Artifacts for CI.
This means that your builds can have some sort of output.
We leveraged this to build GitLab Pages.

So if you have an open source project that you want to give a proper website,
you can now do it straight from your repository.

Have documentation that you want to feature nicely? Use pages to create a
clean experience for your users.

As GitLab.com runs GitLab Enterprise Edition, you can now use that for your
static sites for free. Your projects will be served on `namespace.gitlab.io/project_name`.

We plan to add CNAME and SSL support
[in an upcoming GitLab release](https://gitlab.com/gitlab-org/gitlab-ee/issues/134).
Right now, if you want to use SSL, you need a wildcard certificate for your
domain.

[See the documentation for GitLab Pages](http://doc.gitlab.com/ee/pages/README.html)

If you encounter any problems or have any feature proposals, please open an
issue in the [EE issue tracker](https://gitlab.com/gitlab-org/gitlab-ee/issues).

## Auto-merge on Build Success

If you've reviewed a merge request, but the CI builds are still running,
it can be annoying to have to wait for them to finish.

![Merge on Build Success in GitLab 8.3](/images/8_3/merge_on_pass.jpg)

By default, we will now show you a button that will merge the MR when
the build succeeds. Less waiting, more reviewing!

Thanks to [Zeger-Jan van de Weg](https://twitter.com/zjvandeweg) for
[his contribution](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/1729)!

- [See the documentation on Auto-merge](http://doc.gitlab.com/ce/workflow/merge_when_build_succeeds.html)

## Contribution Analytics (EE only)

In order to make it easy to see how and where are active in your projects,
we're building contribution analytics for Enterprise Edition.

In GitLab 8.3, you can now quickly get an overview of activity of a group
by going to **Group -> Contribution Analytics** at `groups/groupname/analytics`.

![Get contribution analytics in GitLab 8.3 EE](/images/8_3/stats.jpg)

We intend to expand contribution analytics in future
releases of GitLab. We're curious to hear your thoughts and feature proposals.

## Merge Request References in Issues

An issue is often followed by one or multiple merge requests.
Thanks to the great contribution of Greg, you are now able to quickly
see all referenced merge requests with their status (Open / Closed / Merged)
and even their build status (Success / Running / Failed) in an issue!

![See referenced merge requests in issues in GitLab 8.3](/images/8_3/references.jpg)

This makes it much easier to see the current status of an issue and find all related
code, reviews and commits.

## Issue Weight (EE only)

When you have a lot of issues, it can be hard to get an overview.
By adding a weight to each issue, you can get a better idea of how much time,
value, or complexity a given issue has or will cost.

To set the weight of issue, simply change the value in the dropdown menu.
You can set it to a numeric value from 1 to 9.

![Issue Weights in GitLab EE 8.3](/images/8_3/weights1.jpg)

This value will appear in the issues list and on issues themselves, and you can
see the total sum of all issues on the milestone page.

## Quickly create a new MR from the web editor

You know you should create a merge request, but it's so appealing to quickly
fix something in GitLab's editor and push it to the master branch.

To prevent you from being naughty these holidays and onward, we've added
a quick option to create a merge request from your changes in the editor.

![Quickly create a new MR from the web editor in GitLab 8.3](/images/8_3/new_mr.jpg)

Get your commit reviewed and let your CI run before you push to master!

## Builds in Merge Requests

As your merge requests trigger builds to run in CI, you now have quick
access to them in the **Builds** tab.

![See your CI Builds in MRs in GitLab 8.3](/images/8_3/builds.jpg)

This makes it much easier to see what is failing, making it even easier to work
with CI in code review.

As this is another step into integrating CI in GitLab, we're
working hard on bringing more of these improvements. Have any ideas?
Share them by submitting a feature proposal or a merge request!

## Automatic References

You might know that you can reference anything from anywhere in GitLab,
using the simple syntax of `group/projectREF`, for instance to reference
issue 1 in the GitLab CE repo you can do `gitlab-org/gitlab#1`.

We now automatically generate those references for you when posting a URL from
within your GitLab instance. So:
`https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/1991` becomes
`gitlab-org/gitlab-ce!1991`. This makes reading issues much cleaner.

## JIRA support in GitLab CE

Full JIRA integration was previously exclusive to GitLab Enterprise Edition.
With GitLab 8.3 forward, everyone has access to advanced JIRA integration in GitLab.

You can now connect GitLab with JIRA, making it possible to close JIRA tickets
with commit messages and reference JIRA tickets from within GitLab.

Our JIRA integration automatically provides context and links back to
GitLab issues, merge requests, users, and commits whenever you reference
a JIRA ticket.

If you're currently using JIRA, we're curious to hear how we can improve
further integration.

Configure the new settings for JIRA support in your projects under
**Settings -> Services -> JIRA**.

## CI Improvements

With merging GitLab CI into GitLab [with GitLab 8.0](https://about.gitlab.com/2015/09/22/gitlab-8-0-released/)
we set out on a path of integrating two separate codebases.

With GitLab 8.3, we conclude this path, as all CI code has been fully integrated
in GitLab and refactored and cleaned where necessary.

This should make it easier to contribute to the development of GitLab CI and
makes way for further integration those crucial CI tools in GitLab.

## Other changes

This release has more improvements, including security fixes. Please check out [the Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG) to see the all named changes.

### Decoupling GitLab from NGINX

In GitLab 8.3 we are making a major behind the scenes change in how
GitLab works: all HTTP requests are now proxied through
gitlab-workhorse. We have moved most if not all GitLab-specific
configuration from the NGINX configuration files into gitlab-workhorse.

This change will make it easier for GitLab developers to add features
and improve GitLab using gitlab-workhorse because they no longer have
to work in three places: the Rails application, gitlab-workhorse, and
NGINX. This change is also making it simpler to deploy GitLab from
source, and simpler to use GitLab with Apache or HAproxy when so
desired, because the contact surface between GitLab and its reverse
proxy is now much smaller.

We are still recommending to run GitLab with NGINX because it offers
request/response buffering (not yet implemented in gitlab-workhorse)
and SSL termination (not planned for gitlab-workhorse).

If you are using our Omnibus packages and its built-in NGINX service
then no action is needed when upgrading. If you installed GitLab from
source or if you are using your own reverse proxy then you will have
to check your init script (gitlab-workhorse got some new settings) and
reverse proxy configuration. The [8.3 update
guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/8.2-to-8.3.md)
has more details.

Those of you who run GitLab at a "relative URL" (example.com/gitlab)
will be pleased to hear that gitlab-workhorse now supports relative
URLs.

### Mattermost 1.3

We're shipping Mattermost 1.3 with GitLab 8.3.
See the [release post for Mattermost 1.3](http://www.mattermost.org/mattermost-a-top-10-open-source-project-of-2015/)
for details.

## Upgrade barometer

If you are upgrading from GitLab 8.2 and none of your users are using GitLab CI
then you can perform the upgrade to 8.3 without downtime.

Be advised that if you are not using the Omnibus packages and its built-in NGINX
settings, you will have to update your Nginx/Apache settings when upgrading to 8.3.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

### If you are using CI

If you are using CI, there are migrations that will have to be performed offline.

As noted above, we're migrating almost all database models of CI.
The migration of the CI services are somewhat lossy:
Slack and HipChat notifications will only migrate if they are **enabled**
before the migration.

These migrations took 280 seconds on GitLab.com on PostgreSQL (~500k projects).
We expect this to be a little longer for MySQL databases.

### Jenkins Integration Changes (EE only)

Jenkins integration using the
[GitLab Hook Plugin](https://wiki.jenkins-ci.org/display/JENKINS/GitLab+Hook+Plugin)
was deprecated in favor of the
[GitLab Plugin](https://wiki.jenkins-ci.org/display/JENKINS/GitLab+Plugin).
This plugin enables closer integration between Jenkins and GitLab, including the display of build status on each commit and on the project home page. Previously, build status was only available in a merge request.
The deprecated integration has been renamed to 'Jenkins CI (Deprecated)' and will continue to work for existing users. We may remove this in a future release and recommend
using the new 'Jenkins CI' project service instead. See [GitLab Jenkins documentation](http://docs.gitlab.com/ee/integration/jenkins.html) for more details.

### Notes on upgrading from before 8.0

*Note* If you are upgrading from a GitLab version prior to 8.0 *and* you have CI enabled, you have to upgrade to GitLab 8.0 [first](https://about.gitlab.com/2015/09/22/gitlab-8-0-released/).

- - -

## Installation

If you are setting up a new GitLab installation please see the
[download GitLab page](https://about.gitlab.com/installation/).

## Updating

Check out our [update page](https://about.gitlab.com/update/).

## Enterprise Edition

The mentioned EE-only features and things like LDAP group support can be found in GitLab Enterprise Edition.
For a complete overview please have a look at the [feature list of GitLab EE](http://www.gitlab.com/gitlab-ee/).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/pricing/).
No time to upgrade GitLab yourself?
A subscription also entitles you to our upgrade and installation services.

- - -
