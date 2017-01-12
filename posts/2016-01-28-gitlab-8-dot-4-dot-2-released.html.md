---
title: "GitLab 8.4.2 Released"
date: 2016-01-28
author: GitLab
author_twitter: gitlab
filename: 2016-01-28-gitlab-8-dot-4-dot-2-released.markdown
---

Today we are releasing version 8.4.2 for GitLab Community Edition (CE) and
Enterprise Edition (EE).

Most importantly, we've removed those ugly borders that accidentally got added
to all of our tables. That alone should be reason to upgrade, but this version
also includes some performance improvements to project pages and to
Elasticsearch indexing, and squashes a few bugs, including one that was
preventing LDAP users with 2FA enabled from logging in, which we think is an
important feature.

Read on for all the details!

<!-- more -->

It includes the following changes:

- **CE/EE:** Bump required gitlab-workhorse version to bring in a fix for
  missing artifacts in the build artifacts browser ([!2616])
- **CE/EE:** Get rid of those ugly borders on the file tree view ([!2615])
- **CE/EE:** Fix updating the runner information when asking for builds
  ([!2618])
- **CE/EE:** Bump gitlab_git version to 7.2.24 in order to bring in a
  performance improvement when checking if a repository was empty ([!2535])
- **CE/EE:** Add instrumentation for Gitlab::Git::Repository instance methods so
  we can track them in Performance Monitoring. ([!2528])
- **CE/EE:** Increase contrast between highlighted code comments and inline diff
  marker ([!2629])
- **CE/EE:** Fix method undefined when using external commit status in builds
  ([!2576])
- **EE:** Elasticsearch indexer performance improvements ([!140])
- **EE:** Don't redirect away from Mirror Repository settings when repo is empty
  ([!135])
- **EE:** Fix updating of branches in mirrored repository ([!136])
- **EE:** Fix a 500 error preventing LDAP users with 2FA enabled from logging in
  ([!146])
- **EE:** Rake task gitlab:elastic:index_repositories handles errors and shows
  progress ([!143])
- **EE:** Partial Elasticsearch indexing of repo on push ([!142])

[!2528]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2528
[!2535]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2535
[!2576]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2576
[!2615]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2615
[!2616]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2616
[!2618]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2618
[!2629]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2629
[!135]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/135
[!136]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/136
[!140]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/140
[!142]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/142
[!143]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/143
[!146]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/146

## Elasticsearch re-indexing

If you have already enabled Elasticsearch in your Enterprise Edition, you will
have to rebuild the indexes of the Git repositories to benefit from the new
indexer function. The new indexer works 8 times faster than in GitLab versions
8.4.0 and 8.4.1, and the indexes will be much smaller.

In case your repositories are very large, you might want to check the
documentation on [Indexing large repositories][es-large-index].

[es-large-index]: http://doc.gitlab.com/ee/integration/elasticsearch.html#indexing-large-repositories "Elasticsearch - Indexing large repositories"

1.  First, remove the indexes from Elasticsearch:

    ```bash
    curl -X DELETE 'http://localhost:9200/repository-index-development,projectwiki-index-development/'
    ```

    The above request should return `{"acknowledged":true}`.

1.  And then build the new ones:

    ```bash
    # Omnibus installations
    gitlab-rake gitlab:elastic:index_repositories
    gitlab-rake gitlab:elastic:index_wikis

    # Installations from source
    bundle exec rake gitlab:elastic:index_repositories RAILS_ENV=production
    bundle exec rake gitlab:elastic:index_wikis RAILS_ENV=production
    ```

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
