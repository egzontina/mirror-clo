---
title: "GitLab 7.12 released with SAML support, Merge Request Approvers and .gitlab-ci.yml"
date: 2015-06-22
categories: release
author: Job van der Voort
author_twitter: Jobvo
image_title: /images/7_12/sf.jpg
---

A new season is in, and so is GitLab 7.12! This month's release brings some big
additions and changes to Community Edition (CE), Enterprise Edition (EE) and Continuous Integration (CI).
In both CE and EE, GitLab now supports authentication using
SAML! This was requested by many and we're very happy that CERN
was so kind to contribute this. In GitLab Enterprise Edition you can now require multiple
people to approve a merge request before it can be merged. In GitLab CI, we're
introducing the `.gitlab-ci.yml` file, making job scripts much easier to manage.

This month's MVP was an easy choice. Alexandre Lossent from [CERN](http://home.web.cern.ch/)
(where the web was born) contributed the SAML code they
wrote for their own usage. We're very happy with this contribution and are sure
many of you will make use of this.
Thanks Alexandre!

<!--more-->

## SAML Support

With Alexandre's contribution, GitLab can now be configured to act as
a SAML 2.0 Service Provider. This allows GitLab to consume assertions from a SAML 2.0
Identity Provider (IdP) such as Microsoft Active Directory Federation Services to authenticate users.

See our [documentation on how to setup SAML integration](http://doc.gitlab.com/ce/integration/saml.html).

## Web Hook for Comments

There is a new webhook available that will trigger on all comments.
You could use this to add additional automations and integrations to GitLab.
For instance when someone comments on a merge request, you can have it
trigger internal systems or, depending on the comment contents,
run a certain build.

## Better performance for the Web Editor

Every new release of GitLab is faster than the last, but in this release
we did something special. Instead of performing code changes via the web
interface by cloning the bare repository to a temporary location, committing
there, and then pushing the changes back to the bare repository, we now commit
your changes directly into the bare repository. This has significantly
improved the performance of the web editor.

## UI Update

Every month we experiment and tune our UI to be better, prettier and more intuitive
and this month is no different.

We've moved your profile link to the bottom left and updated the looks of
various parts of the UI.

![Profile bottom left](/images/7_12/profile.png)

## Merge Request Approvers (EE only)

If you want to make sure that merge requests on your favorite project are
reviewed by more than one person before they are merged, you can now configure a minimum number of Merge Request approvals for it.

You simply set the amount of approvals that a merge request needs before allowing
it to be merged and GitLab will restrict anyone from merging until the set amount
of approvals has been met.

![Setting up merge request approvers](/images/7_12/approvals_settings.png)
![Using merge request approvers](/images/7_12/approvals_mr.png)

We'd love to hear how you are using this feature in your organization.

## Git hook to check Maximum File Size (EE only)

We've added a new Git Hook that allows you to restrict the incoming commits
with large files. You can simply set the threshold
and GitLab will block all future Git pushes containing files that are too big.
This can be used to prevent people from committing build artifacts, or to motivate them to use git-annex or some other form of large file storage when that's more appropriate.

## LDAP Group Sync improvements (EE only)

We've made several improvements to LDAP Group sync in GitLab EE.
It now checks for several more attributes when syncing and
prevents the sync from removing the last owner in a group.

## `.gitlab-ci.yml` file replaces jobs (CI)

As [announced on May 6](https://about.gitlab.com/2015/05/06/why-were-replacing-gitlab-ci-jobs-with-gitlab-ci-dot-yml/)
we're replacing GitLab CI jobs with a `.gitlab-ci.yml` file stored in the code repository.
The advantages are listed in the announcement but the main ones are:

1. Since the build script is version controlled, more people can see it and propose changes
1. Older and newer branches build correctly since they can contain a different build file
1. Forks automatically get a proper build script that gets updated when they merge upstream in
1. You can experiment with CI build settings in your branch without breaking other branches

The above things are not possible with Jenkins-like scripts that are the same for the whole project.

### How it works

GitLab sends the web-hook and the `.gitlab-ci.yml` contents
to the CI Coordinator, which creates builds based on the YAML file. In turn,
these builds are executed by the Runners as it was before.

Here is an example of YAML file:

```
before_script:
  - gem install bundler
  - bundle install
  - bundle exec rake db:create

rspec:
  script: "rake spec"
  tags:
    - ruby
    - postgres
  only:
    - branches

spinach:
  script: "rake spinach"
  tags:
    - ruby
    - mysql
  except:
    - tags

staging:
  script: "cap deploy staging"
  type: deploy
  tags:
    - capistrano
    - debian
  except:
    - stable

production:
  script:
    - cap deploy production
    - cap notify
  type: deploy
  tags:
    - capistrano
    - debian
  only:
    - master
    - /^deploy-.*$/
```

We include a Lint tool to check your syntax. It is available in every GitLab CI instance by the short url `/lint`.
If something goes wrong with your `.gitlab-ci.yml` after push your code you will be able to see errors in the commit page.

The `before_script` section will be performed before each job.
You can define a deploy job by adding `type: deploy`.
Every job contains parameters such as `script` (shell script), `tags`
(only runner with this tag/tags can pick this build) and `only` or `except` parameter
that defines branch names allowed to run build on.
The `only` section takes precedence over the "except".
You can read more information about new syntax in the
[Configuration of your builds with .gitlab-ci.yml](http://doc.gitlab.com/ci/yaml/README.html)

The new format is inspired by the work of Travis CI and Circle CI who are already using YAML files.
Initially we considered using the open source modules of Travis CI,
but we ended up writing our own so we could offer:

1. Customizable deploy jobs
1. Ability to run jobs on metal, VM's and docker images
1. Ability to run on the same machine each time (for example for performance testing)
1. Ability to run on special architectures (for example a Raspberry Pi 2)
1. Ability to run on machines in a special place or with certain credentials
1. A simple and shallow syntax for the YAML file
1. Named jobs, so they are easily recognizable

Because of this, the "one image per architecture and that's it" -approach was not an option.
As you are able to tag runners and jobs, this gives you a lot of freedom in
assigning a job to a certain runner.
We hope the new format combines the freedom of Jenkins
with the user friendliness of Travis CI.

### Migrating

Upon upgrading to GitLab 7.12, your CI job scripts will be converted automatically
into an example `.gitlab-ci.yml` file, which you can view and download in the
project page in GitLab CI.

On a push that triggers a build, GitLab sends along the `.gitlab-ci.yml` file
from the root of the repository. If this is not present, GitLab CI will make use
of the generated example script. This means your projects that are not updated
should work fine. However, we do recommend that you add the `.gitlab-ci.yml`
file to the root of your repository as soon as possible.

You should add `.gitlab-ci.yml` files to all branches in your projects that receive
ongoing Git pushes.

## BETA: Secret Variables for runner (CI)

We've added a new function to GitLab CI that allows you to set secret variables
for runners. Secret variables will be set to the environment by the runner
and will be hidden from the build log.
Use them for passwords, secret keys or anything else.
Make sure you have runner version 0.4 or greater (released today).

This feature is currently in beta.
Secrets added to GitLab CI 7.12 will be stored in its SQL database WITHOUT encryption.
We will add encryption in 7.13.


![Secret Variables](/images/7_12/secrets.png)

## Other changes

This release has more improvements, including security fixes, please check out [the Changelog](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CHANGELOG) to see the all named changes.

- - -

## Upgrade barometer

This release only adds minor migrations.
If you are on GitLab 7.11 CE or EE you can upgrade to 7.12 while staying online.

#### Changed behavior for 'secret_token' settings when using Omnibus packages

If you set a custom value for `gitlab_rails['secret_token']`, `gitlab_shell['secret_token']` or `gitlab_ci['secret_token']` in `/etc/gitlab/gitlab.rb` then please double-check that the value in `gitlab.rb` matches the value in `/etc/gitlab/gitlab-secrets.json`.
If some of the values do not match, copy the values from `gitlab-secrets.json` to `gitlab.rb` prior to upgrading to GitLab 7.12.

Prior to 7.12, any `secret_token` values you had in `gitlab.rb` were actually being ignored in favor of whatever is in `gitlab-secrets.json`.
This was an unexpected behaviour as it was expected that specifying a setting in gitlab.rb always takes precedence.

On most GitLab omnibus installations the 'secret_token' values are set only in `gitlab-secrets.json`, and no action is required.

This change only applies to GitLab omnibus packages.
Installations from source are not affected.

#### Changed detection of the operating system init

When running `gitlab-ctl reconfigure` omnibus-gitlab needs to decide if the system
is using SysV init, Upstart or Systemd so it can install the `gitlab-runsvdir` service.

Prior to this version, this decision was being done by looking at the platform and version of the OS and what the default init for that system was.

This was unreliable and with omnibus-gitlab being installable on more OS' code that handles this became complicated and error prone.

From this release onwards, this has been replaced and detection is done by querying the OS init system. Based on this response `gitlab-runsvdir` service is installed.

If you encounter an issue as described in [omnibus-gitlab README](https://gitlab.com/gitlab-org/omnibus-gitlab/tree/master#reconfigure-freezes-at-ruby_blocksupervise_redis_sleep-action-run) try applying the workaround and raise an issue on the omnibus-gitlab issue tracker.

#### Updated recommended SSL cipher suites

Following the [Logjam vulnerability](/2015/05/21/security-advisory-for-logjam-vulnerability/) we changed the recommended SSL cipher suites in omnibus-packages and installations from source. More details can be found in [this blogpost](/2015/06/17/gitlab-com-and-logjam/).

- - -

## Installation

If you are setting up a new GitLab installation please see the
[download GitLab page](https://www.gitlab.com/downloads/).

## Updating

Check out our [update page](https://about.gitlab.com/update/).

## Enterprise Edition

The mentioned EE only features and things like LDAP group support can be found in GitLab Enterprise Edition.
For a complete overview please have a look at the [feature list of GitLab EE](http://www.gitlab.com/gitlab-ee/).

Access to GitLab Enterprise Edition is included with a [subscription](http://www.gitlab.com/pricing/).
No time to upgrade GitLab yourself?
A subscription also entitles you to our upgrade and installation services.
