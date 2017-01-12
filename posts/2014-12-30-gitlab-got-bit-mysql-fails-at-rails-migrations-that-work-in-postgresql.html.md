---
title: "GitLab got bit: MySQL fails at Rails migrations that work in PostgreSQL"
date: 2014-12-30
author: Job van der Voort
---

One day after releasing GitLab 7.6 we had to release a patch. This is how we
got bit by a failing migration and why it was our own fault.

<!-- more -->

## What happened

GitLab supports two databases: MySQL and PostgreSQL.

To update our database models for identities in GitLab, we wanted to remove two columns from the `users` table: `extern_uid` and `provider`. These had a composite index, so that uniqueness was checked for any combination of `extern_uid + provider`.

```
add_index :users, [:extern_uid, :provider]
```

So to remove the columns, we wrote a simple migration:

```
def up
  remove_column :users, :extern_uid
  remove_column :users, :provider
end
```

Run the migration on PostgreSQL and it works without a hitch. Try to run it on MySQL and:

```
Mysql2::Error: Duplicate entry 'example' for key 'index_users_on_extern_uid_and_provider': ALTER TABLE `users` DROP `extern_uid`
```

It seems that when removing the `extern_uid` column, MySQL decided to rebuild the index using only the `provider` column, creating duplicate indices (which is not allowed).


## How we fixed it

To fix this, all we had to do is check whether the index exists and remove it if it does.

```
def up
  if index_exists?(:users, [:extern_uid, :provider])
    remove_index :users, [:extern_uid, :provider]
  end

  remove_column :users, :extern_uid
  remove_column :users, :provider
end
```

We quickly released [a new GitLab version](https://about.gitlab.com/2014/12/23/gitlab-7-6-1-released/)
that included the new migration.


## Why we'll _probably_ not repeat this mistake

So how did we miss such a simple mistake? GitLab has a pretty hefty test-suite that tests almost every line of code. On top of that, we do [QA testing](http://doc.gitlab.com/ee/release/monthly.html#workdays-before-release---preparation) on every release.

Turns out, we tested the migrations on an empty database: there were simply no duplicate indices to run into.

For future releases, we make sure that upgrades are tested on a pre-seeded database, and recommend
that migrations [do only one thing](https://gitlab.com/gitlab-org/gitlab-ce/commit/c5a1b808393d5b3769db0d65214df1645b69f6bf).

Simple mistake, simple fix. The trick is in trying to not repeat it.
