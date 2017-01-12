---
title: "Keeping your code protected"
date: 2014-11-26
categories:
author: Job van der Voort
---

Git is very easy to use and abuse.
A single `git push --force` command can easily ruin the day for a lot of people:

> As a result, these [186 Jenkins'] repositories have their branch heads rewinded to point to older commits, and in effect the newer commits were misplaced after the bad git-push.

On November 10, 2013, a Jenkins developer had [accidentally forced pushed](http://jenkins-ci.org/content/summary-report-git-repository-disruption-incident-nov-10th) to 186 repositories,
bringing them back two months in time.

The power that Git gives you to change history is great when you're working alone,
but potentially disrupting if you're working with others, as shown by a poor Jenkins developer.
When you're working with others, not only do you not want to allow `git push --force`,
but before anything is committed to the main repository or branch, the **code should be reviewed**.

At GitLab we believe that by preventing force pushes and by stimulating code review practices,
mistakes can be easily avoided and code quality will improve.
To make it easier to work together with code and Git we have created a surprisingly simple permission system,
built on top of an elegant authorization method.

<!--more-->

## Read, Write

Permission in GitLab are fundamentally defined around the idea of having read or write permission to the repository and branches.
Not only is this an easy-to-grasp concept, it doesn't add any unnecessary complexity to permission management.
By naming our permissions after their role within a project, it immediately becomes clear what each permission is intended for. **In GitLab, developers are called _Developer_**.


In our experience, this covers almost all cases and can be fitted to any organisation easily.

- Guest     - No access to code
- Reporter  - Read the repository
- Developer - Read/Write to the repository
- Master    - Read/Write to the repository + partial administrative capabilities
- Owner     - Read/Write to the repository + full administrative capabilities

The permissions are named to reflect their purpose. A user with the lowest private permission _Guest_
is only able to make use of the issues in a project and does not have read access to the code;
a guest of the project.

The _Reporter_ permission has the same abilities, but also has read access to the code,
meaning they can fork the project.
This is ideal for those that you do not want to be pushing to your repository,
but still want to give access to the code and give the option to fork off.

As the name implies, developers on a project should get the role _Developer_.
Any developer has write permission to the repository, meaning they can branch off,
work in and push their own branch back to the repository.

By defining permission on a read/write basis with clear names,
it quickly becomes clear which permission level should be used to secure a project.
However, they do not solve the issues with modifying history,
nor do they help with collaboration: anyone can (force) push to any branch (such as the master branch).

## Protecting your code


To stop people from messing with history or pushing code without review, we've created **protected branches**. A protected branch does three simple things:

- it prevents pushes from everybody except users with Master permission
- it prevents _anyone_ from force pushing to the branch
- it prevents _anyone_ from deleting the branch

You can make any branch a protected branch. We make the master branch a protected branch by default, but you can turn that off.

[![protected branches in GitLab](/images/protected_branches.png)](/images/protected_branches.png) ***We use protected branches on the [GitLab repository](https://gitlab.com/gitlab-org/gitlab-ce) to protect our release branches***

Now, if you want to contribute code to a protected branch as a developer, you can simply push your feature branch and **create a merge request** towards the protected branch. History is protected and the code gets reviewed before it's merged.

Note that even _Master_ is not able to force push to or delete a protected branch. We believe in a simple solution:

> Do not let anyone change the history of a shared branch. Revert changes in the present.

You can easily add a commit on top of history to revert earlier changes.
This is much easier to work with than changes in history on top of which people already committed.
In addition, you probably do not want to delete such an important branch, hence the inability to remove it.


## How we define permissions

By basing permissions on simple principles and adding protected branches,
GitLab allows you to set up any type of workflow, while protecting your code from easily made mistakes.
Underlying this elegant scheme is a surprisingly simple authorization gem,
[Six](http://randx.github.io/six/).

In a single class `Ability`, we have defined a number of class methods to set the permissions.
For instance, for _Developer_:

```
# app/models/ability.rb:139
def project_dev_rules
  project_report_rules + [
    :write_merge_request,
    :write_wiki,
    :modify_issue,
    :admin_issue,
    :admin_label,
    :push_code
  ]
end
```
Six has defined an `allowed?` method that check whether a permission exists for a certain object,
based on the abilities that you've defined for that class (such as above for _Developer_).
To make use of a similar syntax as the often-used [Cancan](https://github.com/ryanb/cancan) authorization gem, you can define a similar method with Six:

```
# app/models/user.rb:351
def can?(object, action, subject)
  abilities.allowed?(object, action, subject)
end
```

Then all we have to do is check the permission wherever we need it.
For instance to check whether someone is allowed to destroy a snippet:

```
def destroy
  return access_denied! unless can?(current_user, :admin_personal_snippet, @snippet)
  @snippet.destroy
  redirect_to snippets_path
end
```

By using the plain-ruby approach of [Six](http://randx.github.io/six/) you get a very flexible
and expendable authorization solution.
In GitLab we leverage this to create easy to understand permissions
that reflect how most organisations use GitLab.

## About GitLab

Interested in trying GitLab's protected branches?
You can try GitLab by [downloading](https://about.gitlab.com/downloads/) the Community Edition and installing it on your own server or by signing up to our free, unlimited GitLab instance [GitLab.com](https://gitlab.com/users/sign_up).

For support, deep LDAP integration, git hooks, Jenkins integration and more enterprise features, check out [GitLab Enterprise Edition](https://about.gitlab.com/features/#enterprise).

For more on Git workflows, read our article on [GitLab Flow](https://about.gitlab.com/2014/09/29/gitlab-flow/).
