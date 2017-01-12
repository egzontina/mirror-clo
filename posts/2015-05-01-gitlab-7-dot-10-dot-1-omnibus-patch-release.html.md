---
title: "GitLab 7.10.1 Omnibus patch release"
date: 2015-05-01
categories: release
author: Marin Jankovski
author_twitter: maxlazio
---

We have just released new Omnibus packages for GitLab 7.10.1 that address issues
with duplicated settings.

<!-- more -->

GitLab Omnibus packages use [omnibus-ctl](https://github.com/chef/omnibus-ctl) for
service control and configuration management.

For GitLab 7.10, omnibus packages were updated to version 0.3.3 of `omnibus-ctl`.

This caused all settings to be cached in `/opt/gitlab/embedded/nodes/NODENAME.json` and with
that changes to settings in `/etc/gitlab/gitlab.rb` would appear as a new line in
file which contains the changed setting.

The new omnibus packages contain an upgraded version of omnibus-ctl which includes [the fix](https://github.com/chef/omnibus-ctl/issues/24)
for this problem.

If you cannot upgrade right away and you experienced duplicated settings in configuration files, you can use the following workaround for
this problem:

```bash
  sudo rm -rf /opt/gitlab/embedded/nodes
  sudo gitlab-ctl reconfigure
```

## Updates

Please see our [downloads page](/downloads) for installation instructions for
the latest packages.
