---
title: "GitLab CE 6.5 released"
date: 2014-01-21 13:11
categories: release
community: true
---

### GitLab CE 6.5 released!

Hello everyone!

As you know GitLab is open source software to collaborate on code.
Today we released a new version of GitLab Community Edition (CE), with new features and bug fixes.

The main change of this release is the upgrade to the [Twitter Bootstrap 3](http://getbootstrap.com/) front-end framework, up from version 2.
This makes the GitLab UI more responsive and it also gives a fresh look for some of the UI controls.

We also improved the comments system: new comments are loaded with AJAX and we have fixed the comment anchor bug.
Jason Blanchard brought us the ability to change the issue assignee and milestone directly from issue page.
He is the MVP of this month.

This release fixes a security issue with Server generated Javascript Responses ([SJR](http://37signals.com/svn/posts/3697-server-generated-javascript-responses)). We advise everyone to upgrade.

<!--more-->

## New features:

### Customize merge commit message

When you accept a Merge Request in GitLab 6.5 the title and description of the MR will automatically be included in the merge commit.
You can also edit the merge commit if you like.
This feature was sponsored by [Say Media](http://www.saymedia.com/).

_WARNING:_ Be careful not to include text that should stay outside your Git commit history in the title or description of a Merge Request.

[![screenshot](/images/6_5/merge.png)](/images/6_5/merge.png)


### Responsive UI

With Bootstrap 3 we support devices with resolution 768x1024 and higher.

Below are a few screenshots of GitLab 6.5 taken with an iPad 2.


#### Portrait
<div class="inline-images">
<a href="/images/6_5/ipad1.png"><img src="/images/6_5/ipad1.png" alt="screenshot" title="" /></a>
<a href="/images/6_5/ipad3.png"><img src="/images/6_5/ipad3.png" alt="screenshot" title="" /></a>
</div>


#### Landscape
<div class="inline-images">
<a href="/images/6_5/ipad2.png"><img src="/images/6_5/ipad2.png" alt="screenshot" title="" /></a>
<a href="/images/6_5/ipad4.png"><img src="/images/6_5/ipad4.png" alt="screenshot" title="" /></a>
</div>


### Change the assignee directly from the issue page

Dropdown menus on the issue show page for the assignee and milestone allow users to update these fields directly without having to go to the 'Edit Issue' screen first.
Thank you Jason Blanchard!

[![screenshot](/images/6_5/issue.png)](/images/6_5/issue.png)


### New repository download formats: tar.bz2, zip, tar

Now you can download repositories in the format you prefer.
Thank you Jason Hollingsworth!

[![screenshot](/images/6_5/download.png)](/images/6_5/download.png)


### New filters (assigned/authored/all) for Dashboard#issues and Dashboard#merge_requests

We have added new filters to the user's Dashboard Issue and Merge Request index.
This feature was sponsored by [Say Media](http://www.saymedia.com/).

[![screenshot](/images/6_5/filters.png)](/images/6_5/filters.png)

### Create binary files via the GitLab API
It is now possible to select Base64 as the encoding when [creating a file through the GitLab API](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/api/repositories.md#toc_12).
This feature was sponsored by [O'Reilly Media](http://www.oreilly.com/).

- - -

# Links

For a full list of changes see the [CHANGELOG](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG).

If you are setting up a new GitLab installation see the [installation section of the README](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/README.md#toc_6).

For update instructions see the [Update Guide](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/6.4-to-6.5.md). If you have GitLab 6.4.2 you can try our [upgrade script](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/upgrader.md).

For LDAP group support and more have a look at the [feature list of GitLab Enterprise Edition](http://www.gitlab.com/gitlab-ee/).
Access to GitLab Enterprise Edition is included with a [GitLab.com subscription](http://www.gitlab.com/subscription/).
No time to upgrade or maintain Gitlab yourself?
GitLab.com also offers upgrade and installation services as part of a [GitLab.com subscription](http://www.gitlab.com/subscription/) or alternatively on a [consultancy basis](http://www.gitlab.com/consultancy/).
