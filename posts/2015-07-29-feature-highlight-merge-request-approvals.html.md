---
title: "Feature Highlight: Merge Request Approvals"
date: 2015-07-29
author: Job van der Voort
author_twitter: Jobvo
---

If you want keep code quality high, it is important that you use a code review
process. In GitLab, the best way to do this is by using Merge Requests.

We created merge requests so that only a person with the required
permission (developer or higher) can merge code into the target branch.
If you want more people to review code before it's merged, you can now do this
with Merge Request Approvals in [GitLab Enterprise Edition].

_Note: this is a follow up to our [previous feature highlight on approvals],
since we've added additional functionality in GitLab 7.13_

<!-- more -->

## How Approvals work

Approvals will block the merging of a merge request until the configured number
of approvals has been met. This allows you to force a certain amount of people
to check all the code that goes into important branches in your repository.

You can set the number of required approvals and you can assign specific approvers
that need to approve the merge request. If you set specific approvers, only
they will be able to approve the merge request. If you do not, anyone with
developer permission or higher will be able to approve the merge request.

![Approvers in a Merge Request](/images/7_13/approvers_mr.png)

### Assigning Approvers

It's possible to use a combination of specific and non-specific approvers,
for instance by setting the required number of approvers to `3` and only
`Jane` as an approver.

You can even set a higher number of approvers than required approvals, in which
case only a subset of the approvers needs to approve the merge request.
With one required approver and `Jane` and `John` set as approvers, either
`Jane` or `John` need to approve the merge request.

### Default Approvers

You can choose the approvers on merge request creation, but a default can be
set in the project settings. This prevents you from having to change the project
settings every time an important code reviewer is unavailable.

### Automatically Resetting Approvals

If you want to have all your approvals reset after a new push is made to the
merge request, you can configure this. This means that after each push that is
made, any previously done approvals are reset.

If this setting is turned off, approvals will persist, independent of pushes
to the merge request.

## Getting started with Approvals

To start using Approvals, visit the settings of your project and set the
required amount of approvers to a value of your choosing, higher than 1.

![Setting default suggested approvers for a project](/images/7_13/approvers_settings.png)

Here you are also able to set the default approvers, and whether you want to
reset the approvals on each push to the merge request.

## Future

We created the Merge Request Approvals on request of our customers. Our goal
is to add great features to GitLab that benefit everyone that uses them and
don't inconvenience anyone that doesn't.

We're thinking about more improvements to the Merge Request Approvals, the main
improvement being automatic suggestions for reviewers, based on the history of
the changed files in the merge request.
For instance, if Jane worked a lot on a certain class and you submit a change
to that class, Jane gets suggested to approve your merge request.

We're interested in hearing what you think about this feature and how we can
further improve it.

## Documentation

Find our [documentation on Merge Request Approvals].

[GitLab Enterprise Edition]: https://about.gitlab.com/pricing/
[previous feature highlight on approvals]: https://about.gitlab.com/2015/06/16/feature-highlight-approve-merge-request/
[documentation on Merge Request Approvals]: http://doc.gitlab.com/ee/workflow/merge_request_approvals.html
