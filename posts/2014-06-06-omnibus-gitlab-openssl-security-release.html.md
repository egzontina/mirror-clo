---
title: Omnibus-gitlab OpenSSL 1.0.1h security release
date: June 6, 2014
author: Jacob Vosmaer
---

The OpenSSL developers released a [security
advisory](https://www.openssl.org/news/secadv_20140605.txt) yesterday advising
all users of OpenSSL 1.0.1 to upgrade to version 1.0.1h in light of
vulnerabilities CVE-2014-0224, CVE-2014-0221, CVE-2014-0195, CVE-2014-0198,
CVE-2010-5298and CVE-2010-5298. This affects users of omnibus-gitlab because
omnibus-gitlab packages contain their own copy of OpenSSL 1.0.1. Today we are
releasing new omnibus packages for GitLab 6.9.2 CE and GitLab 6.9.3 EE which
contain OpenSSL 1.0.1h.

Versions affected: omnibus-gitlab 6.9.2.omnibus and older, omnibus-gitlab
6.9.3-ee.omnibus and older.

Versions fixed: omnibus-gitlab 6.9.2.omnibus.1, omnibus-gitlab
6.9.3-ee.omnibus.1.

## Checking your omnibus-gitlab OpenSSL version

You can check the version of OpenSSL in your omnibus-gitlab installation by
running the following command.

```
grep openssl /opt/gitlab/version-manifest.txt
```

If the OpenSSL version is 1.0.1g or lower you need to update omnibus-gitlab to
the latest version.

## Downloads

Updated omnibus-gitlab packages for [GitLab Community
Edition](https://www.gitlab.com/downloads) and [GitLab Enterprise
Edition](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/install/packages.md)
are available for download.

Please contact us at support@gitlab.com if you have any questions.
