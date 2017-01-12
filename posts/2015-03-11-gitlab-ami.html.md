---
title: "GitLab AMI"
date: 2015-03-11
author: Job van der Voort
author_twitter: Jobvo
image_title: '/images/stock/mac.jpg'
---

We're happy to announce that GitLab now has [Amazon Web Services Machines Images](https://about.gitlab.com/aws/)
(AMIs) available for GitLab CE. These are simple AMIs, that only require a
single command to bootstrap your GitLab instance on AWS.

<!-- more -->

To use the GitLab machine image, simply create an instance from the AMI
that you find [here](https://about.gitlab.com/aws/) and run:

```
sudo gitlab-ctl reconfigure
```

Your instance will run at your set hostname and you can immediately log in
and start using GitLab!

## Powered by an Omnibus Package

The AMI contains the exact same GitLab CE Omnibus package that is released.
This means that upgrading and maintenance is very easy.

This is actually how we run GitLab.com on AWS. See how we migrated [here](https://about.gitlab.com/2015/03/09/moving-all-your-data/).
