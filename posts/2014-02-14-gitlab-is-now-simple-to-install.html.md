---
title: GitLab is now simple to install
date: February 14, 2014
---

GitLab is the most fully featured open source application to manage git repositories.
However, historically it was not easy to install and update GitLab.
Installing it required copy-pasting commands from a long guide.
The guide [actually worked](https://twitter.com/robinvdvleuten/status/424163226532986880) but it was 10 pages long.
In spite of this GitLab has become the most popular solution for on premise installations with 50,000 organizations using it.
To grow even faster we needed to simplify the update and installations processes.
So in GitLab 6.4 we made sure that [upgrading is now only a single command](/2013/12/21/gitlab-ce-6-dot-4-released).
Today we can announce that installing GitLab is also greatly simplified.

You now have three new options to install GitLab: an official GitLab Chef cookbook, GitLab Packer virtual machines and GitLab Omnibus packages.

The [official GitLab Chef cookbook](https://gitlab.com/gitlab-org/cookbook-gitlab/blob/master/README.md) is the most flexible option.
It supports both development and production environments and both Ubuntu and RHEL/CentOS operating systems.
You can install it with Chef Solo, a Chef server or with Vagrant.
It supports MySQL and PostgreSQL databases, both in the same server as external ones.
The cookbook is [well tested](https://gitlab.com/gitlab-org/cookbook-gitlab/tree/master/spec) with [ChefSpec](https://github.com/sethvargo/chefspec).
For cloud fans there even is [a version that runs on AWS Opsworks](https://gitlab.com/gitlab-com/cookbook-gitlab-opsworks/blob/master/README.md).

If you want to quickly spin up a production GitLab server you can also use a virtual machine image with GitLab preinstalled.
The [downloads page](https://www.gitlab.com/downloads/) already has an Ubuntu 12.04 image and CentOS 6.5 will come soon.
These are made with [Packer](http://www.packer.io/) and [the source code to create your versions](https://gitlab.com/gitlab-org/gitlab-packer/blob/master/README.md) is available.
Example configurations for Digital Ocean and AWS are included. These images are created with the official Chef cookbook mentioned earlier.

Last but not least are the two GitLab Omnibus packages.
A deb package for Ubuntu 12.04 LTS and a RPM package for CentOS 6 can be found on the [downloads page](https://www.gitlab.com/downloads/).
These are packages of the GitLab 6.6.0.pre and should not be used on production machines.
When GitLab 6.6 is stable we will update the packages and link them in the GitLab readme.
Even when stable these packages currently support a reduced selection of GitLab's normal features.
It is not yet possible to create/restore application backups or to use HTTPS, for instance.
But it is a start and we look forward to improving them together with the rest of the GitLab community.
Creating these package has been our dream for a long time.
GitLab has a lot of dependencies which means that native packages would require packaging hundreds of gems.
To solve this we used [omnibus-ruby](https://github.com/opscode/omnibus-ruby) that Chef Inc. uses to package Chef and Chef Server.
Based on [omnibus-chef-server](https://github.com/opscode/omnibus-chef-server) we made [omnibus-gitlab](https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/README.md) that you can use to create your own package.
So now you can finally install GitLab with:

```
apt-get install -y openssh-server postfix
dpkg -i gitlab_6.6.0-pre1.omnibus.2-1.ubuntu.12.04_amd64.deb
gitlab-ctl reconfigure
```

Like any active project there are still many way to improve the [GitLab Chef cookbook](https://gitlab.com/gitlab-org/cookbook-gitlab/issues), the [GitLab Packer virtual machines](https://gitlab.com/gitlab-org/gitlab-packer/issues) and [GitLab Omnibus packages](https://gitlab.com/gitlab-org/omnibus-gitlab/issues) so we welcome your help.
We would like to thank the awesome GitLab community and the [GitLab subscribers](https://www.gitlab.com/subscription/) for their support.
Of course, all previous installation options will continue to be available.
Please join the celebration in the comments and let us know if you have any questions.
