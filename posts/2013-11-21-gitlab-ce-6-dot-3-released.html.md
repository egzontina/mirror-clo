---
title: "GitLab CE 6.3 released"
date: 2013-11-21 10:19
author: Dmitriy Zaporozhets
categories: release
community: true
---

### GitLab CE 6.3 released!

Hello everyone!

Today we released a new version of GitLab Community Edition (CE), with new features, bug fixes, security patches and stability improvements.
GitLab is open source software to collaborate on code.
The main new feature of the 6.3 release is the ability to create and remove files through the web UI.
Because of the security patches we advise everyone to upgrade to this version as soon as possible.

### Create files from the web interface

You can now create new text files directly from the web interface.
To create a new file go to the directory where you want to create the new file and click the '+' button next to the directory name.

[![screenshot](/images/6_3/new-file-1.png)](/images/6_3/new-file-1.png)

Now you can specify the file name, commit message and content in the form.
The new commit will be added to the branch you were browsing when you clicked '+'.

[![screenshot](/images/6_3/new-file-2.png)](/images/6_3/new-file-2.png)

<!--more-->

### Remove files through the web interface

It is also possible to delete files from the web interface using the new 'remove' button in the file view.

[![screenshot](/images/6_3/remove-file-1.png)](/images/6_3/remove-file-1.png)

Because we are making a new commit we must specify a commit message.
The commit is added to the branch you were viewing the file in.

[![screenshot](/images/6_3/remove-file-2.png)](/images/6_3/remove-file-2.png)

### Broadcast messages

Email is not always the best way to inform users about server maintenance.
With the new 'Broadcast Messages' feature administrators can add messages that will be displayed to all users as a banner during a specific time interval.

To add a broadcast message go to the new 'Messages' tab in the admin interface and enter a new message, along with start and end times to determine when the message will be visible to your users.

[![screenshot](/images/6_3/broadcast.png)](/images/6_3/broadcast.png)

The message will appear to your users as a banner at the top of the screen.

[![screenshot](/images/6_3/broadcast-show.png)](/images/6_3/broadcast-show.png)

### Project transfer

Administrators can now transfer projects directly from the admin interface, without having to visit the user-facing project settings screen.
This change also allows administrators to move projects to any existing namespace.

[![screenshot](/images/6_3/admin-transfer.png)](/images/6_3/admin-transfer.png)

### Leaving a project

Previously the only way to leave a project was to ask the owner to remove you.
Now you can leave projects without owner intervention: just visit the 'Projects' tab on the main dashboard.

[![screenshot](/images/6_3/leave-page.png)](/images/6_3/leave-page.png)

### Admin dashboard improvements

Want to know which version of gitlab-shell you are using or whether Gravatar is enabled?
You can now see version and configuration information for your GitLab installation on the Admin dashboard.

[![screenshot](/images/6_3/admin.png)](/images/6_3/admin.png)

### See which branches contain a commit

When viewing a commit you now see links to all branches this commit is contained in.
Thanks to Andrew Kumanyaev for contributing this feature!

[![screenshot](/images/6_3/commit.png)](/images/6_3/commit.png)

### Project home page

We have done a minor redesign of the project home page view to improve the flow and balance of the page.
We hope you like it!

[![screenshot](/images/6_3/project.png)](/images/6_3/project.png)

This release's most valuable person (MVP) is __Andrew Kumanyaev __ for contributing the 'which branches contain this commit?' feature.

- - -

# Links

For a full list of changes see the [CHANGELOG](https://github.com/gitlabhq/gitlabhq/blob/master/CHANGELOG).

If you are setting up a new GitLab installation see the [installation section of the README](https://github.com/gitlabhq/gitlabhq/blob/master/README.md#installation).

__For update instructions see the [Update Guide](https://github.com/gitlabhq/gitlabhq/blob/master/doc/update/6.2-to-6.3.md).__

For LDAP group support and more have a look at the [feature list of GitLab Enterprise Edition](http://www.gitlab.com/gitlab-ee/).
Access to GitLab Enterprise Edition is included with a [GitLab.com subscription](http://www.gitlab.com/subscription/).
No time to upgrade or maintain Gitlab yourself?
GitLab.com also offers upgrade and installation services as part of a [GitLab.com subscription](http://www.gitlab.com/subscription/) or alternatively on a [consultancy basis](http://www.gitlab.com/consultancy/).
