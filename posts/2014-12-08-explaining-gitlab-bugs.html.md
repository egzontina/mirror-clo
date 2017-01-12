---
title: "Explaining GitLab bugs"
date: 2014-12-08
categories: 
author: Marc Radulescu
---

This blog post will give a short overview on how GitLab bugs are handled, and what you can do after you identify a potential bug in GitLab.

The GitLab community differentiates between three different types of bugs:

 - Security bugs
 - Regression bugs
 - Feature bugs

<!-- more -->

The image below illustrates the big picture:

[![screenshot](/images/gitlab_bugs/bugs_alt.png)](/images/gitlab_bugs/bugs_alt.png)

## Security bugs

Security bugs are system vulnerabilities that can be exploited to allow a user to gain unauthorized access to the GitLab server.
The GitLab B.V. team always treats them as top priority.
We give feedback within 1-2 days of notice.
Depending on the severity of the vulnerability, we will either patch GitLab, or fix the issue in the next minor release.

If you find a security bug in GitLab, please make sure to use [responsible disclosure](https://about.gitlab.com/disclosure/), and reach out to the GitLab B.V. team at support@gitlab.com.

## Regression bugs

Regression bugs are bugs in the functionality of GitLab, that are unknowingly introduced in a new release.
These refer to features which used to work in an older version, but which are bugged in the current release.
Regression bugs are treated with priority.
We assess the impact of the regression bug and either create a patch or, more frequently, include the fix in the next minor release.

If you identify a regression bug, please share it to the GitLab community either via [Twitter](https://twitter.com/gitlabhq), or by posting it in the [issue tracker](https://gitlab.com/gitlab-org/gitlab-ce/issues).

## Feature bugs

GitLab's features don't cover all use and corner cases, so you might come across a feature that behaves different from what you'd expect.
If this is the case, and if the unexpected behavior is not a regression, it is considered a feature bug.
Depending on the impact on GitLab's functionality, fixing this kind of bug might be considered a priority.
Before announcing it the GitLab issue tracker, please make sure to double-check the community and our teams' comments on the feature on the feedback tracker, on the changelog and in the release blog post.

If you have a specific corner case that is not covered by the feature, please use the [feedback tracker](http://feedback.gitlab.com/forums/176466-general) to bring it to the community's attention.

If your use case is generic, and the feature is obviously buggy, please report it in the [issue tracker](https://gitlab.com/gitlab-org/gitlab-ce/issues).

##Contributing

The majority of GitLab bugs are found and fixed by the GitLab community.
There are more than 600 external contributors already. 
Whenever you find a bug in GitLab, you can also [contribute](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CONTRIBUTING.md) the fix, and add your contribution in the [changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG).
