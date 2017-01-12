---
title: "Omnibus-gitlab security release: bundled Postgres trusts all local connections"
date: June 19, 2014
author: Jacob Vosmaer
---

Due to a configuration error, the PostgreSQL server that is bundled into omnibus-gitlab trusts all connections originating from the server omnibus-gitlab is running on.
This has been rectified in omnibus-gitlab `6.9.2.omnibus.2` (GitLab Community Edition) and `6.9.4-ee.omnibus.1` (GitLab Enterprise Edition).
We advise all users of omnibus-gitlab to update to the latest release.

__Affected versions:__ all versions of omnibus-gitlab up to and including omnibus-gitlab `6.9.2.omnibus.1` (GitLab Community Edition) and `6.9.4-ee.omnibus` (GitLab Enterprise Edition).

__Not affected:__ Source and cookbook installations of GitLab (e.g. not using .deb or .rpm packages). Omnibus-gitlab installations which use an external DBMS are also not affected.

__Fixed versions:__ omnibus-gitlab `6.9.2.omnibus.2` (GitLab Community Edition) and `6.9.4-ee.omnibus.1` (GitLab Enterprise Edition).

# Releases
You can download the latest version of [omnibus-gitlab for GitLab Community Edition](/downloads/) or [omnibus-gitlab for GitLab Enterprise Edition](https://gitlab.com/subscribers/gitlab-ee/blob/master/doc/install/packages.md) and follow the [update instructions](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/update.md).

# Impact
An attacker who can execute code on the server omnibus-gitlab runs on can get full superuser access to the bundled Postgres database which holds all GitLab metadata.

To see if your omnibus-gitlab installation is affected you can run the following command on your GitLab server.

```
sudo -u root /opt/gitlab/embedded/bin/psql -U gitlab-psql -d template1 -c '\echo connected to an insecure Postgres instance'
```

If the command echoes `connected to an insecure Postgres instance` your omnibus-gitlab installation is affected by this issue.
If you receive an error message `psql: FATAL:  Peer authentication failed for user "gitlab-psql"`, your bundled Postgres service is secured.

Please contact us at support@gitlab.com if you have any questions.
