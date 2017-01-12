---
title: Install Gitlab on AWS with a single script
tags: []
status: publish
type: post
published: true
meta:
  _elasticsearch_indexed_on: '2012-09-03 09:29:17'
---
Since announcing the Gitlab.com plans we've been working on getting everything up and running. Part of this has been exploring the best way to install Gitlab. Although there is a good [installation manua](https://github.com/gitlabhq/gitlabhq/blob/master/doc/installation.md)l it was still a bit of work to set things up. To give back to the open source project we've [contributed](https://github.com/gitlabhq/gitlabhq/pull/1318) a script to install Gitlab on Amazon Web Services with a single command:

> curl https://raw.github.com/dosire/gitlabhq/non-interactive-aws-install/lib/support/aws/debian\_ubuntu\_aws.sh | sh
Read the HOWTO of [the script](https://github.com/gitlabhq/gitlabhq/blob/master/lib/support/aws/debian_ubuntu_aws.sh) to learn more. Please file [an issue](https://github.com/dosire/gitlabhq/issues?state=open) if you have problems or suggestions. We would like to thank [randx](https://github.com/randx) and [tsigo](https://github.com/tsigo) for their feedback. One of the next things to work on for us will be the [Chef cookbook for Gitlab](https://github.com/atomic-penguin/cookbook-gitlab).