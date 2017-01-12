---
title: "8 Tips to help you work better with Git"
date: 2015-02-19
image_title: '/images/unsplash/leaves.jpeg'
categories:
author: Patricio Cano
author_twitter: suprnova32
---

Git is a very powerful version control system. It can be a little bit daunting to try to learn everything around it, so
most people just use the basic commands. We want to give you here some help with some tips you may or may not have heard.
Either way, these tips can make your workflow a little easier.

<!-- more -->

## Git aliases

One of the best ways to ease your daily workflow with Git is to create aliases for common commands you use every day. This
can save you some time in the terminal.

You can use the following commands to create aliases for the most used Git commands, `checkout`, `commit` and `branch`.

```
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.br branch
```

This way, instead of typing `git checkout master` you only need to type `git co master`.

You could also edit them or add more by modifying the `~/.gitconfig` file directly:

```
[alias]
    co = checkout
    ci = commit
    br = branch
```

## Stashing uncommitted changes

Let’s say we are working on a new feature, but there is an emergency and we need to fix to our project immediately.
We don’t want to commit an unfinished feature, and we also don’t want to lose our current changes.

The solution is to temporarily remove these changes with the git stash command:

```
$ git stash
```

The git stash command hides these changes, giving us a clean working directory. We’re now able to switch to a new
branch to make our important updates, without having to commit a meaningless snapshot just to save our current state.

Once you are done working on the fix and want to show your previous changes again, all you need to is run:

```
$ git stash pop
```

And your changes will be recovered. If you no longer need those changes and want to clear the stash stack you can do so
with:

```
$ git stash drop
```

## Compare commits from the command line

An easy and quick way to compare the differences between commits, or versions of the same file is to use the command
line. For this you can use the `git diff` command.

If you want to compare the same file between different commits, you do the following:

```
$ git diff $start_commit..$end_commit -- path/to/file
```

Anf if you want to compare the changes between two commits:

```
$ git diff $start_commit..$end_commit
```

These commands will open the diff view inside the terminal, but if you prefer to use a more visual tool to compare your
diffs, you can use `git difftool`. A really great diff viewer/editor is Meld.

To configure Meld:

```
$ git config --global diff.tool git-meld
```

Now to start viewing the diffs:

```
$ git difftool $start_commit..$end_commit -- path/to/file
# or
$ git difftool $start_commit..$end_commit
```


## Resetting files

Sometimes when you start modifying your code, you realize that the changes you did are not that good and would like to reset
your changes. Instead of clicking undo on everything you edited, you can reset your files to the HEAD of the branch:

```
$ git reset --hard HEAD
```

Or if you want to reset a single file:

```
$ git checkout HEAD -- path/to/file
```

Now, if you already committed your changes, but still want to revert back, you can use:

```
$ git reset --soft HEAD~1
```

## Use Git blame more efficiently

Git blame is a great tool for finding out who changed a line in a file, but there are ways you can use it more efficiently.
You can pass different flags, depending on what you want to show.

```
$ git blame -w  # ignores white space
$ git blame -M  # ignores moving text
$ git blame -C  # ignores moving text into other files
```

<hr/>


Now that you know some very useful tips about working with Git, let us give you some other tips on how to best use Git
within your workflow.

## Pull frequently

If you are using the [GitLab Workflow](https://about.gitlab.com/2014/09/29/gitlab-flow/), it means that you are working
on feature branches. Depending on how long your feature takes to implement, a lot of changes might have been made to the
master branch.

In order to avoid major conflicts at the end of the development of your feature, you should pull the changes from the
master branch to your branch often. This will allow you to resolve any possible conflicts as soon as possible and it will
make merging your branch to master easier.

## Commit often, but don't push every commit

Committing your changes often will keep your changes concise and make them easier to revert, if you were to need that. But
it is not necessary to push every single commit to the server, as it will appear in the activity feed and probably spam
your colleagues. Work on your changes until you are ready to push.

## Push when changes are tested

A nice sign that your changes are ready to push is when they have been tested and the tests are green. This usually also
means that this part of your feature is done and you can concentrate on the next part. Push your changes once this has been
done and let the CI server test them again.
