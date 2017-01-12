---
title: "GitLab + Tower = A Most Efficient Setup"
date: 2015-11-10
author: Tobias Günther
author_twitter: gittower
---
*This is a guest post by Tobias Günther, founder at Tower.*

GitLab and [Tower](http://www.git-tower.com), the popular Git client, have more in common than just "Git". They share the same goal: to make working with code easier. And just recently, with the release of Tower 2.3, they work together more seamlessly than ever.  

You would think that cloning a remote repository was a simple process. And yet it can be quite a drag: You have to find the repository you want to clone, get hold of its URL, remember your authentication credentials (and method!) and fumble them onto the keyboard...  

Solving such minor and major annoyances around Git has always been our motivation for creating Tower - a GUI client for Git that's now used by over 50,000 customers like Apple, Google, and Twitter.  

Since our recent update to version 2.3, Tower makes working with GitLab even easier. You can access your repositories right from within Tower and __clone them with just a single click__:  

![One-Click Cloning](/images/tower_2_3/clone-repositories.jpg)  

Long gone are the days of wrestling with usernames, passwords, tokens, or URLs. Even __creating new repositories__ in your account can be done via Tower. Cloning and managing repositories has become quite a bit easier.  

Let's look at some other pain points that developers face day after day.  

<!--more-->

## Undoing Mistakes

One reason why I love Git is that I can __undo almost anything__. However, actually _remembering_ all the different ways, commands, and parameters to achieve this tends to make my head spin.  

That's when I love to have Tower open: the GUI guides me so I can _easily_ fix my last commit, restore any historic version, revert a certain commit's effects, or discard local changes in my working copy. It's great to know that [I can't mess up](http://www.git-tower.com/learn/git/ebook/mac/advanced-topics/undoing-things).  


## Dealing with Merge Conflicts

Admitting this one is a bit embarrassing: I had always been a bit of a coward when it came to merge conflicts. I had a hard time understanding what had happened - and an even harder time knowing what my options were. We've managed to find a __visual way__ of presenting conflicts in Tower, which helps a lot in __understanding__ the scenario.  

I can clearly see which files clashed, how exactly they looked, who worked on them, and which commit introduced the changes. And, with this knowledge, I can __decide what the solution should look like__ - simply by clicking the files I want in the final resolution.  

![Visual Merge Conflict Resolution](/images/tower_2_3/visual-merge-conflict-wizard.gif)  


## Optimizing Your Workflows

In my opinion, a graphical user interface has to provide some real advantages. Just a handful of pretty colors won't cut it.  

A Git example is that I don't want to check for new changes manually all the time. That's why Tower automatically and regularly performs a "Fetch" operation in the background for me. Thereby, __I know when something new is available__ on my GitLab remote repo.  

Also, tapping the full potential of a modern environment like Mac OS X means (to me) that I can use __drag & drop__ for many actions. From creating and merging branches, to cherry-picking commits or applying even parts of a Stash.  

![Drag and Drop](/images/tower_2_3/drag-drop.gif)  

Other things, like finding and opening any project, has to be a matter of seconds. Tower has a new "Open Quickly" dialog that lets me type just a few characters from the project's name to open what I was looking for.  

![Quick Open](/images/tower_2_3/open-quickly.gif)  

Lastly, Tower's "Auto Stash" feature is a perfect example of the app's philosophy - to take Git to the next level: __Tower automatically saves your current changes to the Stash__ when you're switching branches, pulling, or rebasing. Actions like these are best performed with a clean working copy - and Tower saves you the hassle of remembering and doing it.  

Feel free to [give Tower a try](http://www.git-tower.com) and see how it works with your GitLab account. You can download and test it 30 days for free.  

P.S.: I'm curious to know what _you_ are struggling with in Git and version control. Let me know in the comments!