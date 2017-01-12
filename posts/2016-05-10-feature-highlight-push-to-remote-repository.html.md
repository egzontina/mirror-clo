---
title: "Feature highlight: Push to a remote repository"
date: 2016-05-10
comments: true
author: Ivan Nemytchenko
author_twitter: inemation
---

Since GitLab Enterprise Edition 8.2 you could sync all changes from a remote repository to one on GitLab.

In GitLab 8.7 we introduced the second part of the mirroring functionality: the ability to push changes to an external repository from GitLab.

This means that now you can use GitLab as the main place for your development, and get all your changes pushed to another repository.
There are a number of reasons why it may be important to keep an existing repository in addition to your new GitLab repository:

- You can be tied with company policy to keep using the legacy system
- You want your existing git hosting service to keep playing the role of showcasing your project
- You don't want to spend time reconfiguring all your existing integrations

In any of these cases "Push to remote repository" might be your savior.

## Setting up

It can be configured in **Settings** → **Mirror Repository**:

![Settings: Push to a remote repository](/images/blogimages/push-to-remote-repository/settings.png)

It will be pushed every hour. You can also trigger it manually right from the project page:

![Trigger push to a remote repository](/images/blogimages/push-to-remote-repository/trigger.png)

## Playing with mirroring functionality

As an experiment, I built a chain of 3 repositories: [Bitbucket](https://bitbucket.org/ivannemytchenko/sync) → [GitLab](https://gitlab.com/inem/sync) → [GitHub](https://github.com/inem/sync).

Every change from the Bitbucket repository goes to GitLab, triggers build there (since I checked "Trigger builds for mirror updates" checkbox). Then all the changes are pushed to the repository at GitHub.

![Checkbox](/images/blogimages/push-to-remote-repository/checkbox.png)

As you can see, mirroring gives you an additional dimension of flexibility. You can use it to modify an existing workflow, or to build one from scratch.

"Push to remote repository" is a feature of GitLab Enterprise Edition (EE), which means that you can use it on your own GitLab EE instance or for free at GitLab.com.
GitLab.com is the free SaaS version of GitLab, running most of the features of GitLab EE.
