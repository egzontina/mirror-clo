---
title: "Feature highlight: Git Hooks in GitLab Enterprise Edition"
date: 2014-08-25 13:11:30 +0200
author: Job van der Voort
---

Sometimes you need additional control over pushes to your repository. GitLab already offers protected branches. But there are cases when you need some specific rules like preventing git tag removal or enforcing a special format for commit messages. GitLab Enterprise Edition offers a user-friendly interface for such cases.

For each project you can have unique Git Hooks. You can set them by going to Project settings -> Git Hooks.

![Git Hooks](/images/features/git_hooks.png)

<!--more-->

Here you can simply set a regular expression that requires your rule in a commit message. For instance, if you want every commit to reference a JIRA issue such as `JIRA-123`, you could use an expression such as `/JIRA\-\d+/`.

In addition, you can prevent users from deleting tags through pushes.

We're very excited about Git Hooks and are looking to add more. If you are a customer of GitLab and require a Git Hook, [tell us](mailto:support@gitlab.com) and we can implement it for free.
