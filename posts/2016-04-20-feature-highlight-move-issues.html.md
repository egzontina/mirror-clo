---
title: "Feature highlight: Move issues between projects"
date: 2016-04-20 12:00
comments: true
author: Grzegorz Bizon
author_twitter: GrzegorzBizon
image_title: /images/unsplash/truck.jpg
---


In [8.6][releasepost] we added a feature allowing you to move issues between projects.

If you work on multiple projects, it's possible to accidentally create an issue
in the wrong issue tracker. It's a seemingly simple mistake that is easy to miss.
Let's say you don't catch it right away and you do a decent amount of work
on the wrong project. Now, your "seemingly simple" mistake just became a bigger one.
We've all been in this position before. With our 8.6 release, we want to avoid the
panic that can come from creating an issue in the wrong project. Now, if you
create an issue in the wrong project, you can easily move it to the right one.

<!-- more -->

![Move issues between projects](/images/8_6/move-issue.png)

When you move the issue, the original issue will be copied, closed, and then referenced.
This process makes sure nothing is lost in the move.

Additionally, anyone who is subscribed to the issue will get a notification that the
issue was moved, with a link to the new location. This will, of course,
depend on your notification settings.

![Moved issue email](/images/blogimages/moved-issue-email.png)

It's a relatively simple feature, but it was
[tricky to implement][Merge request !2831].

## Behind the scenes: Moving issues between projects

At first, moving issue between projects seemed like an easy task. However,
we encountered a tricky problem with references in the issue description or
comments.

Suppose we have a project called Alice, and we created an issue inside it:

```markdown
Hey, this issue is related to #123 and the solution is implemented in !456.
```

Now let's suppose we want to move this issue to Bob. The reference #123 points
to an issue in Alice. Similarly, !456 points to a merge request in Alice as well.
If a user moves an issue to Bob, these references need to be updated so that they
continue pointing to Alice, not Bob. Otherwise, the resulting references would
link to the wrong project. The same goes for snippets, labels, commits, etc.

We knew that we needed to fix these references by using GitLab's Markdown
cross-project reference notation. However, at the time, not everything in GitLab
supported this notation. For example, labels (e.g. `~"My Label"`) could not be
shared across projects. We had to fix that, so we did via [Merge request !2996].


Another step was simply substituting `#123` with `gitlab-org/gitlab-ce#123`.
But it is possible you could have text like this:

```markdown
Hi, this is a duplicate of http://gitlab.com/gitlab-org/gitlab-ce/issues/123.
Also see documentation docs.gitlab.com/ce/some-page#123. Also take a look at this code:

    puts 'some code' #123 is a comment
```

So we know that this description holds a reference to issue 123 but we do not
know *where it is*, or how to substitute it in the right place. We needed to modify
the source text. However, changing the source text would interfere with Markdown.
To solve this, I tried some prototypes but couldn't find a better solution than
writing yet another parser for Markdown that would support the full Abstract
Syntax Tree of Markdown. This would add support for mutable nodes in a tree,
allowing us to modify text where needed.

However, once I started this work, I felt that this was a complicated solution so
I decided to look for a [boring solution][values]. I reached out to my fellow
developers on the team to find a better boring solution. After sometime,
[Kamil] helped me and we came with different solution.

We decided to use existing mechanisms to verify if we can substitute reference
in place it has been detected at. We knew that resulting HTML should not change,
so we could try substituting local reference with cross-project variation and
see if generated HTML is different than the original one. If it didn't change,
then substitution is valid.

Below you can find some implementation details of current solution.

1.  Match all local references to project, issue, merge request and all other
    entities using Regexp.

    References like `#123` for issue, `!456` for merge request are being
    matched.

1.  Substitute each subsequent match with fully-expanded cross-project
    reference.

    This substitues reference like `#123` with `gitlab-org/gitlab-ce#123`.

1.  For each substitution generate HTML twice, using a new content and using an
    old content.

    Because of the fact that cross-project reference, when used in a context
    of the project it refers to is rendered as a local reference, both resulting
    HTMLs should be the same.

1.  If resulting HTMLs are the same, we permanently alter original text to
    contain cross-project reference instead of local reference.

This solution is not the most optimal one because of performance reasons, but
it allowed us to ship this feature quickly and in the future we can improve it
by using Abstract Syntax Tree implementation for Markdown.

With this approach, we are also sure that modifications to issue/comments
content are correct and don't break your issue which can hold valuable
information.

[Kamil]: https://twitter.com/ayufanpl
[Merge request !2831]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2831
[values]: https://about.gitlab.com/handbook/#values
[releasepost]: https://about.gitlab.com/2016/03/22/gitlab-8-6-released/
[Merge request !2996]: https://gitlab.com/gitlab-org/gitlab-ce/merge_requests/2966
