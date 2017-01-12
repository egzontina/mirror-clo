---
title: "GitLab.com outage on 2015-09-01"
date: 2015-09-01
author: Jacob Vosmaer
author_twitter: jacobvosmaer
---

This morning GitLab.com was offline for one hour while we were
investigating what seemed to be a filesystem corruption issue.  With
this blog post we want to tell you more about what was going on and
what we discovered.

<!-- more -->

This morning around 7:00 UTC the NFS server that holds the Git
repositories hosted on GitLab.com became very slow. This made
GitLab.com also very slow. While investigating this issue on the
NFS server, we saw the following error messages in the output of
`dmesg`:

```
[870355.932072] EXT4-fs (dm-0): error count since last fsck: 2
[870355.932076] EXT4-fs (dm-0): initial error at time 1439995223: ext4_mb_generate_buddy:756
[870355.932079] EXT4-fs (dm-0): last error at time 1439995223: ext4_mb_generate_buddy:756
[956863.452065] EXT4-fs (dm-0): error count since last fsck: 2
[956863.452070] EXT4-fs (dm-0): initial error at time 1439995223: ext4_mb_generate_buddy:756
[956863.452072] EXT4-fs (dm-0): last error at time 1439995223: ext4_mb_generate_buddy:756
[1043370.972077] EXT4-fs (dm-0): error count since last fsck: 2
[1043370.972081] EXT4-fs (dm-0): initial error at time 1439995223: ext4_mb_generate_buddy:756
[1043370.972084] EXT4-fs (dm-0): last error at time 1439995223: ext4_mb_generate_buddy:756
[1129878.492074] EXT4-fs (dm-0): error count since last fsck: 2
[1129878.492108] EXT4-fs (dm-0): initial error at time 1439995223: ext4_mb_generate_buddy:756
[1129878.492111] EXT4-fs (dm-0): last error at time 1439995223: ext4_mb_generate_buddy:756
[1216386.012085] EXT4-fs (dm-0): error count since last fsck: 2
[1216386.012135] EXT4-fs (dm-0): initial error at time 1439995223: ext4_mb_generate_buddy:756
[1216386.012139] EXT4-fs (dm-0): last error at time 1439995223: ext4_mb_generate_buddy:756
[1302893.532065] EXT4-fs (dm-0): error count since last fsck: 2
```

This made us worry that something was really wrong with the filesystem
that holds all GitLab.com data, and we decided that we should take
the filesystem (and hence GitLab.com) offline to run `fsck` on it.
This was at [7:54
UTC](https://twitter.com/gitlabstatus/status/638621030060290048).
With fsck under way we started thinking about other, faster ways
to bring GitLab.com back online. We considered restoring a backup,
but that would have set back the clock 6-7 hours (we make backups
once a day) and because the backups use block device snapshots,
there was a good chance that whatever file system corruption we
were seeing would be present in the backup too.

At some point we went back to the dmesg output to try and better
understand the errors. What was it really saying? What were those
time stamps at the start of each line? It turns out dmesg can show
human-readable timestamps if you pass the `-T` option. Now things
suddenly looked very different:

```
[Wed Aug 26 14:52:55 2015] EXT4-fs (dm-0): error count since last fsck: 2
[Wed Aug 26 14:52:55 2015] EXT4-fs (dm-0): initial error at time 1439995223: ext4_mb_generate_buddy:756
[Wed Aug 26 14:52:55 2015] EXT4-fs (dm-0): last error at time 1439995223: ext4_mb_generate_buddy:756
[Thu Aug 27 14:54:43 2015] EXT4-fs (dm-0): error count since last fsck: 2
[Thu Aug 27 14:54:43 2015] EXT4-fs (dm-0): initial error at time 1439995223: ext4_mb_generate_buddy:756
[Thu Aug 27 14:54:43 2015] EXT4-fs (dm-0): last error at time 1439995223: ext4_mb_generate_buddy:756
[Fri Aug 28 14:56:31 2015] EXT4-fs (dm-0): error count since last fsck: 2
[Fri Aug 28 14:56:31 2015] EXT4-fs (dm-0): initial error at time 1439995223: ext4_mb_generate_buddy:756
[Fri Aug 28 14:56:31 2015] EXT4-fs (dm-0): last error at time 1439995223: ext4_mb_generate_buddy:756
[Sat Aug 29 14:58:18 2015] EXT4-fs (dm-0): error count since last fsck: 2
[Sat Aug 29 14:58:18 2015] EXT4-fs (dm-0): initial error at time 1439995223: ext4_mb_generate_buddy:756
[Sat Aug 29 14:58:18 2015] EXT4-fs (dm-0): last error at time 1439995223: ext4_mb_generate_buddy:756
[Sun Aug 30 15:00:06 2015] EXT4-fs (dm-0): error count since last fsck: 2
[Sun Aug 30 15:00:06 2015] EXT4-fs (dm-0): initial error at time 1439995223: ext4_mb_generate_buddy:756
[Sun Aug 30 15:00:06 2015] EXT4-fs (dm-0): last error at time 1439995223: ext4_mb_generate_buddy:756
[Mon Aug 31 15:01:53 2015] EXT4-fs (dm-0): error count since last fsck: 2
[Mon Aug 31 15:01:53 2015] EXT4-fs (dm-0): initial error at time 1439995223: ext4_mb_generate_buddy:756
[Mon Aug 31 15:01:53 2015] EXT4-fs (dm-0): last error at time 1439995223: ext4_mb_generate_buddy:756
[Tue Sep  1 07:53:11 2015] nfsd: last server has exited, flushing export cache
```

What we saw now was that we were getting the same error once a day,
going back to the first day we mounted this filesystem on the server
(after our migration from Germany to the US). The scary error message
that made us assume the worst and led us to take emergency measures
(taking GitLab.com offline for fsck) turned out to have been repeating
for weeks, like clockwork, around 15:00 UTC every day. Moreover,
we saw no new errors appearing, just a regular repeat of the same
error. Although the message signals a problem that we should not
ignore, looking at it and understanding the pattern it no longer
looked like a likely cause for the load issues (NFFS server trouble)
that started all of this.

At this point we decided that the best course of action was to abort
the filesystem check and bring GitLab.com back online. This was
around [8:52
UTC](https://twitter.com/gitlabstatus/status/638635500274909184).
After seeing more 502 errors than usual for a few minutes, GitLab.com
was operating normally again.

## Next steps

We are in the process of moving all GitLab.com data off of the ext4
filesystem that scared us with its two errors. This is because three
years after we created it, we are outgrowing its built-in maximum
size of 16 TB. We will run `git fsck` (Git's built-in consistency
check) on each repository once we are on the new filesystem.

We are still in the dark about the cause of the NFS slowdowns. We
see no spikes of any kind of web requests around the slowdowns. The
backend server only shows the ext4 errors mentioned above, which
do not coincide with the NFS trouble, and no NFS error messages.
The NFS clients show kernel messages about processes hanging during
filesystem operations, which really only tells us that here is an
NFS problem.

Last week, on 2015-08-27, we had a similar problem on GitLab.com,
which we responded to by doubling the number of servers that handle
user traffic. That helped that time but it does not seem to have helped with this problem.

We will keep looking for potential causes and keep monitoring the
situation.

## Lessons

As an operations team we still struggle with giving enough status
updates during a crisis. All people who were on this problem were
focused on the GitLab.com servers, and nobody was talking to the
GitLab.com users, leading to an hour of radio silence from
`@gitlabstatus` during the incident. We need to improve on this,
but like debugging NFS server meltdowns, it is a hard problem.