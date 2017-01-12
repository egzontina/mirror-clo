---
title: Working on getting the first people online
tags: []
status: publish
type: post
published: true
meta:
  _wpas_done_twitter: '1'
  _elasticsearch_indexed_on: '2012-09-11 07:09:52'
---
For the past couple of days I've been working on the production environment for Gitlab.com. I say 'I' instead of 'we' because [Marin](http://blog.gitlab.com/2012/09/04/welcome-marin/) is on a well deserved holiday in Norway. I'm using [Amazon Web Services](http://aws.amazon.com/) (AWS) and [Chef](http://www.opscode.com/chef/) which I both like a lot.  I've taken an existing Chef recipe as a starting point but that was quite a bit different from the [current installation manual](https://github.com/gitlabhq/gitlabhq/blob/master/doc/installation.md). So I'm now making [a new recipe](https://github.com/dosire/cookbook-gitlab/). It has taken a bit more time as I expected. I've had no problem setting up  [a database service](http://aws.amazon.com/rds/) and [an email service](http://aws.amazon.com/ses/) using the AWS services. But storing the repositories and attachments on an separate [EBS volume](http://aws.amazon.com/ebs/) has brought out some things that are a bit brittle in the configuration of Gitlab. I look forward to getting the first 10 people online this week. When Marin is back we'll also polish our public chef recipe so other people can leverage it.