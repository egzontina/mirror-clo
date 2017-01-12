---
title: "GitLab 7.10.0 Omnibus patch release"
date: 2015-04-23
categories: release
author: Jacob Vosmaer
author_twitter: jacobvosmaer
---

We have just released new Omnibus packages for GitLab 7.10 that address issues
with outgoing SSL connections for GitLab and GitLab CI. The new packages also
contain instructions to work around RPM upgrade issues going from GitLab 7.9 or
earlier to 7.10 or later.

<!-- more -->

## Outgoing SSL connection issues

GitLab Omnibus packages contain a copy of the mozilla.org CA certificate bundle
[as distributed by the cURL project](http://curl.haxx.se/docs/caextract.html).
These CA certificates are required to verify SSL peer identities during
outgoing SSL connections such as API calls made by GitLab and GitLab CI. Due to
a build error, the CA certificate bundle file included in the original 7.10
Omnibus packages had incorrect permissions, denying access to GitLab processes.
The result is that it is as if the original 7.10 packages came with no trusted
CA certificates at all. The new Omnibus packages released today address this
issue.

If you cannot upgrade straightaway, you can use the following workaround for
this problem:

```
sudo chmod 644 /opt/gitlab/embedded/ssl/certs/cacert.pem
sudo gitlab-ctl restart
```

## <a id="rpm-upgrade-issues"></a> RPM upgrade issues

Motivated by our move to distributing GitLab Omnibus packages via
[packages.gitlab.com/gitlab](https://packages.gitlab.com/gitlab) we have
renamed our Omnibus packages from plain 'gitlab' to 'gitlab-ce' and 'gitlab-ee'
respectively. When you upgrade from GitLab 7.9 or earlier to the latest Omnibus
packages, the package system will detect a 'conflict' and remove 'gitlab' in
favor of 'gitlab-ce' or 'gitlab-ee'.

It has come to our attention that due to the order in which RPM post-removal
and post-installation scripts run, this change from 'gitlab' to
'gitlab-ce'/'gitlab-ee' removes `/usr/bin/gitlab-ctl` and related commands.
This issue does not affect Debian-based systems.

As a workaround on RPM-based systems, please run the following command _after_
upgrading to GitLab 7.10 or newer:

```
sudo ln -sf                       \
  /opt/gitlab/bin/gitlab-ctl      \
  /opt/gitlab/bin/gitlab-rake     \
  /opt/gitlab/bin/gitlab-rails    \
  /opt/gitlab/bin/gitlab-ci-rake  \
  /opt/gitlab/bin/gitlab-ci-rails \
  /usr/bin/
```

The post-install message of the package will also tell you to make this change.

## Updates

Please see our [downloads page](/downloads) for installation instructions for
the latest packages.
