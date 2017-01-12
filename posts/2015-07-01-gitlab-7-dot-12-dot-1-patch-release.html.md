---
title: "GitLab 7.12.1 patch release"
date: 2015-07-01
categories: release
author: Jacob Vosmaer
author_twitter: jacobvosmaer
---

Today we released GitLab 7.12.1 (Community Edition, Enterprise Edition and
Continuous Integration). This is a bug fix release.

<!-- more -->

GitLab Community Edition (CE) and Enterprise Edition (EE) 7.12.1 contain fixes
for integration with external issue trackers (e.g. Redmine), user removal and
SAML user activation. 

In GitLab Continuous Integration (CI) we fixed several bugs related to the new
`.gitlab-ci.yml` job specification format.

In the Omnibus packages we fixed the remote_syslog feature (EE only), added
support for special SAML settings in gitlab.yml, and we fixed a bug in the
automatic GitLab / GitLab CI integration.

<a name="omnibus-fix-web-tags"/></a>_Update 2015-07-02_: we have just pushed
new Omnibus packages (7.12.1.omnibus.1) which fix a regression preventing users
from creating annotated Git tags in the web interface.

For more details on the changes please see the
[CE](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG),
[EE](https://gitlab.com/gitlab-org/gitlab-ee/blob/master/CHANGELOG),
[CI](https://gitlab.com/gitlab-org/gitlab-ci/blob/master/CHANGELOG), and
[Omnibus](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/CHANGELOG.md)
CHANGELOGs.

Please see our [Update page](/update/) for update instructions. Coming from
7.12.0 updating to 7.12.1 does not require downtime.

Edit: added comment about downtime.
