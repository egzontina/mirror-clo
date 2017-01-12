---
title: Gitlab improvements
tags: []
status: publish
type: post
published: true
meta:
  publicize_reach: a:2:{s:7:"twitter";a:1:{i:1532919;i:33;}s:2:"wp";a:1:{i:0;i:1;}}
  _wpas_done_1532919: '1'
  _elasticsearch_indexed_on: '2012-10-04 12:44:07'
---
We've been hard at work to improve Gitlab, here are some of the items we've worked on:

- Our method for properly validating ssh keys was recently [merged into Gitlab](https://github.com/gitlabhq/gitlabhq/pull/1617)
- The fingerprint of our git server will stay the same, the server host key should be: ECDSA f1:d0:fb:46:73:7a:70:92:5a:ab:5d:ef:43:e2:1c:35
- Gitlab.com was upgraded to the [latest Gitlab version](http://blog.gitlabhq.com/gitlab-2-dot-9-released/)
- [Helped](https://github.com/gitlabhq/gitlabhq/pull/1616) track down a bug in ssh key deletion
- [Fixed](https://github.com/gitlabhq/gitlabhq/pull/1561) a mass assignment vulnerability
