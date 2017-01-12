---
title: "We’re bringing GitLab Pages to the Community Edition"
author: Job van der Voort
author_twitter: Jobvo
categories: GitLab
image_title: '/images/pages_gift.jpg'
description: "We're bringing GitLab Pages from GitLab Enterprise Edition to the open source Community Edition. GitLab Pages allows you to host static sites straight from GitLab, using any static site generator."
---

The wider community asked us open source GitLab pages.
Inspired by the holiday-spirit we're happy to bring GitLab Pages to the Community Edition (CE) of GitLab.

<!-- more -->

[GitLab Pages][gl-pages] allows you to [host static websites][host] straight from GitLab, with any kind of [static site generator][static].
For instance, [my personal website](http://www.jobvandervoort.com) is hosted
through GitLab Pages on GitLab.com using my favorite static site generator
[Middleman][middleman] ([see the source here][jobs-site]). Even our [documentation site][doc-site] is
also fully built on GitLab Pages. Until today, GitLab Pages was exclusive to
the [Enterprise Edition][ee] of GitLab.

[gl-pages]: http://pages.gitlab.io/
[host]: https://about.gitlab.com/2016/04/07/gitlab-pages-setup/
[static]: https://about.gitlab.com/2016/06/17/ssg-overview-gitlab-pages-part-3-examples-ci/
[middleman]: https://middlemanapp.com/
[jobs-site]: https://gitlab.com/JobV/jobv.gitlab.io
[doc-site]: https://about.gitlab.com/2016/12/07/building-a-new-gitlab-docs-site-with-nanoc-gitlab-ci-and-gitlab-pages/
[ee]: https://about.gitlab.com/products/

When we chose to limit this functionality to EE, we did so based on the
reasoning that small teams wouldn’t be interested in this
functionality. We thought it met our [stewardship][stewardship] criteria that it was more relevant for organizations that have more than 100 potential users.

We thought that small teams would use the option of using GitLab.com (which runs EE) for free.
Or that they would set up only one website which is easy to do manually.

[stewardship]: https://about.gitlab.com/about/#stewardship

Yet, [more than a hundred people voted][many-people] and discussed bringing
GitLab Pages to our open-source MIT-licensed Community Edition (CE). We’re
always willing to reconsider our decisions and the passionate messages we
received were more than enough reason to do so. Of course, for GitLab Inc. this
is also a business decision. When we decide to bring a feature from EE to CE,
this lowers the relative value of EE and therefore the potential of selling
subscriptions. Subscriptions allows us to keep investing in new features, packaging, bugfixing and performance improvements.

[many-people]: https://gitlab.com/gitlab-org/gitlab-ce/issues/14605

**In this case, I’m happy to announce that we will be bringing GitLab Pages to the Community Edition.** We’ll do this at the earliest convenience, most likely
with GitLab 8.16 on January 22nd.

We’re very fortunate that the wider community keeps us
sharp. It’s our hope that in the new year, you will continue to support,
guide, criticize, and contribute to GitLab.

_Want to give Pages a try? [Read our documentation here](https://docs.gitlab.com/ee/pages/README.html)._

Happy holidays!
