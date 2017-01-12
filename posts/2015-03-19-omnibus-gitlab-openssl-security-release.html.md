---
title: Omnibus GitLab OpenSSL 1.0.1m security release
date: 2015-03-19
author: Marin Jankovski
---

The OpenSSL developers released a [security
advisory](http://openssl.org/news/secadv_20150319.txt) today advising
all users of OpenSSL 1.0.1 to upgrade to version 1.0.1m in light of
vulnerabilities CVE-2015-0204, CVE-2015-0286, CVE-2015-0287, CVE-2015-0289,
CVE-2015-0292, CVE-2015-0293, CVE-2015-0209 and CVE-2015-0288.

This affects users of omnibus-gitlab because
omnibus-gitlab packages contain their own copy of OpenSSL 1.0.1. Today we are
releasing new omnibus packages for GitLab 7.8.4 CE and GitLab 7.8.4 EE which
contain OpenSSL 1.0.1m.

For installations from source we advise you to upgrade your openssl version using the OS package manager.
If openssl was compiled from source we advise you to compile the new version.

<!-- more -->

Versions affected: omnibus-gitlab 7.8.4.omnibus and older, omnibus-gitlab
7.8.4-ee.omnibus and older.

Versions fixed: omnibus-gitlab 7.8.4.omnibus.1, omnibus-gitlab
7.8.4-ee.omnibus.1.

# Checking your omnibus-gitlab OpenSSL version

You can check the version of OpenSSL in your omnibus-gitlab installation by
running the following command.

```
grep openssl /opt/gitlab/version-manifest.txt
```

If the OpenSSL version is 1.0.1j or lower you need to update omnibus-gitlab to
the latest version.

After the update is done, make sure that you restart GitLab so all processes can get the new version of openssl.

You can initiate the restart with `sudo gitlab-ctl restart`.

# Downloads

Updated omnibus-gitlab packages for [GitLab Community
Edition](https://about.gitlab.com/downloads/) and [GitLab Enterprise
Edition](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/install/packages.md)
are available for download.

Please contact us at support@gitlab.com if you have any questions.
