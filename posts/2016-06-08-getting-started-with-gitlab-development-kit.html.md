---
layout: post
title: "Getting Started with GitLab Development Kit"
date: 2016-06-08
author: Drew Blessing
author_twitter: drewblessing
categories: contributing,development
image_title: '/images/default-blog-image.png'
---

> This post is part of a series [Celebrating 1,000 Contributors][1k-post]

GitLab is built on open-source and has a thriving community. We appreciate all
of our existing contributors and we look forward to welcoming new contributors,
as well. This post is helpful if you've considered developing a feature or fix
for GitLab but are unsure how to set up a development environment.

As with any Rails application, GitLab has a few moving parts: a database, Redis,
Sidekiq, the Rails application server, GitLab Workhorse, and GitLab Shell. It
can be a challenge to configure each of these components on your own. That's why
we created the GitLab Omnibus packages for users, recently highlighted in
[another blog post][omnibus-blog-post]. Perhaps not as well known is that we
also have the [GitLab Development Kit (GDK)][gdk] to improve the experience for
developers. In this post we'll go through the steps necessary to get GDK set up
on your workstation.

<!-- more -->

All of the details here were obtained from the GDK [README file][gdk-readme],
which is comprehensive and should be your first resource when you have
questions.

## Installing Prerequisites

First, you need to install some prerequisite items. Every platform has
different requirements and we've outlined the steps for each in the
['Prerequisites for all platforms'][gdk-prereq] section of the README. We have
instructions for Mac, Ubuntu, Arch Linux, Debian, Fedora, and CentOS/Red Hat.
For example, to install prerequisites for a Mac, run the following commands in
Terminal:

```bash
brew tap homebrew/dupes
brew tap homebrew/versions
brew install git redis postgresql libiconv icu4c pkg-config cmake nodejs go openssl node npm
bundle config build.eventmachine --with-cppflags=-I/usr/local/opt/openssl/include
npm install phantomjs@1.9.8 -g
```

## Installation

Next, clone the GDK repository:

```
cd /path/to/your/workspace
git clone git@gitlab.com:gitlab-org/gitlab-development-kit.git
cd gitlab-development-kit
```

Before configuring GDK, fork any GitLab repositories that you plan
to contribute to. By default, GDK will install using the source repositories,
such as `https://gitlab.com/gitlab-org/gitlab-ce.git`. Community members do not
have privileges in the main `gitlab-ce` project so you will need a fork to
submit merge requests. Here is a list of various GitLab repositories you may
want to fork:

- **GitLab CE** - [https://gitlab.com/gitlab-org/gitlab-ce](https://gitlab.com/gitlab-org/gitlab-ce)
- **GitLab EE** - [https://gitlab.com/gitlab-org/gitlab-ee](https://gitlab.com/gitlab-org/gitlab-ee)
- **GitLab Shell** - [https://gitlab.com/gitlab-org/gitlab-shell](https://gitlab.com/gitlab-org/gitlab-shell)
- **GitLab Workhorse** - [https://gitlab.com/gitlab-org/gitlab-workhorse](https://gitlab.com/gitlab-org/gitlab-workhorse)

After forking any of the above repositories, you are ready to run the `make`
command to install all components. Be sure to tell `make` about your forks.
If you chose not to fork one or more repositories you can leave off the
corresponding argument and GDK will use the source repository.

```bash
make gitlab_repo=git@gitlab.com:example/gitlab-ce.git gitlab_shell_repo=git@gitlab.com:example/gitlab-shell.git gitlab_workhorse_repo=git@gitlab.com:example/gitlab-workhorse.git
```

The above `make` command installs and configures all components.
Then, run `support/set-gitlab-upstream` to automatically add an upstream remote
in each cloned GitLab component. This will ensure that upstream changes are
pulled in later when you run `make update`.

Start GDK by executing `./run`. All components will be started and output will
be logged to the console. You can access GitLab in your browser at
`http://localhost:3000` or press `Ctrl-C` to stop all processes.

## Making changes

The various component repositories are all cloned inside the GDK directory.
For example, GitLab code is checked out in `$GDK_HOME/gitlab`. Change in to
this directory and check out a new feature branch.

As you make changes you can refresh your browser to see the effects. In some
cases, you may need to restart GDK to load the change. Restart by pressing
`Ctrl-C` and then execute `./run` again.

## Running tests

Some changes will require writing tests, or running existing tests to ensure
you didn't break anything. GDK makes this very easy using the following commands:

- `rake spinach` to run the spinach suite
- `rake spec` to run the rspec suite
- `rake gitlab:test` to run all the tests

GitLab has a lot of tests and it can take a long time to run the full suite.
Use the following command format to run tests in a single file:

- `bundle exec rspec spec/controllers/commit_controller_spec.rb` for a rspec test
- `bundle exec spinach features/project/issues/milestones.feature` for a spinach test

## Opening a merge request

If all tests pass and you're ready to submit for review, commit the changes and
push them to your fork. Then, visit GitLab.com and you should notice a banner
near the top. Click the blue 'Create Merge Request' button to initiate a merge
request. This will create a merge request from your fork to the GitLab source
project so our team can review your contribution.

![Last push widget](/images/gdk/last_push_widget.png)

Congratulations! After installing the GitLab Development Kit you are
well-equipped to contribute to GitLab. We're happy to welcome you to our
community and look forward to your future contributions.

For more information on contributing to GitLab, please see our
[Contributing Guide][contrib-guide].

[1k-post]: https://about.gitlab.com/2016/05/24/1k-contributors/
[omnibus-blog-post]: https://about.gitlab.com/2016/03/21/using-omnibus-gitlab-to-ship-gitlab/
[gdk]: https://gitlab.com/gitlab-org/gitlab-development-kit/
[gdk-readme]: https://gitlab.com/gitlab-org/gitlab-development-kit/blob/master/README.md
[gdk-prereq]: https://gitlab.com/gitlab-org/gitlab-development-kit/tree/master#prerequisites-for-all-platforms
[contrib-guide]: https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CONTRIBUTING.md
