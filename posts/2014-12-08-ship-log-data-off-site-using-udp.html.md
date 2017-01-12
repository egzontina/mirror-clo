---
title: "How you can send your logs ballistically using UDP"
date: 2014-12-08
categories:
author: Job van der Voort
---

The last thing you want to happen is having problems on your server due to your logs.
You need them to debug problems, not cause them. With large GitLab instances, it's
a great idea to ship your logs to a separate server. This way, they are easier to manage
and you don't need to worry about space. But by using TCP to send the logs you risk
a connection failure and subsequent problems with your instance.

Therefore, with GitLab Enterprise Edition (7.1 and up) Omnibus packages,
we introduced UDP log shipping.
As opposed to TCP, UDP doesn't care about whether packets get received,
it keeps sending them in a non-blocking, fire-and-forget manner.
That makes UDP really fast, lightweight and if you log server crashes, it won't
affect your GitLab instance. UDP doesn't care.

<!-- more -->

## Setting up UDP log shipping

UDP log shipping is very easy to setup. You simply add the following lines to `/etc/gitlab/gitlab.rb`:

```
logging['udp_log_shipping_host'] = '1.2.3.4' # Your syslog server
logging['udp_log_shipping_port'] = 1514 # Optional, defaults to 514 (syslog)
```

And run `sudo gitlab-ctl reconfigure`. Now your logs will be shipped speedily to `1.2.3.4:1514`!

An example of what your syslog server will receive:

```
<13>Jun 26 06:33:46 ubuntu1204-test production.log: Started GET "/root/my-project/import" for 127.0.0.1 at 2014-06-26 06:33:46 -0700
<13>Jun 26 06:33:46 ubuntu1204-test production.log: Processing by ProjectsController#import as HTML
<13>Jun 26 06:33:46 ubuntu1204-test production.log: Parameters: {"id"=>"root/my-project"}
<13>Jun 26 06:33:46 ubuntu1204-test production.log: Completed 200 OK in 122ms (Views: 71.9ms | ActiveRecord: 12.2ms)
```

## How it works

The services of GitLab write log messages to logfiles (such as `production.log`)
or to STDOUT. GitLab Omnibus packages use [svlogd](http://smarden.org/runit/svlogd.8.html)
to log STDOUT to for instance `sidekiq/current`.

svlogd is great, as it allows us to ship these logs using UDP and even rotate them.
However, it can't work with `.log` files. So in addition to svlogd, we make
use of [remote_syslog](https://github.com/papertrail/remote_syslog), which can work
with `.log` files and allows us to ship the using UDP.

By using a single configuration option in the Omnibus package, as shown above,
we were able to make UDP log shipping simple to setup and flexible enough to work
with both `.log` files and STDOUT logging.


## About GitLab

Want to start to use UDP log shipping? Check out [GitLab Enterprise Edition](https://about.gitlab.com/features/#enterprise).
A subscription also includes support, deep LDAP integration, git hooks, Jenkins integration and many more powerful enterprise features.

You can try GitLab by [downloading](https://about.gitlab.com/downloads/) the Community Edition and installing it on your own server or by signing up to our free, unlimited GitLab instance [GitLab.com](https://gitlab.com/users/sign_up).

See our previous feature highlights:

- [Groups](https://about.gitlab.com/2014/06/30/feature-highlight-groups/)
- [Git Hooks](https://about.gitlab.com/2014/08/25/feature-highlight-git-hooks/)
- [Branded Login](https://about.gitlab.com/2014/09/02/feature-highlight-branded-login-gitlab-ee/)
- [LDAP Integration](https://about.gitlab.com/2014/07/10/feature-highlight-ldap-sync/)
