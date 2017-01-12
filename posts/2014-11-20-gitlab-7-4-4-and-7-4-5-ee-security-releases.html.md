---
title: "GitLab 7.4.4 and 7.4.5-ee security releases"
date: 2014-11-20
author: Jacob Vosmaer
categories: release
---

We have just released GitLab Community Edition 7.4.4 and GitLab Enterprise Edition 7.4.5 (7.4.5-ee).
These releases fix two cross-site scripting (XSS) vulnerabilities.
In addition to the security fixes, GitLab Enterprise Edition 7.4.5 also fixes an LDAP group synchronization regression.

<!--more-->

## XSS vulnerabilities via merge request and commit attributes

An attacker with commit acess to GitLab can inject malicious Javascript code into pages that show commits or merge requests.
This Javascript code would then be executed in the context of another user viewing the page on the GitLab server.

### Affected versions

GitLab Community Edition 7.4.3 and earlier.

GitLab Enterprise Edition 7.4.4 and earlier.

### Unaffected versions

None.

### Fixes

The two XSS issues have been fixed in GitLab Community Edition 7.4.4 and GitLab
Enterprise Edition 7.4.5.

### Acknowledgments

We would like to thank Hugh Davenport for their responsible disclosure of the XSS issues.

## LDAP group synchronization regression

Due to an oversight a bug fix for a regression in GitLab 7.4 Enterprise Edition found right before the 7.4 release did not get shipped.
Affected users would see an `Missing setting 'active_directory' in ` error message.
GitLab Enterprise Edition 7.4.5 includes the fix for this error.

## Upgrading

Omnibus-gitlab packages for GitLab 7.4.4 and 7.4.5-ee are [now
available](https://about.gitlab.com/downloads/). To upgrade an installation
from source please use the
[upgrader](http://doc.gitlab.com/ce/update/upgrader.html) or the [patch update
guide](http://doc.gitlab.com/ce/update/patch_versions.html).
