---
title: Security advisory for multiple Rails vulnerabilities
date: 2016-01-26
author: Marin Jankovski and Jacob Vosmaer
author_twitter: maxlazio
---

GitLab is built using the Ruby on Rails framework.
The team behind Ruby on Rails has [recently announced 9 possible security vulnerabilities](http://weblog.rubyonrails.org/2016/1/25/Rails-5-0-0-beta1-1-4-2-5-1-4-1-14-1-3-2-22-1-and-rails-html-sanitizer-1-0-3-have-been-released/).

This means that some of these Rails vulnerabilities could potentially
be exploitable in GitLab.

We have [released GitLab 8.4.1](https://about.gitlab.com/2016/01/26/gitlab-8-dot-4-dot-1-released) to address these
vulnerabilities.

Update: we have amended this blog post with more detailed information
about the impact on GitLab.

<!-- more -->

None of yesterday's Rails vulnerabilities has been confirmed to affect any
version of GitLab. However, due to the large number of Rails vulnerabilities and
the large number of GitLab versions that could theoretically be affected
it is hard for us to say anything definitive.

**The simplest and safest thing to do is to upgrade to GitLab 8.4.1 or newer.** In
that version we are using a version of Rails 4.2 which is patched
against all of the Rails vulnerabilities announced yesterday.

It is hypothetically possible that CVE-2016-0752 affects some version of
GitLab prior to 8.4.1. If this is the case it could be bad because
CVE-2016-0752 has the potential to be used for remote code execution.
However we have been unable to find signs that any version of GitLab is
affected by this vulnerability.

There are also three [XSS
vulnerabilities](https://en.wikipedia.org/wiki/Cross-site_scripting) in
the yesterday's set. We do not seem to be affected by them but it is not
impossible. Generally speaking, the older your GitLab version, the more
likely it has some (known) XSS vulnerability.

Below we will go into some more detail of the possible impact of
yesterday's Rails vulnerabilities on GitLab.

Because a code execution vulnerability, if present, is very severe, we
advise you to upgrade to 8.4.1 to prevent possible issues.

If you are an Enterprise Edition subscriber, please contact support with any questions.

## Impact on GitLab

### CVE-2015-7576 Timing attack vulnerability in basic authentication in Action Controller

GitLab does not use the HTTP Basic Authentication implementation from
Action Controller. In addition we have had rate limiting on HTTP Basic
endpoints since GitLab 7.6.

### CVE-2016-0751, CVE-2015-7581 Denial of service

Both of these denial of service vulnerabilities involve memory
exhaustion. Because GitLab has been using
[unicorn-worker-killer](http://doc.gitlab.com/ce/operations/unicorn.html#unicorn-worker-killer)
since GitLab 6.4 it is unlikely that these vulnerabilities can be
exploited against GitLab. Note that the same may not be true if you use
GitLab with a custom Ruby web server such as Puma or Passenger.

### CVE-2015-7578, CVE-2015-7579, CVE-2015-7580 XSS vulnerabilities

It is hard to tell if GitLab is vulnerable to any of these. From the
[vulnerability
disclosures](https://about.gitlab.com/vulnerability-acknowledgements/)
we receive we do know that we have been and continue to be probed for
XSS a lot.

### CVE-2015-7577 Nested attributes rejection proc bypass in Active Record

This vulnerability needs a special `allow_destroy: false` setting which
was not shipped in any existing GitLab version. In other words
it does not affect GitLab.

### CVE-2016-0753 Possible Input Validation Circumvention in Active Model

This vulnerability only affects Rails 4 and newer, and the 'Strong
Parameters' paradigm introduced in Rails 4 counteracts it. GitLab uses
Rails 4 since version 7.1.0. None of the GitLab versions released since
7.1.0 use the ActiveRecord `permit!` method in an unsafe way. It is very
unlikely that any released version of GitLab is affected by this
vulnerability.

### CVE-2016-0752 Possible Information Leak Vulnerability in Action View

This vulnerability, when present, lets an attacker load an arbitray file
on disk to be interpreted by Rails as a template. Combined with user
uploads (which GitLab offers) this creates the potential for remote code
execution.

It is hard to search for this vulnerability in source code because
untrusted input may be assigned to a variable in one place, with the
variable being passed to `render` in another place. We have not found
occurences of unsafely passing a value *directly* from `params`
to `render` in any released version of GitLab.

It is unlikely that any released version of GitLab is affected by this
vulnerability.
