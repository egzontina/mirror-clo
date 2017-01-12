---
title: "GitLab CE 6.4 released"
date: 2013-12-21 12:20
author: Dmitriy Zaporozhets
categories: release
community: true
---

### GitLab CE 6.4 released!

Hello everyone!

As you know GitLab is open source software to collaborate on code.
Today we released a new version of GitLab Community Edition (CE), with new features, bug fixes, stability improvements and Rails 4 under the hood.
This month we have 2 MVPs because both of them contributed awesome stuff to GitLab 6.4.
Steven Thonus brought us the side-by-side diff view and the ability to archive old projects.
Jason Hollingsworth contributed the new 'internal projects' feature.


### Internal projects

Internal projects can be cloned and browsed by any logged in user.
It will also be listed on the public access directory for logged in users.

[![screenshot](/images/6_4/new-project.png)](/images/6_4/new-project.png)

<!--more-->

### Side-by-side diff view

The unified diff view is still the default but you now can also switch to a side-by-side diff view.

[![screenshot](/images/6_4/diff.png)](/images/6_4/diff.png)

### Archive old projects

Archiving a project will mark its repository as read-only.
It is hidden from the dashboard and it does not show up in searches.

[![screenshot](/images/6_4/arch.png)](/images/6_4/arch.png)

Archived projects you have access to will still be listed on your profile page (gitlab.example.com/u/my_user).


### Project webhooks

Project webhooks were extended with new types of events.
Webhooks can now also be triggered when an issue is created or a merge requst is closed.


[![screenshot](/images/6_4/hook.png)](/images/6_4/hook.png)

### Awesome sorting for the Issues page

Thanks to Jason Blanchard for contributing this very useful feature.

[![screenshot](/images/6_4/issues.png)](/images/6_4/issues.png)

### README link at the project home page

For projects that have a README that is recognized by GitLab you can now go straight to the README from the project home page.

[![screenshot](/images/6_4/readme.png)](/images/6_4/readme.png)


### And some good news for people who want easier upgrades

We included an upgrade script with GitLab CE 6.4.
This means you will be able to upgrade to next version (6.5) with just one command.

[![screenshot](/images/6_4/upgrade.png)](/images/6_4/upgrade.png)
[![screenshot](/images/6_4/upgrade2.png)](/images/6_4/upgrade2.png)


- - -

# Links

For a full list of changes see the [CHANGELOG](https://github.com/gitlabhq/gitlabhq/blob/master/CHANGELOG).

If you are setting up a new GitLab installation see the [installation section of the README](https://github.com/gitlabhq/gitlabhq/blob/master/README.md#installation).

__For update instructions see the [Update Guide](https://github.com/gitlabhq/gitlabhq/blob/master/doc/update/6.3-to-6.4.md).__

For LDAP group support and more have a look at the [feature list of GitLab Enterprise Edition](http://www.gitlab.com/gitlab-ee/).
Access to GitLab Enterprise Edition is included with a [GitLab.com subscription](http://www.gitlab.com/subscription/).
No time to upgrade or maintain Gitlab yourself?
GitLab.com also offers upgrade and installation services as part of a [GitLab.com subscription](http://www.gitlab.com/subscription/) or alternatively on a [consultancy basis](http://www.gitlab.com/consultancy/).
