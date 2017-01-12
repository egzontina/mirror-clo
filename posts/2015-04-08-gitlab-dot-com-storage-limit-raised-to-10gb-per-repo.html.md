---
title: "GitLab.com storage limit raised to 10GB per repo"
date: 2015-04-08
author: Sytse Sijbrandij
author_twitter: sytses
image_title: '/images/unsplash/milkyway.jpg'
---

We want to congratulate GitHub on [launching git-lfs today](https://github.com/blog/1986-announcing-git-large-file-storage-lfs), their method for storing large files.
Their command line client looks easy to use since you can use existing git commands, a very nice innovation.

We think that a solution for storing large files will benefit the entire git ecosystem.
GitLab.com and GitLab Enterprise Edition have included support for the open source git-annex [since February](https://about.gitlab.com/2015/02/17/gitlab-annex-solves-the-problem-of-versioning-large-binaries-with-git/).
GitHub has based their solution on git-media but chose to make it a new format.

We would love to see one standard emerge over time and we're glad to see that git-lfs is open source and that they [didn't call it assman](https://github.com/github/git-lfs/commit/10a8eceefdb081edf6114eda6f68c1f4db204a96).
We hope that going forward development happens in the open so that the different large file solutions can grow to a unified solution.

To celebrate today's good news we've permanently raised our storage limit per repository on GitLab.com from 5GB to 10GB. As before, public and private repositories on GitLab.com are unlimited, don't have a transfer limit and they include unlimited collaborators.
