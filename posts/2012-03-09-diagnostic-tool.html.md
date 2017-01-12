--- 
title: Diagnostic tool
wordpress_id: 254
wordpress_url: http://blog.gitlabhq.com/?p=254
date: 2012-03-09 18:52:26 +00:00
community: true
---
We pushed to master new support util.
If you have some troubles with gitlab installation - try diagnostic tool.

<code>
bundle exec rake gitlab_status

Starting diagnostic
config/database.yml............exists
config/gitlab.yml............exists
/home/git/repositories/............exists
/home/git/repositories/ is writable?............YES
remote: Counting objects: 603, done.
remote: Compressing objects: 100% (466/466), done.
remote: Total 603 (delta 174), reused 0 (delta 0)
Receiving objects: 100% (603/603), 53.29 KiB, done.
Resolving deltas: 100% (174/174), done.
Can clone gitolite-admin?............YES
UMASK for .gitolite.rc is 0007? ............YES
</code>
