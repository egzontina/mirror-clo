---
title: "Note on license expiration in GitLab 7.10.5 EE"
date: 2015-06-04
author: Job van der Voort
author_twitter: Jobvo
---

If you're upgrading to GitLab Enterprise Edition 7.11, which introduces
licenses keys, you're probably planning to upgrade to 7.10.5 first.
This way you are able to [upload your license key in advance](https://about.gitlab.com/2015/05/27/gitlab-7-dot-10-dot-5-released/).

One of our customers notified us of a faulty description in the license
uploader in GitLab 7.10.5. Upon uploading, the license is checked properly,
however the text in the license view in the admin page in GitLab will show:

![Wrong text](/images/7_10_5/wrong.png)

While it should look like this:

![Correct text](/images/7_10_5/correct.png)

This only occurs in GitLab 7.10.5 and does not affect functionality.
The license information is correctly shown in GitLab 7.11 and up.

If you have any questions or comments do not hesitate to comment below
or contact support.
