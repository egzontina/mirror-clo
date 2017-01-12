---
title: "GitLab 8.12 Released with Cycle Analytics and Global Code Search"
categories: release
author: Job van der Voort
author_twitter: Jobvo
image_title: "/images/8_12/header.jpg"
description: "GitLab 8.12 with Cycle Analytics, Global Code Search, Merge Request Versions, Review Apps, Push rules to prevent secrets and much, much more!"
twitter_image: '/images/tweets/gitlab-8-12-released.png'
---

Whether you're working on a small or a large project, your tools should get out of your way and give you actionable feedback. This month, we're making sure GitLab does both better than ever.

GitLab 8.12 gives you feedback on how efficiently you actually work, helps you find code across the entire instance, makes your workflow much safer with a single click, and much more.

This month's Most Valuable Person ([MVP](https://about.gitlab.com/mvp/)) is
James Munnelly for contributing the
[Kubernetes executor in the GitLab CI runner](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/30).
This feature allows users to run CI tests in a Kubernetes cluster easily.
James created this merge request over a year ago and showed great patience
and persistence in the review process to see it to completion.
Thanks, James!

<!--more-->

## Cycle Analytics

Reducing cycle time, the time it takes you to go from idea all the way to
production, is the [first principle of conversational development][convdev].
The shorter the cycle time, the higher the efficiency of your team.

In order to make it possible to actually see what your cycle time is, we're
introducing [Cycle Analytics][cycle-analytics] with GitLab 8.12.

![Cycle Analytics in GitLab 8.12](/images/8_12/cycle_analytics.png)

Cycle Analytics tells you what your cycle time is and breaks it down into
several steps, so you can quickly see where to improve and accurately predict
when you're shipping something.

Find Cycle Analytics under Pipelines in all your projects.

[convdev]: https://about.gitlab.com/2016/09/14/gitlab-live-event-recap/#convdev
[cycle-analytics]: /2016/09/21/cycle-analytics-feature-highlight/

> Read more in the [documentation for Cycle Analytics](https://docs.gitlab.com/ce/user/project/cycle_analytics.html)

## Global Code Search (EE)

If you're running Elasticsearch on your GitLab Enterprise Edition instance,
you will now be able to search through _all_ code on the server!

![Global code search in GitLab EE 8.12](/images/8_12/search.gif)

Just use the search as before and GitLab will show you matching code from each
project you have access to.

Note that this change requires that you rebuild your Elasticsearch index.
See the upgrade barometer below for more information.

## Merge Request Versions

When you're pushing more than a single commit to a merge request,
it can be hard to view what changed between versions and the target branch.

![Merge Request Versions in GitLab 8.12](/images/8_12/mr_versions.png)

With merge request versions you can view previous states of a merge request: compare between a previous commit and the target branch or even between versions, showing you what has changed between certain commits.

> Read more in the [documentation for Merge request revisions](https://docs.gitlab.com/ce/user/project/merge_requests/versions.html)

## Preventing Secrets in your repositories (EE)

It's a bad idea to commit secrets (such as keys and certificates) to your repositories: they'll be cloned to the machines of anyone that has access to the repository, only one of which has to be insecure for the information to be compromised.

Yet it happens quite easily. You write `git commit -am 'quickfix' && git push` and suddenly you've committed files that were meant to stay local!

GitLab now has a new push rule that will prevent commits with secrets from entering the repository. Just check the checkbox and GitLab will prevent common unsafe files such as `.pem` and `.key` from being committed.

![Prevent secrets in your repo in GitLab EE 8.12](/images/8_12/secrets.png)

GitLab Enterprise Edition already had a feature that allows you to block files based on a regular expression, which you can leverage to block anything that we didn't think of. We also welcome suggestions and contributions to make this push rule even better.

> Read more in the [documentation on Push rules](https://docs.gitlab.com/ee/push_rules/push_rules.html#prevent-pushing-secrets-to-the-repository)

## Review Apps (Experimental)

We've made several additions to CI that, when combined, make some magic.

You can now use predefined CI variables as a name for environments. In addition, you can specify a URL for the environment configuration in your `.gitlab-ci.yml` file. Together, these features bring the first iteration of Review Apps.

Review apps are automatically-created environments that run your code for each branch. That means merge requests can be reviewed in a live-running environment. This was inspired by [Heroku's Review Apps](https://devcenter.heroku.com/articles/github-integration-review-apps) which itself was inspired by [Fourchette](https://github.com/rainforestapp/fourchette).

These are small changes, but will make a huge impact on your development flow.
Reviewing anything from performance to interface changes becomes much easier
with a live environment.

Right now, Review Apps are labelled experimental, as the environments are not automatically destroyed when no longer necessary.

We're [working on a blog post](https://gitlab.com/gitlab-com/blog-posts/issues/275) that will have an example.

## SSH Authentication for LFS

If you're used to using SSH for your Git pushes, it was frustrating to
still have to enter credentials whenever using LFS.

GitLab will now leverage your SSH key when using LFS, meaning that if you're
using LFS while connecting through SSH, you no longer have to manually
enter your credentials!

File transfers of LFS still happen over HTTP.

## Toggle LFS

Git LFS (Large File Storage) is great, but as the name implies, it can have
significant impact on your disk capacity. To make you feel a bit more secure about the LFS usage on your instance, you can now toggle LFS on instance, group, and project levels.

For instance, as a GitLab administrator, you can decide to turn off LFS for the entire instance, yet enable it for only a single group or project.

## Limit Project Size (EE)

As an alternative to restricting LFS, you might just want to prevent projects
from growing too large. You can now limit project size. This will take into account all repository data and LFS objects and stop any commits that will surpass that limit.

![Limit project size in GitLab EE 8.12](/images/8_12/repo_size.png)

You can set a global project limit and override that on group and project level, as an admin. This way, you can give particular projects extra space if necessary.

> Read mote in the [documentation about limiting the repository size](https://docs.gitlab.com/ee/user/admin_area/settings/account_and_limit_settings.html#repository-size-limit)

## LDAP/Active Directory Improvements

This release contains several improvements to LDAP/Active Directory support
for GitLab CE and EE:

- CE/EE - Request only the LDAP user/group attributes that GitLab requires (CE [!6187] and EE [!712]), reducing the amount of data across the wire between GitLab and the LDAP/Active Directory server. This also decreases the object memory footprint within GitLab.
- EE - Faster Active Directory nested group and ranged member (large group) retrieval ([!719])
- EE - Add 'Sync now' option to group membership page when LDAP group links are present ([!704])

[!6187]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6187
[!712]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/712
[!719]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/719
[!704]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/704

## Recover 2FA tokens through SSH

You can now recover your 2FA security codes using SSH. This should make it
easier to recover your account, while still maintaining a level of security.

> Read more in the [documentation about recovering 2FA via SSH](https://docs.gitlab.com/ce/user/account//two_factor_authentication.html#generate-new-recovery-codes-using-ssh).

## Filter Tags by Name

Want to quickly find a tag? That's much easier now with a handy little filter on top:

![Filter tags by name in GitLab 8.12](/images/8_12/tag_filter.png)

## API additions

We've expanded our API on several points with GitLab 8.12:

- Allow to set `request_access_enabled` for groups and projects using API
- Add `notification_settings` API calls
- Add a `BroadcastMessage` API
- You can now fork to a specific namespace through the API
- Allow to set enable/disable access request for groups and projects.
- Add `web_url` field to issue, merge request, and snippet objects.  (community contribution)
- Expose `sha` and `merge_commit_sha` in merge request API.  (community contribution)
- Expose issue confidentiality flag.  (community contribution)
- Added `only_allow_merge_if_build_succeeds` project setting.  (community contribution)
- Add endpoint to lint your `.gitlab-ci.yml` file.  (community contribution)
- Add an API to list manual actions on Environments and Deployments

[!6359]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6359

## Improved GitHub Importer

Our GitHub importer keeps getting better, making it easier to migrate to
GitLab. With GitLab 8.12, the importer will also copy release notes over to
GitLab and now lets you choose the namespace you want your imported projects
to go into.

![Improved GitHub importer in GitLab 8.12](/images/8_12/gh_namespace.png){: .shadow}

This should make it easier to migrate if you already have existing projects
or prefer something different than GitLab's way of importing your projects.

> Read more in the [documentation about importing your repositories from GitHub](https://docs.gitlab.com/ce/workflow/importing/import_projects_from_github.html).

## Bulk update Merge Requests

You can now bulk update merge requests. This means you can set the status, assignee, milestone, label or subscription to multiple merge requests at once.

![Bulk update Merge Requests in GitLab 8.12](/images/8_12/bulk.gif)

Managing merge-request-heavy project should be a lot easier with this!

[!6226](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6226)

## Build Grouping

If you have many similar builds, your pipeline graph becomes very long. We've made a small change to improve this: similar builds will now automatically group together.

![Build grouping in GitLab 8.12](/images/8_12/build_grouping.png){: .shadow}

## Expanded syntax highlighting

By upgrading to [rouge](https://github.com/jneen/rouge) 2.0.6, we've added syntax highlighting for JSX, Prometheus, mxml, 1c, turtle/trig, vhdl, and improved highlighting for Swift 3.

## Sentry integration of Workhorse

GitLab-Workhorse can now report application errors to Sentry.

> [Read more in the GitLab-Workhorse docs](https://gitlab.com/gitlab-org/gitlab-workhorse/blob/master/README.md#error-tracking)

## GitLab Runner 1.6

We are also releasing GitLab Runner 1.6 today. Some highlights:

- Kubernetes executor ([!30](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/30) and [!277](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/277)), this allows Kubernetes to automatically scale the number of CI runners. All your builds will be processed immediately without having idle machines running when it's not busy.
- Autocompletion of _/ci_ in GitLab URL while registering the Runner ([!289](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/289))
- Configuration options for specifying scripts executed before clone/fetch is done and before build script is executed ([!106](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/106))
- Improvements in passing CA certificates to builds ([!299](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/299))
- Improvement in disabling recursive submodules fetching/cloning ([!314](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/314))
- Improve docker machine logging ([!234](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/234))
- Add possibility to specify a list of volumes to inherit from another container ([!236](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/236))
- Generate a `BuildError` instead of `SystemError` when Docker/Kubernetes image is missing ([!295](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/merge_requests/295))

To see the full list of all changes please read [the Runner's CHANGELOG file](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/CHANGELOG.md).

## GitLab Mattermost 3.4

GitLab 8.12 includes [Mattermost 3.4](https://about.mattermost.com/mattermost-3-4/),
an [open source Slack-alternative](https://about.mattermost.com) whose newest
release offers 700 integrations with full Markdown support via Zapier,
simplified bot and 3rd party authentication via OAuth2, and community
integrations with Gitter, Heroku, Pivotal Tracker, Chef, Ansible and Yunohost.

## Performance Improvements

* Sidekiq processes now use a connection pool when using Rails' caching
  mechanism: [merge request](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6429)
* The `oj` Gem is now used for faster JSON processing: [merge request](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6395)
* The column `projects.last_activity_at` is only updated once an hour to reduce
  database load: [merge request](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6391)
* The column `projects.pushes_since_gc` has been moved from the database to
  Redis to reduce database load: [merge request](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6326)
* Protected branch checks are not performed when no branch name is known,
  reducing time spent in this process: [merge request](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6317)
* Checking if one can resolve a note is only done when notes can be resolved in
  the first place: [merge request](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6298)
* The `ci_runners` table is now updated less frequently to reduce database load:
  [merge request](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/6126)
* The number of database queries used for the "Builds" tab for
  commits/merge requests has been reduced: [merge request](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5957)
* The payload size for the contributions calendar has been reduced:
  [merge request](https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/5784)

## Build permissions changes

GitLab 8.12 brings very important changes to build permissions.

We decided that build permissions should be tightly integrated with the
permissions of the user triggering a build for the following reasons:

- We already have a permission system in place: group and project membership of
  users.
- We already know who is triggering a build (using git push, using web,
  executing triggers).
- We already know what that user is allowed to do.
- We use the user's permissions for builds that are triggered by pusher.
- It is simple and convenient that your build can access everything that you
  have access to.
- We can issue a short-lived unique tokens, granting access for the duration of
  the build.
- It fits very well into our philosophy of having everything integrated.
- This provides a lot of possibilities to further enforce user permissions, such
  as allowing only specific users to access runners, secure variables and
  environments.

Now, any build that was triggered by the user is also signed with his
permissions. When a user does `git push` or modifies files through the UI (**the
pusher**), we will create a new Pipeline. The Pipeline will be owned by the
pusher. So builds created in this pipeline will have the permissions of **the
pusher**.

This allows us to make it easy to evaluate access for all dependent projects and
container images that the pusher would have access too. The permission is
granted only for the duration of the build. The access is revoked after the
build is finished.

For detailed information about the build permissions and the changes it brings
please see [our documentation](https://docs.gitlab.com/ce/user/permissions.html#build-permissions).

For the history and reasoning behind this change, you can read the full
discussion in [the issue](https://gitlab.com/gitlab-org/gitlab-ce/issues/18994).

## Submodules in CI

Submodules were one of the reasons we redesigned the build permissions.
Now using Submodules in your CI builds is easy.

To use submodules you have to use a `.gitmodules` file, which looks something
like this:

```ini
[submodule "tools"]
    path = tools
    url = git@gitlab.com/group/tools.git
```

To use the new build permissions for your submodules you have to convert your
URLs to be relative:

```ini
[submodule "tools"]
    path = tools
    url = ../../group/tools.git
```

This will instruct Git to use the same credentials as it would for checking out
your project sources.

The last step is to tell GitLab CI to fetch submodules:

```yaml
before_script:
  - git submodule update --init --recursive
```

You can read more about support for submodules in our [documentation](https://docs.gitlab.com/ce/user/project/new_ci_build_permissions_model.html#git-submodules).

## Other changes

This release has more improvements, including security fixes. Please check out
[the Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG.md)
to see the all named changes.

## Upgrade barometer

This release requires downtime due to foreign keys being added, column types
being changed, and various columns being removed from some tables. The whole
migration process could take up to 30 minutes for large instances. Smaller instances should expect a downtime of about 10-15 minutes.

### (EE Only) Elasticsearch re-indexing

We changed the structure of Elasticsearch index for repositories, making use of Parent Child relationships. This requires a total rebuild of the ES index. Also
Elasticsearch 2.3.x contains a bug that causes to fail all queries that use highlight feature and Parent Child relationship at once, so we recommend to use the version 2.4 and newer. After upgrading to GitLab 8.12, you will need to remove the old index and rebuild new index:

To remove the old index, call to Elasticsearch:

```
curl -XDELETE 'http://localhost:9200/gitlab-production/'
```

Then rebuild new indexes as described in [Elasticsearch integration](http://docs.gitlab.com/ee/integration/elasticsearch.html#add-gitlabs-data-to-the-elasticsearch-index)

### Ruby Update

In our last release blog post we mentioned we'd be dropping Ruby 2.1.x support in GitLab 8.13, we no longer plan to stop supporting Ruby 2.1.x in
the near future.

We still recommend you upgrade to Ruby 2.3 if you're running a source
installation, as this is the same version that ships with our Omnibus package
now.

### Expanded usage data ping (EE)

In order to better understand the usage of GitLab by our customers,
GitLab 8.12 EE now sends additional data along with its usage ping.

No information about the nature of the data, such as project names, comments or
other content is transmitted. You can view the exact data that is sent in
the admin settings, where this feature can also be disabled entirely.

> [See also the implementation in the merge request](https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/735)

### GitLab-Workhorse Secret Key

GitLab-Workhorse now uses a secret key to sign certain messages sent
to the GitLab Rails application. For now this is mostly a
configuration sanity check; in future releases we want to add features
to GitLab-Workhorse that require this secret key to establish trust.

If you use our Omnibus packages, or if you installed GitLab from
source with our official init.d script, then this secret key will be
generated and picked up automatically for you. If you use a custom
init.d script or if you use packages not created by GitLab Inc. then
you may have to set the `-secretPath` option on GitLab-Workhorse.

### Note

We assume you are upgrading from the latest version. If not, then also consult the upgrade barometers of any intermediate versions you are skipping.
If you are upgrading from a GitLab version prior to 8.0 *and* you have CI enabled, you have to upgrade to GitLab 8.0 [first](https://about.gitlab.com/2015/09/22/gitlab-8-0-released/).

Please be aware that by default the Omnibus packages will stop, run migrations,
and start again, no matter how “big” or “small” the upgrade is. This behavior
can be changed by adding a [`/etc/gitlab/skip-auto-migrations`
file](http://doc.gitlab.com/omnibus/update/README.html).

----

## Installation

If you are setting up a new GitLab installation please see the
[download GitLab page](https://about.gitlab.com/installation/).

## Updating

Check out our [update page](https://about.gitlab.com/update/).

## Enterprise Edition

The mentioned EE only features and things like LDAP group support can be found in GitLab Enterprise Edition.
For a complete overview please have a look at the [feature list of GitLab EE]( https://about.gitlab.com/features/#enterprise).

Access to GitLab Enterprise Edition is included with a
[subscription]( https://about.gitlab.com/pricing/).
No time to upgrade GitLab yourself?
A subscription also entitles you to our upgrade and installation services.

----
