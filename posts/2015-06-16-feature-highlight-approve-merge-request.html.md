---
title: "Feature Highlight: Approve Merge Request"
date: 2015-06-16
author: Dmitriy Zaporozhets
author_twitter: dzaporozhets
---

With less than a week until GitLab 7.12, we've got a nice preview for you today:
Merge Request Approvals in GitLab EE.

Usually you accept a merge request the moment it is ready and reviewed.
But in some cases you want to make sure that every merge request is reviewed
and signed off by several people before merging it.
With GitLab Enterprise Edition 7.12, you can enforce such a workflow
that requires multiple reviewers with the new Merge Request Approval feature.

![approve_merge_request](/images/feature_approval/mr.png)

<!-- more -->

To enable approvals, go to project settings page and set the
"Approvals required" field to a numeric value. For example, if you set it to `3`
each merge request has to receive 3 approvals from different people
before it can be merged through the user interface.

![approve_setting](/images/feature_approval/settings.png)

After setting the approval, you will see an `Approve` button on merge requests,
rather than an `Accept` button. Once the merge request has enough approvals,
you will be able to merge it as usual.

We'd love to hear what you think of this new feature in the comments below.
