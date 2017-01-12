---
title: "Responding to Ghost"
date: 2015-01-28
categories:
author: Jacob Vosmaer
---

Yesterday the [Ghost vulnerability in
glibc](http://www.openwall.com/lists/oss-security/2015/01/27/9) was announced.
A bug in a networking function in the version of the C standard library found
on many Linux systems can potentially lead to remote code execution.  There is
no indication at this time that this bug can be exploited against GitLab but it
is nevertheless recommendable to install the latest updates from your OS
vendor.  In this post we will tell you how we did this at GitLab B.V.

<!-- more -->

## 1. Update your OS packages

The first step for us was to run `apt-get upgrade` and `yum update` on all our
Linux machines.

## 2. Reboot your machine

Rebooting your server(s) is disruptive but with something as common as the C
standard library, it is difficult to pinpoint the individual services that need
to be restarted. If you reboot you are sure you caught them all; this is what
we did with our Linux servers.

If you do decide to restart only selected services instead of the whole server,
you can restart GitLab with `sudo gitlab-ctl restart` (for Omnibus packages) or
`sudo service gitlab restart` (for installations from source).

## Fast 'reboots' using HA

Rebooting one of our [gitlab.com production
servers](/2015/01/03/the-hardware-that-powers-100k-git-repos/) can easily take
5 minutes. To reduce the downtime for our users we used our [DRBD-based High
Availability setup](https://about.gitlab.com/high-availability/). First we
installed updated packages on our stand-by server, followed by a reboot. Then
we did a failover from the active server to the stand-by in under a minute.
This gives us the same end result as a server reboot, namely gitlab.com running
on a freshly booted server, without having to wait for the reboot cycle of an
individual server.
