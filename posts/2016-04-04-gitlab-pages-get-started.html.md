---
title: "Get Started with GitLab Pages"
date: 2016-04-04 10:00
categories:
author: Achilleas Pipinellis
author_twitter: _axil
image_title: '/images/unsplash/ios-development.jpg'
---

With [GitLab Pages][docs-pages] you can host your static website for free.
We added GitLab Pages in GitLab Enterprise Edition (EE) 8.3, and
then added support for custom domains and TLS certificates in GitLab EE 8.5. We
made this service freely available to users on [GitLab.com](https://gitlab.com),
which is our hosted GitLab EE service, offering unlimited and free public or
private projects.

We've since added some great resources to help you get started, including this
handy [quickstart guide][quickstart].

<!-- more -->

## What you need to know about GitLab Pages

1. There are two kinds of Pages:
    - User or group Pages
    - Project Pages
2. You can use [any static site generator][staticgen]
3. You can connect custom domains and TLS certificates to secure your domains
4. The service is completely free as part of GitLab.com

## New resources to learn how to use GitLab Pages

We added improved documentation to help you get your site set up.

- GitLab Pages Quick Start Guide: https://pages.gitlab.io
- Documentation: [GitLab Pages User guide][docs-pages]
- Documentation: [GitLab Pages Admin guide][docs-adminpages]

We also [added a group][group] with a number of example GitLab Pages projects.

![GitLab Pages example projects](/images/blogimages/gitlab-pages-examples.png)

You can easily get started with a [Plain HTML](https://gitlab.com/pages/plain-html)
site, but you can do much more.
The range of examples show that GitLab can support *any static site generator*.
You name the generator, you can build it with GitLab!

- [Jekyll](https://gitlab.com/pages/jekyll)
- [Pelican](https://gitlab.com/pages/pelican)
- [Hugo](https://gitlab.com/pages/hugo)
- [Middleman](https://gitlab.com/pages/middleman)
- [Hexo](https://gitlab.com/pages/hexo)
- [Brunch](https://gitlab.com/pages/brunch)
- [Metalsmith](https://gitlab.com/pages/metalsmith)
- [Harp](https://gitlab.com/pages/harp)

All of this is made possible with [GitLab CI][ci]. If you'd like to know more,
sign up for our webcast below!

## Need some help to get started?

We'd love your feedback on our [GitLab Pages Quick Start][quickstart] guide.
If you have any questions you can submit them in the comments,
or on the [issue tracker] for the GitLab Pages Quick Start Guide project.

## Live webcast: GitLab CI

Sign up for our webcast on April 14th, which includes an overview and tutorial
about using GitLab CI. Meet people from the GitLab CI team and get your questions
answered live!

- Date: Thursday, April 14, 2016
- Time: 5pm (17:00) UTC; 12pm EST; 9am PST
- [Register here](http://page.gitlab.com/apr-2016-gitlab-intro-ci-webcast.html)

Can't make it? Register anyway, and we'll send you a link to watch it later!

[issue tracker]: https://gitlab.com/pages/pages.gitlab.io/issues
[docs-pages]: http://doc.gitlab.com/ee/pages/README.html
[docs-adminpages]: http://doc.gitlab.com/ee/pages/administration.html
[quickstart]: https://pages.gitlab.io
[group]: https://gitlab.com/groups/pages
[ci]: https://about.gitlab.com/gitlab-ci/
[staticgen]: https://www.staticgen.com/
