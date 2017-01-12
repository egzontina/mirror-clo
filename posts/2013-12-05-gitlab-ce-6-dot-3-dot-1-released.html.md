---
title: "GitLab 6.3.1 security release"
date: 2013-12-05
author: Jacob Vosmaer
categories: release
community: true
---
### GitLab 6.3.1 security release
We have just released GitLab Community Edition 6.3.1 and GitLab Enterprise Edition 6.3.1 in response to this week's [Ruby on Rails security update 3.2.16](http://weblog.rubyonrails.org/2013/12/3/Rails_3_2_16_and_4_0_2_have_been_released/).
We advise all our users to upgrade to GitLab Community Edition 6.3.1 or GitLab Enterprise Edition 6.3.1 immediately.

<!--more-->

Ruby on Rails security update 3.2.16 addresses four security issues, including [denial of service through memory exhaustion](https://groups.google.com/d/msg/ruby-security-ann/A-ebV4WxzKg/KNPTbX8XAQUJ).

Versions affected: all

Versions fixed: GitLab Community Edition 6.3.1, GitLab Enterprise Edition 6.3.1

### Releases
GitLab Community Edition 6.3.1 is available at [GitLab Cloud](https://gitlab.com/gitlab-org/gitlab-ce) and [GitHub](https://github.com/gitlabhq/gitlabhq).
GitLab Enterprise Edition 6.3.1 is available for subscribers at [GitLab Cloud](https://gitlab.com).
Update instructions can be [found](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/update/patch_versions.md) [here](https://github.com/gitlabhq/gitlabhq/blob/master/doc/update/patch_versions.md).

### Workarounds
Users who cannot upgrade can address address the DoS vulnerability by applying [this patch based on the workaround provided by Rails](/files/0001-Monkey-patch-for-CVE-2013-6414.patch) in `/home/git/gitlab` with `git am` and restarting GitLab.
