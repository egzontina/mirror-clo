---
title: "Feature Highlight: Todos"
date: 2016-03-02
categories:
author: Douglas Alexandre
author_twitter: dbalexandre
image_title: '/images/unsplash/taking-notes.jpg'
---

In this blog post I'll guide you through the "Todos" feature we introduced in
[GitLab 8.5](https://about.gitlab.com/2016/02/22/gitlab-8-5-released/)
and also tell you how this feature came to life.
We'll also talk about how you can contribute to GitLab.

<!-- more -->

### First let’s look at this feature

When you log into GitLab, you'll want to see where you should spend your time,
where your team members need help, where you need to take some action, or what
you need to keep an eye on. All without the mess of a huge pile of e-mail
notifications.

When an issue or merge request is assigned to you, or when you are `@mentioned`
in a comment, this triggers a notification and you may get an e-mail, depending
on your notification settings. Starting from GitLab 8.5, these actions will
also add a notice in your Todos list, which you can access by clicking the
round gray icon next to the search bar in the upper right corner.

![Todos screenshot showing a list of items to check on](/images/blogimages/todos-screenshot.jpg)

You can then respond to the todo by performing an action to the corresponding
issue or merge request. This action can include changing the milestone, adding
a label, commenting on the issue and pretty much everything that adds extra
information to the issue/merge request.

In case where you think no action is needed, you can manually mark the todo as
**Done** and it will disappear from your Todos list.

In order for a todo to be marked as done, the action must be coming from you.
So, if you close/merge the related issue or merge request yourself, and you had
a todo for that, it will automatically get marked as done. On the other hand,if
someone else closes, merges or takes action on the issue or merge request, your
todo will remain pending. This makes sense because you may need to give
attention to an issue even if it has been resolved.

Another thing is that you won't have a gazillion Todos about the same issue or
merge request. There is just one todo per issue or merge request, you won’t be
annoyed repeatedly.

Next, let’s see how this feature came to life.

### How we developed this feature

It was just a few weeks before the 8.5 release when
[Dmitry](https://twitter.com/dzaporozhets) asked me to work on this feature.
In fact, that was a lot of work to be done in such a short time and I actually
delivered this task on the last release candidate before our release day.
As it turned out, people were quite surprised and happy to have this feature in
8.5.

There had been a long discussion about this feature, but no one had touched it
yet. The original proposal was very complicated, there were a lot of comments
on the issue too, with a more active discussion in the last two months.

Finally, after considering all the options,
[Dmitry commented on the issue][comment] and greatly simplified it.

I was excited about taking on the challenge. Not only because I knew it would
be an important feature, but it would also be a feature that most people will
use every day. This is the second major feature I've worked on since I started
at GitLab in December. Previously, I had worked on the GitHub import project
which came out in GitLab 8.4.

I needed to learn quite a lot of the GitLab codebase in order to create this
feature. And then, while I was reading the code, I was surprised to discover it
was going to be much easier than I thought. My epiphany was that we already had
the Activity feed system in place which I could reuse. As it turned out, it was
going to be very easy to implement this feature.

At the beginning, I spent the first week reading the code, understanding how
the system worked, discovering the points that we needed to trigger a todo. I
wrote some guidelines about what I needed to achieve and then I started writing
the actual code by the end of the week. Yep, most of the coding was done in one
week.

At first, I needed to investigate how the Activity feed system works.

![Screenshot of activity feed](/images/blogimages/activity-feed-screenshot.jpg)

Then, I plugged in another service to trigger the todo when an issue or merge
request is assigned to someone, or when someone is `@mentioned` in a comment or
the issue description. After this, I just needed to make sure that when someone
completed whatever they thought is needed on the issue or merge request, the
todo will be marked as **Done**.

Depending on the action that someone made on the issue or merge request, we
need to know exactly what attributes were changed. This is specially important
to know when Todos are automatically marked as **Done**.

To know what changed inside a issue or merge request, we used the
[Rails ActiveModel::Dirty API][dirty] that allows us to quick track what
attributes on a model have changed, even after the model was saved.

The `ActiveModel::Dirty` works very well, except that it doesn't track changes
on associations. So how we determine what changed inside the association? For
example, how to check if a label was added, or removed from an issue or merge
request? To accomplish this, we came with a boring solution, where we receive
the old items of the association through a parameter, and compare it with
the current association to check if something has changed.

The method that checks if at least one valid attribute has changed, is the
following:

```ruby
def has_changes?(issuable, options = {})
  valid_attrs = [:title, :description, :assignee_id, :milestone_id, :target_branch]

  attrs_changed = valid_attrs.any? do |attr|
    issuable.previous_changes.include?(attr.to_s)
  end

  old_labels = options[:old_labels]
  labels_changed = old_labels && issuable.labels != old_labels

  attrs_changed || labels_changed
end
```

A quick note about this code snippet is that it will run _after_ the model was
saved, so `previous_changes` is the method that we need to call, and it returns
a hash with the attributes that were changed before the model was saved.

We can see on the following snippet that other GitLab features, like
the system note and the notification service, also use this API to trigger an
action after certain attributes have changed:

```ruby
if issue.previous_changes.include?('assignee_id')
  create_assignee_note(issue)
  notification_service.reassigned_issue(issue, current_user)
  todo_service.reassigned_issue(issue, current_user)
end
```

To get an idea about the points that trigger an action related to Todos,
you can take a look at the source code of the [TodoService] class, that
describes the expected behavior for each of these points.

My colleague, [Douwe](https://twitter.com/DouweM), guided me through some of
these edge cases and helped me a lot with daily code reviews. Together we
considered the aspects of the functionality. I had to make many changes during
the review period, but that worked out well in the end.

Some people asked for changes which we thought didn't fit for what we were
trying to achieve. There was for example a request to be notified of Todos on
commits. We ultimately decided against this request since there are no clear
actions to take on a commit, except for replying to a comment. Most of the time
you’re actually working on an issue or a merge request, this is where the action
happens.

### About that name

There was a long discussion about naming the feature. In the beginning this
feature was called 'Notification System'. Then 'Action Center'. Then 'Todos'.
Then 'Tasks', and finally 'Task Queue' was chosen.

But Douwe and Sytse discussed the naming for the umpteenth time, and concluded
that 'Todos' would be the best name since 'Tasks' is already used (by us and
GitHub) for the Markdown checklist.

Todo makes more sense to me than a Task, you just need to take a look at it.
Tasks are obligations. A Todo is just a reminder, and as such, maybe it is
relevant for you and you'll take a look or maybe you'll just mark it as done.

### Conclusion

I'm really happy to have worked on a feature that people will use every day!
It's a simple feature and even though we've only been using it a few days,
we can't imagine how we managed to work without it.

This Tweet from a user pretty much sums it up.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">.<a href="https://twitter.com/gitlab">@gitlab</a>&#39;s new ToDos feature is simply amazing. Simple feature but something you cannot live without once you tried it.</p>&mdash; Tero Tasanen (@ttasanen) <a href="https://twitter.com/ttasanen/status/702249244950974464">February 23, 2016</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

For more information you can [read our documentation][doc].

---

Hopefully in this post you've also gotten a peek at the underlying systems in GitLab.
It if has inspired you to contribute to GitLab, check out our [Contributing guide][contributing].
Issues marked ["up for grabs"][up for grabs] will be of reasonable size and
challenge, for anyone to start contributing to GitLab.
The [Merge Request Guidelines][merge request] explain how to make a merge request
and what that process will be like.

[contributing]: https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CONTRIBUTING.md
[up for grabs]: https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CONTRIBUTING.md#i-want-to-contribute
[merge request]: https://gitlab.com/gitlab-org/gitlab-ce/blob/master/CONTRIBUTING.md#merge-requests
[comment]: https://gitlab.com/gitlab-org/gitlab-ce/issues/2425#note_3116626
[dirty]: http://api.rubyonrails.org/classes/ActiveModel/Dirty.html
[todoservice]: https://gitlab.com/gitlab-org/gitlab-ce/blob/8-5-stable/app/services/todo_service.rb
[doc]: http://doc.gitlab.com/ce/workflow/todos.html
