---
title: "Omnibus packages with OpenSSL 1.0.1p"
date: 2015-07-10
author: Jacob Vosmaer
author_twitter: jacobvosmaer
---
We have just released new Omnibus packages for GitLab Community Edition, GitLab Enterprise Edition and GitLab Continuous Integration.
These new packages contain an OpenSSL security update.

<!-- more -->

Yesterday a [new version of OpenSSL](http://openssl.org/news/secadv_20150709.txt) was released to address security vulnerability CVE-2015-1793.
This vulnerability, present in OpenSSL 1.0.1n and 1.0.1o, allows an attacker to trick an SSL client into accepting an untrusted server certificate.
This OpenSSL issue affects the Omnibus packages for GitLab 7.12 and newer because they contain OpenSSL 1.0.1o.
Older GitLab packages contain older versions of OpenSSL which are not affected by this particular issue.
This issue only affects outgoing SSL connections initiated by GitLab such as webhooks and 'git clone' repository imports.
Incoming HTTPS requests are not affected (unless you use client side SSL certificates which is very uncommon).

If you installed GitLab from source you need to check whether the OpenSSL version provided by your operating system is affected.
Omnibus users should upgrade to the 7.12.2-omnibus.1 packages and run `sudo gitlab-ctl restart` to make sure the latest version of OpenSSL is used.

Please see our [Update page](https://about.gitlab.com/update) for update instructions.
Coming from 7.12.x this upgrade requires short downtime because of `gitlab-ctl restart`.