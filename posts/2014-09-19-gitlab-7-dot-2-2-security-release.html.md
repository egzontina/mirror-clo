---
title: "GitLab 7.2.2 Security Release and hooks migration"
date: 2014-09-19
categories:
author: Jacob Vosmaer
---

Today we released GitLab 7.2.2. This release addresses a security issue in the
`.deb` packages for GitLab 7.2.x. In addition, the 7.2.2 release includes a
[hooks migration script](#hooks-migration-script) that can be used to avoid
long downtime during the upgrade to 7.3 for GitLab installations with many (>
1000) repositories.

<!--more-->

## Insecure file permissions in omnibus-gitlab 7.2.x .deb packages

Due to a [regression in
omnibus-ruby](https://www.getchef.com/blog/2014/09/19/security-releases-omnibus-2-0-2-and-3-2-2-insecure-file-ownership-in-omnibus-built-debian-and-ubuntu-packages/),
the omnibus-gitlab `.deb` packages for GitLab 7.2.x Community Edition and
Enterprise Edition install files with insecure permissions. We advise all users
who installed omnibus-gitlab 7.2.x on Ubuntu 12.04, Ubuntu 14.04 or Debian 7 to
run the workaround commands below and upgrade to GitLab 7.2.2 as soon as
possible. Centos 6 and Centos 7 are not affected by this security
vulnerability.

### Affected versions

Omnibus-gitlab 7.2.0 CE (Community Edition), omnibus-gitlab 7.2.0 EE
(Enterprise Edition), omnibus-gitlab 7.2.1 CE, omnibus-gitlab 7.2.1 EE on
__Ubuntu 12.04__, __Ubuntu 14.04__ and __Debian 7__.

### Unaffected versions

Installations from source or with cookbook-gitlab and omnibus-gitlab packages
for Centos 6 and Centos 7 are not affected by this vulnerability.

### Impact

Omnibus-gitlab 7.2.0 and newer use omnibus-ruby 3.2.1. Due to a regression,
`.deb` packages (the format used by Debian and Ubuntu) built by omnibus-ruby
3.2.1 use insecure defaults when extracting the package contents causing the
files created on the target system to be owned by the numeric uid/gid of the
build user on the server the omnibus package was built on, instead of the files
being owned by 0/0 (root). This could (theoretically) be exploited by an
attacker with the ability to write arbitrary files on your system.

### Detection

You can check whether your omnibus-gitlab installation is affected with the
following command:

```
ls -lnd /opt/gitlab/embedded/service/gem/ruby/2.1.0/gems/rugged-0.21.0/ /opt/gitlab/embedded/bin/ruby
```

The output should look like:

```
-rwxr-xr-x 1 0 0 11991 Sep 18 15:02 /opt/gitlab/embedded/bin/ruby
drwxrwxr-x 5 0 0  4096 Sep 18 16:04 /opt/gitlab/embedded/service/gem/ruby/2.1.0/gems/rugged-0.21.0/
```

If you see `1001 1001` (or another non-zero number) instead of `0 0`, your
omnibus-gitlab installation is affected by this vulnerability.

### Mitigation

All users who installed omnibus-gitlab 7.2.0 or omnibus-gitlab 7.2.1 __on
Ubuntu or Debian__ should [upgrade to omnibus-gitlab 7.2.2](/downloads/) _and_
run the following two commands.

```
# Change ownership of all omnibus-gitlab packaged files to root:root
sudo sh -c 'dpkg-query -L gitlab | while read f; do chown root:root "$f"; done'

# Restore gitlab-specific permissions
sudo gitlab-ctl reconfigure
```

The two commands above can also be used as a workaround for users who cannot
upgrade immediately.

<a name="hooks-migration-script"></a>
## Hooks migration script

In GitLab 7.3 we are changing the git repository hooks that GitLab creates in
each Git repository to improve performance for Git pushes with many branches.
To achieve this change, the set of migrations for GitLab 7.3 contains one
migration that will loop through all Git repositories managed by GitLab and
update the `hooks` directory to become a symlink to gitlab-shell's `hooks`
directory. On GitLab servers with many repositories this may take a long time.

To avoid long downtime on very large GitLab installations, we came up with a
workaround to perform the hooks migration without downtime prior to upgrading
to GitLab 7.3. This workaround is optional; if you skip it your hooks will get
upgraded automatically when you upgrade to 7.3. _If your GitLab server has less
than 1000 repositories the steps below are not worth the hassle._

After upgrading to 7.2.2 (and on Ubuntu/Debian, running the two commands
above), you can perform the hooks migration online with the following rake
task.

```
# Omnibus installations: note that you will be prompted to do a cp command
sudo gitlab-rake gitlab:migrate:shell_hooks

# Installations from source / cookbook-gitlab:
cd /home/git/gitlab
sudo -u git -H bundle exec rake gitlab:migrate:shell_hooks RAILS_ENV=production
```

## Upgrading

Omnibus-gitlab packages for GitLab 7.2.2 are [now
available](https://about.gitlab.com/downloads/). To upgrade an installation
from source please use the
[upgrader](http://doc.gitlab.com/ce/update/upgrader.html) or the [patch update
guide](http://doc.gitlab.com/ce/update/patch_versions.html).

_Update 2014-09-22 13:57 CEST:_ added link to Chef blog post.
