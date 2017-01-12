---
title: "GitLab.com now supports an alternate git+ssh port"
date: 2016-02-18
author: Achilleas Pipinellis
author_twitter: _axil
image_title: '/images/unsplash/altssh.jpg'
---

Have you ever tried to push changes to GitLab and gotten the error
“port 22: Connection refused"? The network you're connected to doesn't allow
using port 22 and you suddenly can't get your work done. I want to push and I
want to push now!

You'd be happy to know that GitLab.com now runs an alternate `git+ssh` port
(443) which you can use whenever you are in a place where port 22 is blocked.

<!-- more -->

## The problem

It's not uncommon that in some places the network traffic is being monitored
and heavily firewalled, allowing only ports 80 (HTTP) and 443 (HTTPS) to be
used.

Blocking the standard SSH port is a measure that network sysadmins
occasionally [have to take](http://serverfault.com/a/25566).

## The solution

Luckily for the users, there is more than one option to overcome this issue.
One can use a VPN, Tor or [sshuttle] to alter their network route traffic to
be able to use SSH.

But even then, [VPNs can be blocked][vpn-wiki] and these counter measures
require some knowledge to be set up and used.

The common solution is to make the SSH daemon listen to a port that is highly
likely not to be firewalled, that's why many people prefer the port 443. If you
are in a position where even port 443 is blocked, you have more serious matters
to be concerned about.

There are three potential ways to get around this problem in GitLab. The first
is to run the SSH server on a different port than the default 22 and
[configure GitLab] to use that (no user interaction). The second is to run the
SSH server on a different port and make no changes to GitLab, just instruct the
users to use that port in their `.ssh/config`.

There is a third option which involves port forwarding and avoids changing the
SSH port in the instance GitLab runs. This gives you the option to have two
distinct usable SSH ports and is the case with GitLab.com.

## How GitLab.com implements an alternate SSH port

Our current infrastructure setup goes something like this:

> **GitLab.com > Azure availability set > Loadbalancer (443->443, 80->80, 22->22) > HAProxy nodes -> workers**

Normally you can't just simply use port 443 on the same GitLab instance because
it runs GitLab itself, and that's assuming you are running GitLab with HTTPS
(if not you are highly encouraged to do so). In that case, you should better
use a separate host which forwards port 443 to port 22 of your GitLab instance.
You can do this with HAProxy or any other loadbalancer, or even with IPTables.

In GitLab.com's case, we have setup a separate Azure availability set with two
HAProxy nodes exactly the same configured as for GitLab.com. The only thing
that differs is the creation of a different Azure loadbalancer in that
availability set which forwards TCP connections from port 443 to port 22.

So the new extra setup goes something like this:

> **altssh.gitlab.com > Azure availability set > Loadbalancer (443->22) > HAProxy nodes (lb10,lb11) > workers**

## How to use the alternate SSH connection on GitLab.com

GitLab.com runs a second SSH server that listens on the commonly used port `443`,
which is unlikely to be firewalled.

All you have to do is edit your `~/.ssh/config` and change the way you
connect to GitLab.com. The two notable changes are `Hostname` and `Port`:

```
Host gitlab.com
  Hostname altssh.gitlab.com
  User git
  Port 443
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/gitlab
```

The first time you push to `altssh.gitlab.com` you will be asked to verify
the server's key fingerprint:

```
The authenticity of host '[altssh.gitlab.com]:443 ([104.208.154.249]:443)' can't be established.
ECDSA key fingerprint is SHA256:HbW3g8zUjNSksFbqTiUWPWg2Bq1x8xdGUrliXFzSnUw.
Are you sure you want to continue connecting (yes/no)?
```

That's only normal since you are connecting to the new loadbalancer. If you
watch closely, the key fingerprint is
[the same as in GitLab.com](/gitlab-com#availability-and-security).

---

Happy pushing!

[configure gitlab]: https://gitlab.com/gitlab-org/gitlab-ce/blob/28d42a33f3385b57660906d4ca35e96d56785d7e/config/gitlab.yml.example#L412-413
[sshuttle]: https://github.com/apenwarr/sshuttle "sshuttle - a poor man's VPN"
[vpn-wiki]: https://en.wikipedia.org/wiki/VPN_blocking "Wikipedia - VPN Blocking"
