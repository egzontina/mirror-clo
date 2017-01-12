---
title: Fast Search Using PostgreSQL Trigram Indexes
date: 2016-03-18 19:00:00 UTC
author: Yorick Peterse
author_twitter: yorickpeterse
---

GitLab 8.6 will ship with improved search performance for PostgreSQL thanks to
the use of trigram indexes. In this article we'll look at how these indexes work
and how they can be used to speed up queries using LIKE conditions.

<!--more-->

GitLab allows users to search for issues, comments, commits, code, merge
requests, and snippets. The traditional approach to developing a system for
searching data like this in an RDBMS is to simply use a LIKE condition. A LIKE
operates on a string that specifies what to search for and optional percentage
signs acting as wildcards. For example, to match all values starting with
"Alice" you'd use the string `'Alice%'`. If one wants to search all records in a
table (e.g. all users) they might write the following query:

    SELECT *
    FROM users
    WHERE name LIKE 'Alice%';

The wildcards used for a LIKE condition can appear anywhere (and optionally
multiple times) in the string, as such all these values are valid:

* `'Alice%'`
* `'%Alice'`
* `'%Alice%'`
* `'%Al%ice%'`

However, wildcards being allowed poses a problem: index usage. When a wildcard
appears somewhere at the end of a string both MySQL and PostgreSQL are able to
use any existing indexes. However, when a wildcard appears at the start of a
string things become problematic. To better understand the problem, imagine you
have the following list of names:

* Alice
* Bob
* Charlie
* Eve
* Emily

When searching for any name containing "li" the only solution is to iterate over
all values and check if each value contains the string "li". Because the value
can appear anywhere in the strings to search an index won't help as we'd still
have to compare every value one by one with no way of reducing the set of rows
to search through. This in turn can lead to very slow queries depending on the
amount of data to search through.

## Full Text Search

Since both MySQL and PostgreSQL provide full text searching capabilities one
solution would be to use this instead of a regular LIKE condition. Sadly both
implementations are not without their problems. Up until MySQL 5.6 full text
search only worked on MyISAM tables which in turn meant not being able to use
transactions. Both MySQL and PostgreSQL also use different syntax for searching
and require different steps to set things up. For example, MySQL uses the
following syntax:

    SELECT *
    FROM users
    WHERE MATCH (username) AGAINST ('yorick');

PostgreSQL uses the following instead:

    SELECT *
    FROM users
    WHERE to_tsvector('english', username) @@ to_tsquery('english', 'yorick');

The differences in syntax make the code more complex. On top of that
PostgreSQL's full text search works best when the text vectors are stored in
physical columns with an index. This in turn means having to adjust all your
queries to use these columns instead of the regular ones, resulting queries such
as:

    SELECT *
    FROM users
    WHERE username_tsvector @@ to_tsquery('english', 'yorick');

This assumes `username_tsvector` contains a text vector built from the data
stored in the `username` column. To further complicate matters you'd have to set
up a stored procedure and database trigger to keep these text vector columns in
sync with the ones containing the raw data.

Another problem with full text search is that words are broken up according to
the rules defined by the language of the text. For example, on PostgreSQL
converting "Yorick Peterse" to a text vector results in the values "peters" and
"yorick". This means that searching for "yorick" or "peterse" _will_ match the
data, but searching for "yor" _will not_. To showcase this we can run the
following query in PostgreSQL:

    SELECT 1
    WHERE to_tsvector('english', 'Yorick Peterse') @@ to_tsquery('english', 'peterse');

Here `to_tsvector()` creates a text vector with English as the language and
"Yorick Peterse" as the input. The `to_tsquery()` function in turn creates a
text search query with English as the language and "peterse" as the input.

Running this query will result in a single row being returned. On the other
hand, this will return no rows:

    SELECT 1
    WHERE to_tsvector('english', 'Yorick Peterse') @@ to_tsquery('english', 'yor');

This is problematic when you don't know exactly what you're looking for, for
example when you're looking for a person but only know part of their first name.

In short, full text search is only really an option if you only support
PostgreSQL or MySQL as supporting both leads to a lot of unwanted complexity.

## Trigram Indexes

While MySQL offers no further solutions (that I know of), PostgreSQL on the
other hand has some extra tricks up its sleeves: trigram indexes. Trigram
indexes work by breaking up text in [trigrams][trigrams]. Trigrams are basically
words broken up into sequences of 3 letters. For example, the trigram for
"alice" would be:

    {ali, lic, ice}

PostgreSQL supports trigram indexes and operations via the [pg_trgm][pg_trgm]
extension. This extension adds a few functions, operators, and support for
trigram indexes (using GIN or GiST indexes to be exact). To see what kind of
trigrams PostgreSQL can produce we can run the following query:

    select show_trgm('alice');

This will generate the trigrams for the string "alice", producing the following
output:

                show_trgm
    ---------------------------------
     {"  a"," al",ali,"ce ",ice,lic}

A big benefit of this extension is that these trigram indexes can be used by the
LIKE and ILIKE conditions without having to change your queries or setting up
complex full text search systems. There are 2 requirements for this to work:

1. The index created must be either a GIN or a GiST index, in case of GitLab we
   went with GIN indexes due to them leading to better query timings (at the
   cost of being larger and somewhat slower to build).
2. The index must have the appropriate [operator class][opclass] set.

In case of a GIN index the operator class we have to use is called
`gin_trgm_ops`. We can create the appropriate indexes using a query such as the
following:

    CREATE INDEX CONCURRENTLY index_issues_on_title_trigram
    ON issues
    USING gin (title gin_trgm_ops);

To showcase the impact these indexes have on performance let's use the following
query as an example:

    SELECT COUNT(*)
    FROM users
    WHERE username ILIKE '%yorick%';

This query counts the amount of users where the username contains the string
"yorick", regardless of the casing. Running this query on my local PostgreSQL
database takes around 160 milliseconds and produces the following query plan:

     Aggregate  (cost=8143.40..8143.41 rows=1 width=0) (actual time=157.981..157.982 rows=1 loops=1)
       ->  Index Only Scan using index_users_on_username on users  (cost=0.42..8143.34 rows=26 width=0) (actual time=155.153..157.974 rows=6 loops=1)
             Filter: (username ~~* '%yorick%'::text)
             Rows Removed by Filter: 257532
             Heap Fetches: 0
     Planning time: 0.143 ms
     Execution time: 158.008 ms

To speed this up we'll run the following to create an index:

    CREATE INDEX CONCURRENTLY index_users_on_username_trigram
    ON users
    USING gin (username gin_trgm_ops);

If we now re-run the query it takes only around 0.2 milliseconds and produces
the following query plan:

     Aggregate  (cost=152.41..152.42 rows=1 width=0) (actual time=0.128..0.128 rows=1 loops=1)
       ->  Bitmap Heap Scan on users  (cost=52.20..152.35 rows=26 width=0) (actual time=0.115..0.126 rows=6 loops=1)
             Recheck Cond: (username ~~* '%yorick%'::text)
             Heap Blocks: exact=6
             ->  Bitmap Index Scan on index_users_on_username_trigram  (cost=0.00..52.19 rows=26 width=0) (actual time=0.106..0.106 rows=6 loops=1)
                   Index Cond: (username ~~* '%yorick%'::text)
     Planning time: 0.366 ms
     Execution time: 0.167 ms

In other words, creating the trigram index results in the query being around
946 times faster.

## GitLab & Trigram Indexes

GitLab 8.6 will create trigram indexes for PostgreSQL users leading to vastly
improved search performance (though there's still some work to be done in the
future). To make this work (while still supporting MySQL) we did have to port
over some changes from an open Rails pull request to ensure the indexes were
dumped properly to `db/schema.rb`. These changes can be found in
[config/initializers/postgresql_opclasses_support.rb][opclass-support] and were
taken from [Rails pull request #19090][rails-pr-19090].

We also had to make some changes to ensure MySQL doesn't end up trying to create
these indexes when loading the schema definition into a database. For example,
`db/schema.rb` contains lines such as `add_index ..., using: :gin` and the
`using` option is passed straight to the underlying database. Since MySQL
doesn't support GIN indexes this would lead to database errors when trying to
load `db/schema.rb`. The code that makes this work can be found in
[config/initializers/mysql_ignore_postgresql_options.rb][mysql-ignore-pg].

Finally we made some small changes to the code to ensure queries automatically
use ILIKE on PostgreSQL instead of `lower(some_column)` as ILIKE performs quite
a bit better. On MySQL a regular LIKE is used as it's already case-insensitive.

All of the other details can be found in GitLab CE merge request ["Refactor
searching and use PostgreSQL trigram indexes for significantly improved
performance"][mr2987].

[trigrams]: https://en.wikipedia.org/wiki/Trigram
[pg_trgm]: http://www.postgresql.org/docs/current/static/pgtrgm.html
[opclass]: http://www.postgresql.org/docs/current/static/indexes-opclass.html
[mr2987]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2987
[opclass-support]: https://gitlab.com/gitlab-org/gitlab-ce/blob/0602091f0cdebbc3183732dee78c38f89b4b7d01/config/initializers/postgresql_opclasses_support.rb
[mysql-ignore-pg]: https://gitlab.com/gitlab-org/gitlab-ce/blob/0602091f0cdebbc3183732dee78c38f89b4b7d01/config/initializers/mysql_ignore_postgresql_options.rb
[rails-pr-19090]: https://github.com/rails/rails/pull/19090
