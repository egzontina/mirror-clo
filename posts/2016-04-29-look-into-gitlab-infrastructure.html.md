---
title: "An inside look at the infrastructure of GitLab.com"
date: 2016-04-29
author: Tomasz Maczukin
author_twitter: TomaszMaczukin
categories:
image_title: '/images/unsplash/goal.jpg'
---

A number of people have asked about the infrastructure of GitLab.com. Our passionate
and curious Twitter followers inquired specifically about how many servers we use for
GitLab.com. Given the number of questions we've gotten on this topic, we wanted to go
ahead and offer an inside look at our GitLab.com infrastructure. In this post,
you'll find out just how many servers we use. You'll gain some perspective on what
those servers are up to.

<!-- more -->

## Baseline

For running GitLab.com as an application we have:

- 5 HAProxy load balancers that are handling GitLab.com HTTP, HTTPS, and SSH
- 2 HAProxy load balancers that are handling "[alternative SSH][altssh]" (altssh.GitLab.com) so they do redirection from 443 to 22
- 2 HAProxy load balancers that are handling <https://pages.gitlab.io> HTTP and HTTPS
- 20 workers running GitLab EE application stack (Nginx, Workhorse, Unicorn + Rails, Redis + Sidekiq)
- 2 NFS servers for the storage
- 2 Redis servers
- 2 PostgreSQL servers
- 3 Elasticsearch servers

Those are servers that we manage directly. With that, the server count is at 38.

## Next

We also use 6 of Azure's "Availability Sets": 3 for load balancers, 1 for Redis HA, 1 for
PostgreSQL HA, and 1 for Elasticsearch HA. Each of these Availability Sets has its own "internal"
load balancer that is managing the HA traffic. If we count them as a GitLab.com servers, then
we need to add 6 servers (now, the count is 44).

We also have 3 servers for GitLab Runners in [autoscale mode][scale]. Two of them are managing autoscaling
of runners for GitLab CE/EE projects (so they are used only by GitLab and I will not count them).
But the third is used to manage [autoscaling for Shared Runners][shared] at GitLab.com. So +1 for
the "Shared Runners manager."

We also have some servers that are specific for GitLab as a company (Runners for building
Omnibus packages, etc.) but I wouldn't count that as a part of GitLab.com.

And at the end, we have 45 servers that are used to make GitLab.com a usable application for our
users.

## But wait, there's more

Ah! Don't forget about autoscaled Docker machines! Each user's builds are running on Docker hosts
created "on demand" by the autoscaling mode of the Runner. Last week, I looked at a diagram of the
machine utilization and it showed that we had:

- minimum 12 machines running at once,
- maximum 150 machines running at once,
- an average of 54 machines running at once.

Because Shared Runners can be used by all GitLab.com users then I would count them as well!

## Final count

So, the answer is, GitLab.com is currently running on 45 servers. However, if we also
count the build hosts for Shared Runners, then GitLab.com is using 60 to 200 servers!

We appreciate the question and the curiosity. As always, keep the questions coming!
You can also visit [our Operations issue tracker](https://gitlab.com/gitlab-com/operations/issues) for a live look at what
the team is working on.

[altssh]: /2016/02/18/gitlab-dot-com-now-supports-an-alternate-git-plus-ssh-port/
[shared]: /2016/04/05/shared-runners/
[scale]: /2016/03/29/gitlab-runner-1-1-released/
