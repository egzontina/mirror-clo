---
title: "Implementing .gitlab-ci.yml"
date: 2015-06-08
author: Job van der Voort
author_twitter: Jobvo
---

We [wrote] about why we're replacing GitLab CI jobs with a `.gitlab-ci.yml` file.
As we've started on implementing this large change, we wanted to share the details
of that process with you and would love to hear what you think.

<!-- more -->

To recap the [previous article]:
currently you are required to write out your CI jobs in GitLab CI's interface.
We're replacing this with a single file `.gitlab-ci.yml`, that you place in the root
of your repository.

## Schema change

Currently, on a push to GitLab, GitLab sends a web-hook to the CI Coordinator.
The coordinator creates a build based on the jobs that are defined in its UI,
which can then be executed by the connected Runners.

In the new schema, GitLab sends the web-hook _and the `.gitlab-ci.yml`_ contents
to the CI Coordinator, which creates builds based on the yml file. In turn,
these builds are executed by the Runners as before.

## Migrating to new style

Keeping two different ways of doing things would be a strain on development and
support, not to mention confusing. So we're not just deprecating the old style
of defining jobs, we're removing it entirely and will migrate existing jobs.

Upon upgrading your existing jobs defined in the GitLab CI Coordinator will be
converted into a YAML file with the new syntax. You can download this file at any
time from the project settings.

When the GitLab webhook triggers and doesn't transmit the content from `.gitlab-ci.yml`,
the coordinator will use the converted YAML file instead.

This makes migrating to the new style very easy. You can start by simply copy-pasting
the contents of the converted YAML file to the root of your repository. Existing projects
will continue to build successfully, yet new projects do not have the option to
use anything else.

## An example `.gitlab-ci.yml`

To get an idea of how the `.gitlab-ci.yml` will look, we've prepared an example
for a Ruby on Rails project (such as GitLab itself). Of course, this is due to
change as we're still working on this.

```
# Refs to skip
skip_refs: “deploy*”

# Run before each script

# Refs to skip
skip_refs: “deploy*”

# Run before each script
before_script:
  - export PATH=$HOME/bin:/usr/local/bin:/usr/bin:/bin
  - gem install bundler
  - cp config/database.yml.mysql config/database.yml
  - cp config/gitlab.yml.example config/gitlab.yml
  - touch log/application.log
  - touch log/test.log
  - bundle install --without postgres production --jobs $(nproc)
  - “bundle exec rake db:create RAILS_ENV=test”

# Parallel jobs, each line is a parallel build
jobs:
  - script: “rake spec”
    runner: “ruby,postgres”
    name: “Rspec”
  - script: “rake spinach”
    runner: “ruby,mysql”
    name: “Spinach”
    tags: true
    branches: false

# Parallel deploy jobs
on_success:
  - “cap deploy production”
  - “cap deploy staging”
```

<a id="update"></a>

## UPDATE

Dmitriy and Sytse spend some time thinking about file syntax.
Scripting should be simple and memorable. Thats why we come with better proposal:

```
before_script:
  - gem install bundler
  - bundle install
  - bundle exec rake db:create

rspec:
  test: "rake spec"
  tags:
    - ruby
    - postgres
  only:
    - branches

spinach:
  test: "rake spinach"
  tags:
    - ruby
    - mysql
  except:
    - tags

staging:
  deploy: "cap deploy stating"
  tags:
    - capistrano
    - debian
  except:
    - stable

production:
  deploy:
    - cap deploy production
    - cap notify
  tags:
    - capistrano
    - debian
  only:
    - master
    - /^deploy-.*$/
```

## Contribute

GitLab is nothing without its community.
Contribute or follow the development in the [GitLab CI repository].

[wrote]: https://about.gitlab.com/2015/05/06/why-were-replacing-gitlab-ci-jobs-with-gitlab-ci-dot-yml/
[previous article]: https://about.gitlab.com/2015/05/06/why-were-replacing-gitlab-ci-jobs-with-gitlab-ci-dot-yml/
[GitLab CI repository]: https://gitlab.com/gitlab-org/gitlab-ci/commit/c2c9236cde807e98ff9571f8d23ac4def75eb9ba