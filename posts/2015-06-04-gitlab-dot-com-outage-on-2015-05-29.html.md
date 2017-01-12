---
title: "GitLab.com outage on 2015-05-29"
date: 2015-06-04
author: Jacob Vosmaer
author_twitter: jacobvosmaer
---

GitLab.com suffered an outage from  2015-05-29 01:00 to 2015-05-29 02:34 (times in UTC).
In this blog post we will discuss what happened, why it took so long to recover the service, and what we are doing to reduce the likelihood and impact of such incidents.

<!-- more -->

# Background

GitLab.com is provided and maintained by the team of GitLab B.V., the company behind GitLab.
On 2015-05-02 we performed a major infrastructure upgrade, moving GitLab.com from a single server to a small cluster of servers, consisting of a load balancer (running HAproxy), three workers (NGINX/Unicorn/Sidekiq/gitlab-shell) and a backend server (PostgreSQL/Redis/NFS).
This new infrastructure configuration improved the responsiveness of GitLab.com, at the expense of having more moving parts.

GitLab.com is backed up using Amazon EBS snapshots.
To protect against inconsistent snapshots our backup script 'freezes' the filesystem on the backend server with `fsfreeze` prior to making EBS snapshots, and 'unfreezes' the filesystem immediately after.

# Timeline

Italic comments below are written with the knowledge of hindsight

- 1:00 The GitLab.com backup script is activated by Cron on the backend server.
  _For unknown reasons, the backup script hangs/crashes before or during the 'unfreeze' of the filesystem holding all user data._
- 1:07 Our on-call engineer is paged by [Pingdom](http://status.gitlab.com).
  The on-call engineer tries to diagnose the issue on the worker servers but is unable to diagnose the problem.
  _The issue was on the backend server, not on the workers._
- 1:30 The on-call engineer decides to call in more help.
  The other team members with access and knowledge to resolve the issue are all in Europe at this time, where it is 3:30/4:30am.
- 1:45 A second engineer in Europe has been woken up and takes the lead on the investigation of the outage.
  More workers are rebooted because they appear to be stuck.
  It becomes apparent that the workers cannot mount the NFS share which holds all Git repository data.
- 1:51 One of the engineers notices that the load on the backend server is more than 150. _A normal value would be less than 5._
- 2:10 The engineers give up on running commands on the workers to bring the NFS share back, and start investigating the backend server.
  The engineers discuss whether they should reboot the backend server but they are unsure if it is safe given that this setup is fairly new.
- 2:21 The engineers reboot the backend server.
  The reboot is taking a long time.
  _The AWS 'reboot' command first tries a soft reboot, and only does a hard reboot after a 4-minute timeout.
  The soft reboot probably hung when it tried to shut down services that were trying to write to the 'frozen' disk._
- 2:30 The backend server has rebooted and the engineers regain SSH access to it.
  The worker servers are able to mount the NFS share now but GitLab.com is still not functioning because the Postgres database server is not responding.
  One of the engineers restarts Postgres on the backend server.
  _It may have been that Postgres was still busy performing crash recovery._
- 2:34 Gitlab.com is available again.

# Root causes

Although we cannot explain _what_ went wrong with the backup script it is hard to come to another conclusion that _something_ did go wrong with it.

The length of the outage was caused by insufficient training and documentation for our on-call engineers following the infrastructure upgrade rolled out on May 2nd.

# Next steps

We have removed the freeze/unfreeze steps from our backup script.
Because this (theoretically) increases the risk of occasional corrupt backups we have added a second backup strategy for our SQL data.
In the future we would like to have automatical validation of our GitLab.com backups.

The day before this incident we decided the training was our most important priority.
We have started to do regular operations drills in one-on-one sessions with all of our on-call engineers.
