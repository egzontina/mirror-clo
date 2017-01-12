---
title: "GitLab 8.4.1 Released"
date: 2016-01-26
author: GitLab
author_twitter: gitlab
filename: 2016-01-26-gitlab-8-dot-4-dot-1-released.markdown
---

Today we are releasing version 8.4.1 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

This update includes several security fixes for gem dependencies, [including
Rails itself][rails], and is a recommended upgrade for all installations.

It includes the following changes:

- **CE/EE:** Apply security updates for Rails (4.2.5.1), rails-html-sanitizer (1.0.3),
  and Nokogiri (1.6.7.2) ([!2603])
- **CE/EE:** Fix redirect loop during import ([!2606])
- **CE/EE:** Fix diff highlighting for all syntax themes ([!2530], [!2563],
  [!2594])

[!2530]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2530
[!2563]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2563
[!2594]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2594
[!2602]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2602
[!2603]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2603
[!2606]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2606
[rails]: http://weblog.rubyonrails.org/2016/1/25/Rails-5-0-0-beta1-1-4-2-5-1-4-1-14-1-3-2-22-1-and-rails-html-sanitizer-1-0-3-have-been-released/

<!-- more -->

## Upgrade barometer

This version does not include any new migrations, and should not require any
downtime.

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

## Updating

To update, check out our [update page](https://about.gitlab.com/update).

## Enterprise Edition

Interested in GitLab Enterprise Edition? Check out the [features exclusive to
EE](https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/subscription/).
No time to upgrade GitLab yourself? Subscribers receive upgrade and installation
services.
