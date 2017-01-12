---
title: "A Brief History of GitLab Workhorse"
date: 2016-04-12 12:00
comments: true
author: Jacob Vosmaer
author_twitter: jacobvosmaer
image_title: /images/brief-history-of-gitlab-workhorse/gopher.jpg
---

In the past 8 months gitlab-workhorse, a 'weekend project' written in Go
instead of our preferred Ruby, grew from a tiny program that addressed
`git clone` timeouts into a critical component that touches almost all
HTTP requests to GitLab. In this blog post I will reflect on how we got
here.

<!-- more -->

## Technical and personal motivations

GitLab is a Ruby on Rails web application that uses the
[Unicorn](http://unicorn.bogomips.org/) Ruby web server. I am a fan of
Unicorn because it makes application resource leaks manageable and
because it has served GitLab well for a long time by patching up
problems which we found or find too hard to solve 'properly'. (I am
known to growl at people who suggest swapping out Unicorn for another
web server in GitLab.)

At the same time, the design of Unicorn is incompatible with one of
GitLab's main functions, namely Git repository access (`git clone`,
`git push`, etc.) via HTTP(S). The reason it is incompatible is that
Unicorn heavily relies on (relatively) short request timeouts. If you
configure Unicorn to time out slowly rather than quickly then it starts
to become a lot less pleasant to work with. A `git clone` on the other
hand may take quite a long time if you are fetching a large Git
repository. In my previous role as a service engineer at GitLab I
regularly had to explain this tension to customers. The only solution we
could offer was 'use Git over SSH instead'.

Another factor that led to gitlab-workhorse was my unfulfilled curiosity
about the [Go programming language](https://golang.org/). Go is
sometimes credited with (or discredited for) having a strong marketing
push behind it. The marketing worked on me: I have had a plush Go mascot
staring at me on my desk for almost three years now.

![Gopher](/images/brief-history-of-gitlab-workhorse/gopher.jpg)

## A weekend project gets merged into master

So one weekend in July last year I found myself with an itch to build
something in Go and a lack of imagination which led me to ask myself:
could I rewrite
[gitlab-grack](https://gitlab.com/gitlab-org/gitlab-grack), the GitLab
component that responds to Git HTTP clients, in Go? For the record I am
not proud of having used my own (non-work) time to drive development of
this project for the first few months, I think it sets a bad example for
myself and others. But that is how it went.

The result was a very short and mostly correct Go program called
'gitlab-git-http-server' that suffered from none of the timeout issues
that `git clone` via Unicorn had. It integrated with GitLab in a sneaky
way by letting NGINX divert Git HTTP requests away from Unicorn to
gitlab-git-http-server. The required changes in the GitLab Rails
codebase were so minor that I could easily hide them behind a [feature
flag](https://en.wikipedia.org/wiki/Feature_toggle). To top it off I
announced gitlab-git-http-server to the team on a day the CTO was on
vacation: the ultimate sneak attack. Just kidding, but I thought it was
a funny coincidence about [Dmitriy](https://gitlab.com/u/dzaporozhets)'s
vacation.

The team somehow let me 'try gitlab-git-http-server out' (read: merge it
into master and deploy it on our staging server) and so it got started.
Less than a month later GitLab 7.14 shipped with gitlab-git-http-server
behind a feature flag. This allowed us to test it on GitLab.com for a
month. Between our staging environment and GitLab.com we were able to
catch the worst bugs. In GitLab 8.0 (released the month after 7.14)
we made gitlab-git-http-server an official (and required!) component of
GitLab.

The acceptance of gitlab-git-http-server by the team was probably helped
by a shared understanding that GitLab's Git-over-HTTP solution was just
not quite cutting it, and by the fact that we already used Go for
[gitlab-ci-multi-runner](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner).
But there was no up-front decision to solve the problem of Git-over-HTTP
at this particular time, or using these means.

## Feature creep

Until now gitlab-git-http-server was a one-trick pony: it only handled
Git HTTP clients. But as usually happens when you have a new hammer,
other things started looking like nails. In GitLab 8.1 we changed
gitlab-git-http-server to also handle the 'download zip' button from the
GitLab web interface. In retrospect this seems obvious but at the time
it felt like a big leap: in our minds, gitlab-git-http-server was a
daemon that understood (stateless) [HTTP Basic
Authentication](https://en.wikipedia.org/wiki/Basic_access_authentication)
but not the session cookies used by GitLab to identify individual users.
But a session cookie is just an HTTP header so nothing stopped
gitlab-git-http-server from 'impersonating' a logged-in user and
generating a zip file for them on the fly. I have a bit of a hard time
explaining now why but we thought this was very neat at the time.

## Time for a new name

In GitLab 8.2 we wanted to ship two new features for which we expected
the same sort of Unicorn timeout problems that had plagued Git-over-HTTP
in the past: [Git LFS](https://git-lfs.github.com/) support (developed
by [Marin](https://gitlab.com/u/marin)) and [CI build
artifacts](http://doc.gitlab.com/ce/ci/build_artifacts/README.html)
(developed by [Kamil](https://gitlab.com/u/ayufan)). Both of these
features depended on users uploading and downloading arbitrarily large
files.

This development brought many improvements to gitlab-git-http-server.
First of all, the more people had to say or write
'gitlab-git-http-server', the more obvious it became that the name was
too awkward. And with all these new features it was also no longer
appropriate, because the program did more than dealing with
Git-over-HTTP. We have Marin to thank for coming up with
'gitlab-workhorse' which I especially like because it pokes fun at
Unicorn.

It was also a great development for gitlab-workhorse to be getting
attention from Kamil because he is our resident Go expert. This was very
welcome: I felt confident enough that gitlab-workhorse functioned
correctly, but I am not an experienced Go programmer. Having Kamil in
the game helped us make gitlab-workhorse a better Go program.

For a short while, Marin and I were on the one hand trying to implement
file uploads/downloads in gitlab-workhorse, while Kamil on the other
hand was implementing the same thing for CI artifacts using NGINX
plugins. Luckily we spotted the duplication of efforts before the code
went out the door so we were able to implement this in gitlab-workhorse
together for GitLab 8.2.

We ended up with an especially nice solution for file downloads in
gitlab-workhorse, inspired by the mechanism Kamil intended to use in
NGINX: `X-Sendfile` headers. Most of the time when you want to use
gitlab-workhorse to make something faster or more robust in GitLab you
have to write both Ruby code and Go code. But because [Ruby on Rails
understands `X-Sendfile`
already](http://api.rubyonrails.org/classes/ActionController/DataStreaming.html#method-i-send_file),
GitLab developers can reap the benefits of gitlab-workhorse for file
downloads without writing any Go code!

## Betting the farm

By this time the success with which we could build new GitLab features
by doing part of the work in gitlab-workhorse started to cause problems
of its own. Each time we added a feature to gitlab-workhorse that meant
diverting more HTTP requests to gitlab-workhorse in the NGINX
configuration. This complexity was hidden from people who installed
GitLab using our [Omnibus packages](https://packages.gitlab.com/gitlab)
but I could tell from the gitlab-workhorse issue tracker that this was a
recurring source of problems for installations from source.

Prior to gitlab-workhorse, NGINX served static files or forwarded
requests to Unicorn:

    +----------+      +-------------+
    |          |      |             |
    |  NGINX   +----> |   Unicorn   |
    |          |      |             |
    +------+---+      +-------------+
           |
           |
           |          +------------+
           |          |            |
           +--------> |   static   |
                      |   files    |
                      |            |
                      +------------+


Now with gitlab-workhorse in the picture, NGINX had to know which
requests to send to Unicorn, which to gitlab-workhorse, and which to
static files.

                    +--------------------+
                    |                    |
           +------> |  gitlab-workhorse  |
           |        |                    |
           |        +---------+----------+
           |                  |
           |                  v
           |
    +------+---+      +-------------+
    |          |      |             |
    |  NGINX   +----> |   Unicorn   |
    |          |      |             |
    +------+---+      +-------------+
           |
           |
           |          +------------+
           |          |            |
           +--------> |   static   |
                      |   files    |
                      |            |
                      +------------+


Kamil half-jokingly suggested at one point that we could route all HTTP
traffic to GitLab through gitlab-workhorse. Over time I started to
believe this was a good idea: it would radically simplify the NGINX
configuration for GitLab, and consequently make it easier to deploy
GitLab behind other web servers (like Apache) which some people prefer
strongly to using NGINX. It seems the idea grew on Kamil too because we
soon saw a huge merge request from him to gitlab-workhorse which turned
it into a 'smart proxy' that serves static files, injects error pages,
implements Git-over-HTTP plus other features, *and* proxies traffic to
GitLab.

    +-------------+         +---------------------+        +------------+
    |             |         |                     |        |            |
    |   NGINX     +-------> |  gitlab-workhorse   +------> |  Unicorn   |
    |             |         |                     |        |            |
    +-------------+         +---------------------+        +------------+

This change went out in GitLab 8.3. In little over four months
gitlab-workhorse went from being a little helper daemon on the side to a
traffic cop that routes all HTTP requests going into GitLab.

This work immediately paid off in GitLab 8.4 when
[Grzegorz](https://gitlab.com/u/grzesiek) added the CI artifact browsing
feature and GitLab 8.5 where we started serving 'raw' Git blobs via
gitlab-workhorse. Neither of these changes forced GitLab administrators
to update their NGINX configuration.

## What to do next

The most important next step for gitlab-workhorse is to make it less
dependent on me by getting more of my team members to contribute to the
code. I am trying to do this by purposely leaving some [nice
changes](https://gitlab.com/gitlab-org/gitlab-ce/issues/13999) for
others to implement.

Because of the gradual (and sneaky :) ) way gitlab-workhorse was added
to GitLab we still have some technical debt in GitLab in the [Git HTTP
authentication / authorization
code](https://gitlab.com/gitlab-org/gitlab-ce/issues/14501). It would be
nice to clean this up.

Finally, it is sub-optimal that we still buffer Git pushes in NGINX
before forwarding them to gitlab-workhorse. We could avoid this
unncessary delay and give people who use Apache instead of NGINX a
better experience if we [implement selective request buffering in
gitlab-workhorse](https://gitlab.com/gitlab-org/gitlab-workhorse/issues/1#note_2681403).

If you want to know what is coming next in GitLab, check out our
[Direction](https://about.gitlab.com/direction/) page, or follow developments on
our latest milestones for 8.7 [CE](https://gitlab.com/gitlab-org/gitlab-ce/milestones/23)
and [EE](https://gitlab.com/gitlab-org/gitlab-ee/milestones/9).
