---
title: "GitLab 7.12.2 released"
date: 2015-07-03
author: Jacob Vosmaer
author_twitter: jacobvosmaer
---

Today we released version 7.12.2 of GitLab Community Edition, GitLab Continuous Integration and GitLab Enterprise Edition.
This version reverts a breaking change in GitLab CI 7.12.1 and fixes RPM upgrade problems.

<!-- more -->

## GitLab CI runner tags and runners without tags

GitLab CI builds and runners can be tagged.
This allows you to do things like running different builds on different platforms: some on Linux, some on Windows.
GitLab CI 7.12.0 and earlier would send tagged builds to runners without tags.
This is not what we intended and we 'fixed' it in 7.12.1.
But now we [found out](https://gitlab.com/gitlab-org/gitlab-ci/issues/210) that some users were depending on untagged runners running tagged builds.
A breaking change like this does not belong in a patch release (7.12.1) so in GitLab CI 7.12.2 we are bringing back the old behavior.
The change will come back in GitLab CI 7.13.0.

## Omnibus RPM upgrades

In the GitLab 7.12.0 and 7.12.1 RPM packages we were seeing an [issue](https://gitlab.com/gitlab-org/omnibus-gitlab/issues/649) where right after `yum update`, GitLab would not be in a correctly configured state.
A file called `.gitlab_shell_secret` was going missing.
This problem could and can be solved quickly by running `gitlab-ctl reconfigure` manually after upgrading.
It was caused by an unfortunate interaction of a packaging change we made and the way that RPM handles package upgrades.
We included a fix in the GitLab 7.12.2 packages that removes the need for the second manual `gitlab-ctl reconfigure`.

## Other fixes

We also fixed a CSS alignment issue in GitLab Enterprise Edition and an Oauth integration bug in both Community Edition and Enterprise Edition.


For more details on the changes please see the
[CE](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG),
[EE](https://gitlab.com/gitlab-org/gitlab-ee/blob/master/CHANGELOG-EE),
[CI](https://gitlab.com/gitlab-org/gitlab-ci/blob/master/CHANGELOG), and
[Omnibus](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/CHANGELOG.md)
CHANGELOGs.

Please see our [Update page](/update/) for update instructions.
Coming from 7.12.0 or 7.12.1, updating to 7.12.2 does not require downtime.
