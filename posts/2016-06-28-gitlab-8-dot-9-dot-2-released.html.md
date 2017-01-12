---
title: "GitLab 8.9.2, 8.8.6, and 8.7.8 released"
author: Robert Speicher
author_twitter: rspeicher
---

Today we are releasing versions 8.9.2, 8.8.6, and 8.7.8 for GitLab Community
Edition (CE) and Enterprise Edition (EE).

These versions contain security fixes, and we recommend that all GitLab
installations be upgraded to one of these versions.

Please read on for more details.

<!-- more -->

## Information disclosure via Snippet search

It was possible for guests to find snippets set to "Internal" via search. See
[the issue][18997] for more details. This vulnerability affected both the
default search backend and the Elasticsearch backend in GitLab EE, and both have
been fixed.

[18997]: https://gitlab.com/gitlab-org/gitlab-ce/issues/18997

Thanks to Teun Beijers for responsibly disclosing this issue to us.

## Information disclosure via "Request Access to Group" feature

It was possible for a user to see a list of private projects in a group simply
by requesting access to it. See [the issue][19102] for more details. This
feature was only introduced in GitLab 8.9, so versions 8.8 and 8.7 were not
affected by this vulnerability.

[19102]: https://gitlab.com/gitlab-org/gitlab-ce/issues/19102

Thanks to [Colin Dean] for responsibly disclosing this issue to us.

[Colin Dean]: https://hackerone.com/colindean

## Security fix in `ruby-saml` dependency

We've upgraded our version of [`ruby-saml`] to address [CVE-2016-5697]. See [the
merge request][4951] for more details.

[`ruby-saml`]: https://rubygems.org/gems/ruby-saml
[CVE-2016-5697]: https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-5697
[4951]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/4951

## Upgrade barometer

These versions do not include any migrations, and should not require any
downtime.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

## Updating

To update, check out our [update page](https://about.gitlab.com/update).

## Sign up for security notices

Want to be alerted to new security patches as soon as they're available? Sign up
for our [Security Newsletter](https://about.gitlab.com/contact/).

## Enterprise Edition

Interested in GitLab Enterprise Edition? Check out the [features exclusive to
EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](https://about.gitlab.com/subscription).
No time to upgrade GitLab yourself? Subscribers receive upgrade and installation
services.
