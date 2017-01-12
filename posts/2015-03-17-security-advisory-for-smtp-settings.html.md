---
title: Security advisory for smtp settings
date: 2015-03-17
author: Marin Jankovski
---

In GitLab 7.8.x, smtp settings example file contained the line `openssl_verify_mode: 'none'`. This meant that mail server TLS certificate wasn't verified by GitLab.

Confusion came from assumption that `none` is the default value when TLS is enabled and that it behaved the same as when the setting is omited. In contact with Rails team member we've learned omiting `openssl_verify_mode` defaults to `peer`.

If you have installation from source, smtp enabled, TLS enabled and the above setting we advise you to change the setting to `openssl_verify_mode: 'peer'`.

Installations using omnibus packages are not affected.
