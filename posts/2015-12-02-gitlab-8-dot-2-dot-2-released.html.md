---
title: "GitLab 8.2.2 Released"
date: 2015-12-02
author: GitLab
author_twitter: gitlab
---

Today we are releasing version 8.2.2 for Community Edition (CE) and Enterprise
Edition (EE).

It includes the following fixes:

* **CE/EE:** Ensure GitLab fires custom update hooks after commit via UI ([#3069]).
* **CE/EE:** Expire application settings cache at startup ([#3643]).
* **CE/EE:** Fix raw private snippet access workflow ([#3677]).
* **CE/EE:** Prevent 500 error when viewing a user's projects from the admin area
  ([#3680]).
* **CE/EE:** Prevent 404 error after removing a project ([#3559]).
* **CE/EE:** Nginx should no longer block large LFS uploads ([#3708]).
* **EE:** Use configured shared path for rebase before merge ([#56]).

[#3069]: https://gitlab.com/gitlab-org/gitlab-ce/issues/3069
[#3559]: https://gitlab.com/gitlab-org/gitlab-ce/issues/3559
[#3643]: https://gitlab.com/gitlab-org/gitlab-ce/issues/3643
[#3677]: https://gitlab.com/gitlab-org/gitlab-ce/issues/3677
[#3680]: https://gitlab.com/gitlab-org/gitlab-ce/issues/3680
[#3708]: https://gitlab.com/gitlab-org/gitlab-ce/issues/3708
[#56]: https://gitlab.com/gitlab-org/gitlab-ee/issues/56

<!-- more -->

## Upgrade barometer

This version does not include any new migrations, and should not require any
downtime.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

***Note for installations from source:*** The installation and update guides for
versions 8.2 and 8.2.1 mistakenly included instructions that would leave
installations with an outdated version of `gitlab-shell`. Please ensure that you
have the correct required version (`2.6.8`) by performing the following
commands:

```sh
cd /home/git/gitlab-shell
sudo -u git -H git fetch
sudo -u git -H git checkout v2.6.8
```

## Updating

To update, check out our [update page](https://about.gitlab.com/update).

## Enterprise Edition

Interested in GitLab Enterprise Edition?
Check out the [features exclusive to GitLab EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/pricing).
No time to upgrade GitLab yourself?
Subscribers receive upgrade and installation services.
