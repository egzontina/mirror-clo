---
title: GitLab.com and Logjam
date: 2015-06-17
author: Marin Jankovski
author_twitter: maxlazio
---

We've previously announced [security advisory for Logjam vulnerability](https://about.gitlab.com/2015/05/21/security-advisory-for-logjam-vulnerability/). In that announcement we've mentioned that GitLab.com is using 1024-bit DH groups to retain compatibility with older Java-based clients.

We've updated the default/recommended SSL ciphers for all GitLab installations and implemented new ciphers on GitLab.com.

<!--more-->

After some reasearch and testing we've decided to change the SSL cipher suite served by the web server/load balancer.

This decision was made after weighing on the trade-offs between having the stronger DH params and denying access to Java 6 based clients.


#### Using 2048-bit DHE params

Generating the 2048-bit DHE params was advised to help against the Logjam vulnerability. While this is a way to go for most servers, with GitLab.com we have to keep in mind that we have users using older Java-based clients.
Adopting the stronger params suites would prevent those users using GitLab.com completely.
Although the number of these users is not high, denying them access does not seem like an option.

#### Removing DHE suites

DHE suites have a couple of issues:

* [DHE is slow](https://community.qualys.com/blogs/securitylabs/2013/06/25/ssl-labs-deploying-forward-secrecy)
* Not all browsers support all the necessary suites

One advantage of having DHE together with ECDHE suites is that this allows forward secrecy to all clients.

We then turned to investigating how others are handling this issue and we found out that, for example, Google sites mostly [do not have DHE suites in their configuration](https://www.ssllabs.com/ssltest/analyze.html?d=www.google.com).

With this in mind we've tried removing the DHE suites and the result was as follows:

* All major browsers and clients retain forward secrecy using ECDHE
* SSL labs score went from B to A
* There is no forward secrecy for Android 2.3.7, Java 6 and OpenSSL 0.9.8

After considering the trade-offs, we've decided to remove the DHE suites from our cipher suite on GitLab.com.

Forward secrecy is now denied for Android 2.3.7, Java 6 and OpenSSL 0.9.8 but we suspect that number of users affected will be extremely low.

We have also updated the recommended configurations for omnibus-gitlab packages and GitLab installation from source.

