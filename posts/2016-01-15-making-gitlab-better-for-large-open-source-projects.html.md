---
title: "Making GitLab Better for Large Open Source Projects"
date: 2016-01-15
author: Job van der Voort
author_twitter: Jobvo
---

Dear open source maintainers,

We want GitLab to be the best place for any software project,
whether open source or not, whether big or small.

[The letter of GitHub's open source community](https://github.com/dear-github/dear-github/tree/2f45c3255a55c3ac111817840537151d96e1649e)
is clearly not addressed to us,
but we're thinking a lot about the issues that were mentioned in it.
We see many of these things happening and have been working on them for a long time,
not in the least because we develop on a [busy public issue tracker](https://gitlab.com/gitlab-org/gitlab-ce/issues) ourselves.

Here we would like to share our thoughts about these issues and
what we’re planning to do to make things better with GitLab.

<!-- more -->

## Major issues

> Issues are often filed missing crucial information like reproduction steps or version tested.
> We’d like issues to gain custom fields, along with a mechanism (such as a mandatory issue template,
> perhaps powered by a newissue.md in root as a likely-simple solution) for ensuring they are filled out in every issue.

In GitLab you can [set a template for an issue and for a merge request](https://gitlab.com/gitlab-org/gitlab-ee/blob/master/doc/customization/issue_and_merge_request_template.md).

We're also planning to add [multiple templates](https://gitlab.com/gitlab-org/gitlab-ee/issues/101),
that you can use depending on the reason for making an issue.

We're also [interested in exploring](https://gitlab.com/gitlab-org/gitlab-ce/issues/8988)
custom (required) fields.

Using a `new_issue.md` file for templates is a nice idea, that we're happy
to discuss [in this issue](https://gitlab.com/gitlab-org/gitlab-ce/issues/9088).

> Issues often accumulate content-less “+1” comments which serve only to spam the
> maintainers and any others subscribed to the issue.
> These +1s serve a valuable function in letting maintainers know how widespread an issue is,
> but their drawbacks are too great. We’d like issues to gain a first-class voting system,
> and for content-less comments like “+1” or “:+1:” or “me too” to trigger a warning
> and instructions on how to use the voting mechanism.

GitLab currently has a voting system that automatically transforms `+1` into
a vote. As we use GitLab ourselves for issue tracking _and_ feature voting,
this is something that has a high priority for us.

We've also planned [several improvements to votes](https://gitlab.com/gitlab-org/gitlab-ce/issues/3763)
and welcome more ideas and merge requests.

> Issues and pull requests are often created without any adherence to the
> CONTRIBUTING.md contribution guidelines, due to the inconspicuous nature of
> the “guidelines for contributing” link when creating an issue and the fact that
> it often contains a lot of information that isn’t relevant to opening issues
> (such as information about hacking on the project). Maintainers should be able
> to configure a file in the repo (interpreted as GFM) to be displayed at the top
> of the new issue / PR page instead of that link. Maintainers can choose to inline
> content there and / or link to other pages as appropriate.

Currently, we provide links to `CONTRIBUTING.md` whenever you create an
issue or merge request. At the moment you can also leverage the issue
template to point people to specific rules.

We're [interested in adding a custom contributing file on top of issues](https://gitlab.com/gitlab-org/gitlab-ce/issues/9083) in GitLab.

## Responses to specific suggestions

The original letter also included a long list of suggestions.
To see our response to every single point, please view
[this issue on GitLab.com](https://gitlab.com/gitlab-org/gitlab-ce/issues/8938).

One issue that was raised several times was the ability to not create
merge commits. In GitLab.com and EE you can, as an alternative to the merge commits,
[use fast-forward merges](http://doc.gitlab.com/ee/workflow/ff_merge.html)
or have [merge requests be automatically rebased](http://doc.gitlab.com/ee/workflow/rebase_before_merge.html).

## How we all build GitLab

GitLab is built in the open. Our decisions, doubts, and arguments about
changes to GitLab, new features, and everything else can all be found in our
repositories (mainly [GitLab CE](https://gitlab.com/gitlab-org/gitlab-ce/issues)
and [GitLab EE](https://gitlab.com/gitlab-org/gitlab-ee/issues)).

Everyone is free to comment, create new issues, vote on, and
[contribute to the development](http://contributors.gitlab.com/)
of GitLab. We have short- and long-term goals, all of which are visible on the
issues of the repositories and on the [direction page on the website](https://about.gitlab.com/direction/).

If you want to change something, create an issue or submit a merge request.
You can choose to implement something yourself, or ask someone else to do it.
Great ideas will always get the attention they need.
