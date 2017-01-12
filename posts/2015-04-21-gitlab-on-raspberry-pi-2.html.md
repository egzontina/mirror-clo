---
title: "GitLab on Raspberry Pi 2!"
date: 2015-04-21
author: Job van der Voort
author_twitter: Jobvo
image_title: '/images/stock/rbp.jpg'
---

Want to run GitLab on your Raspberry Pi 2?
Now you can do so much easier!

Previously you had to install GitLab from source yourself.

We have just released the [official Raspberry Pi 2 Omnibus package for Raspbian OS](/installation/#other-methods)
that you can use to install GitLab quickly on your new small-but-powerful
repository server!

*We recommend adding at least 1GB of swap*, read about the reasons at the [hardware requirements page.](http://doc.gitlab.com/ce/install/requirements.html#memory)

Install the required packages like shown on the [installation instructions](/downloads) page.

*UPDATE* Raspberry Pi 2 packages are now uploaded to its own package repository so it's now even easier to keep your GitLab up-to-date! Just go to the [installation instructions page](/downloads) and select `Raspberry Pi 2 for Raspbian` from the `Select Operating System` dropdown for directions on how to add the repository and install GitLab.

~~Download the Omnibus package for Raspberry Pi 2 and install it:~~

```
wget https://s3-eu-west-1.amazonaws.com/downloads-packages/raspberry-pi/gitlab_7.9.0-omnibus.pi-1_armhf.deb
sudo dpkg -i gitlab_7.9.0-omnibus.pi-1_armhf.deb
```

Run reconfigure to install:

```
sudo gitlab-ctl reconfigure
```

Sign in on your new micro-instance with username `root` and password `5iveL!fe`.

<!-- more -->

## Help us scaling GitLab up the fruit tree

Currently, the packages for Raspberry Pi are built manually and for minor
releases only.

We are looking for ways to automate building the Raspberry Omnibus packages,
so we can keep them up to date. For this we either need to cross-compile them (complex),
or build them on ARM servers (hard to find).

~~We welcome suggestions on this subject.~~

*UPDATE* Thank you for all your suggestions. Currently we are using Scaleway.com to build packages for Raspberry Pi 2 on Raspbian OS.


### Update

If you are using GitLab on your Raspberry Pi 2, it works exactly the same way as it does regularly. You can use [GitLab's official user documentation](https://about.gitlab.com/downloads/) as a guide.
