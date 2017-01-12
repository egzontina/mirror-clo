---
title: Using the Omnibus GitLab package to ship GitLab
date: 2016-03-21 17:00
author: Marin Jankovski
author_twitter: maxlazio
image_title: /images/unsplash/cat-in-the-box.jpg
---

Two years ago we announced that [GitLab is now simple to install] to great
triumph. Since then, GitLab has grown to become an irreplaceable tool for
many professionals. Part of this success can certainly be credited to an easier
installation process using the omnibus-gitlab packages. The packages, however,
seem to have polarized people to either
[love](https://twitter.com/invalidusrname/status/673862628125614080)
[them](https://twitter.com/Merenon/status/692027386272047104), or
[hate](https://twitter.com/phessler/status/672747920635109376)
[them](https://twitter.com/jiphex/status/672746104103051265).

Let's take a look at what kind of decisions we need to make on
every release of GitLab and how omnibus-gitlab package fits into this process.

<!--more-->

## Omnibus concept

The [Omnibus project] is the brainchild of Chef Inc.
Their product, Chef Server, was notoriously hard to install and configure. To
tackle this issue the Omnibus project was created. The idea behind it was to
have one binary package for the supported OS that would install all required
dependencies and allow configuration of each required component.
This meant that the end binary package will not be lean like the packages
that people usually encounter. In fact, they will be "fat" and
hence [the name Omnibus].
This also meant going against [the Unix design principles] which favor
[composable components] as opposed to [monolithic software] (which reminds Unix
users too much of Windows software).

The concept is simple:

* Have one binary package that contains all required components.
* Make sure that a specific version of the package has all required components.
* Make sure that the supplied components have the version that is known to work
  in a predictable manner with other components.

## Installing GitLab from source

GitLab is facing similar challenges.
[Installation and upgrade guides] for what we call *installation from source*
are available but they are at least 10 pages long.

They show how to install and configure multiple dependencies,
system users, which directories and files need to exist, and user permissions
they need to have and so on. Installing a wrong version of a dependency
means that things might not work as expected, so it is imperative to follow the
guide strictly to the letter.

Upgrading can sometimes be challenging. The update guide is shorter but there are time constraints that can make the upgrade stressful. Having everyone breathing down
your neck and expecting everything to go smoothly makes upgrading very stressful.

## Omnibus-gitlab

Enter the omnibus-gitlab package.

Anyone should be able to install and configure GitLab with minimum knowledge.
GitLab should be available on the most widely-used Linux distributions.

We want the focus to be on GitLab and its features.
Installation and upgrades should be easy and almost enjoyable!

This is how omnibus-gitlab was born.

Benefits for everyone:

1. Users need only to apply minimal effort to install GitLab.
1. Users need only to provide minimum configuration to get GitLab up and running.
1. Users can easily upgrade between GitLab versions.
1. Users are encouraged to upgrade to the latest version of GitLab which is
always better than the previous one.

Benefits for the maintainers of GitLab:

1. We provide our users with only one binary package they would need to
install.
1. We ship packages for multiple platforms at the same time.
1. We make sure that the components that GitLab requires for a specific
version are shipped.
1. We know that the components are running on versions that are compatible.
1. It becomes easier to support any issues users have because we have a more
consistent environment.
1. We maintain one project that covers all of the above.

The last point is very important for a project like GitLab.

GitLab has a monthly release cycle. Every month on the 22nd we need to release
a new version. We usually follow up the release with a couple of patch releases
to address any regressions that might have been introduced previously.
Given how important GitLab is to the development infrastructure, we need to be
able to react quickly to any vulnerabilities in GitLab or any of its components.

### A Silver Bullet?

Not quite.

The omnibus-gitlab package does a lot for the end user but because of that it
makes a lot of choices for the user. It will create the directories and files
on the file system and assume that it can do so.
It will create the system users. It will occupy the ports it needs.
It ships with its own UNIX init supervision system, runit.
It ships with libraries that may already exist on the system
(albeit maybe of a different version).

For a very large portion of users all of the above won't matter but there are
environments which are highly restrictive.
The package has a lot of configuration to make it easier to adjust to the
environment but this can be a lot of work to get right.
We are always working on making the package even more customizable while
assuming the best possible defaults for users who don't need to customize.
However, it is a marathon rather than a sprint.

### Alternatives to Omnibus we've considered

We are always evaluating the new options that become available.
Let's take a look at a few of the options that we've already considered.

#### Docker images

Two years ago Docker was still a very new project. It had problems like any new
project (like us!) The number of users using it in production is growing but
we could not and cannot count on everyone supporting Docker in their
environments. Introducing Docker into your environment adds another piece of
software that needs support and not everyone can add this layer.

The packages in .deb and .rpm archive format are usually allowed in most if not
all systems.

We do release new [Docker] images on every release as an additional method of
installing GitLab.

#### Native Debian Packages

Users encouraging us to ship GitLab as a native Debian package usually say that
this would keep us in line with the Unix design principles and we can leverage
packages that already exist on the system instead of reinventing the wheel! You
most likely already have openssl installed on your system, why do you want to
ship another one?

Let's take a look at what that would entail:

1. Packaging over 300 Ruby gems as separate packages. (This is Spartaaa!)
1. If a component version we require does not exist in the system package
repository, tell the user to compile it.
1. Do this at least once a month to be able to follow the monthly release.
1. Make sure that any change that was created in GitLab by us or any of the
contributors does not break the package.

Native packages are more suited for the slower release cycles and this clashes
with the way GitLab does releases.

We also don't have enough expertise and big enough team to do native packaging.
It is a lot of work and we would need a dedicated team only for the packaging
for this specific platform.

There is some good news though!
Pirate Praveen has been working for the past 6-8 months on
[native Debian packages].
The packages are almost ready to be included in the Debian package
repository.

This will allow all users who do not want the omnibus-gitlab package to touch
their system to easily install GitLab.

We have yet to see how much of an effort will it be to release new
versions but this is something that will be announced once the packages are
ready.

#### Native Fedora Packages

This case is pretty much the same as the native Debian packages.
There was an attempt to package GitLab for Fedora as a part of the
[Google Summer of Code project] by Achilleas Pipinellis, who has since become
a GitLab team member. Through that effort, we learned it is a multi-person
job and packaging alone is a lot of work. So, the project was never completed.

If you are interested in helping to create the native Fedora packages,
you can leave your comment in
[this issue on GitLab CE issue tracker.](https://gitlab.com/gitlab-org/gitlab-ce/issues/14043)

#### Anything else

We've been asked a few times why we don't just let Chef, Puppet, or Ansible to
be configured by the developer.

You can still use your favourite configuration management tool to do this work.
However, be advised that it is _still_ a lot of work. That also means that for
every GitLab update, the administrator needs to go through a list of changes
and see if they need to upgrade the software. If they don't, GitLab might not
work as expected.
The end user most likely won't care how the setup is done, they might just see
something not working as they would expect. That is a risk we want to remove if
we can.


## Conclusion

One of GitLab's strengths is that we are able to have a very short release
cycle, getting the updates to all our users very quickly.
The omnibus-gitlab packages aren't perfect but they are currently the best
option currently for frequent GitLab updates.

If you consider the amount of time required to maintain eight packages
(four platforms, one package each for CE and EE, two docker images,
two Raspberry Pi 2 packages),
the monthly release cycle, and making upgrades between versions and
installations as simple as possible,
then omnibus-gitlab is doing a very good job.

[A lot](https://twitter.com/choyer/status/670273120566120449)
[of users](https://twitter.com/jrblier/status/613077041219399681)
[that have been using](https://twitter.com/mickael_andrieu/status/646278424936480768)
the omnibus-gitlab packages
[to maintain](https://twitter.com/invalidusrname/status/673862628125614080)
[their GitLab installation](https://twitter.com/J_Salamin/status/687884326629937152)
[seem to](https://twitter.com/alexzeitler_/status/692812151296282625)
[agree with this](https://twitter.com/berkeleynerd/status/692093491149582339).

With the omnibus-gitlab packages available for everyone, we can work in parallel
to create more ways to install GitLab.

Want to help improve omnibus-gitlab package? Contribute to omnibus-gitlab at the
[omnibus-gitlab repository].

Want to work on making GitLab available on your favourite platform but need
some feedback? Get in touch through the [GitLab CE issue tracker].

Are you in New York on April 12th, 2016?
Ask me a question at the [Software Architecture Conference] where I'll be
speaking about Shipping a Ruby on Rails stack to thousands of companies every
month.


[GitLab is now simple to install]: https://about.gitlab.com/2014/02/14/gitlab-is-now-simple-to-install/
[Omnibus project]: https://github.com/chef/omnibus
[the name omnibus]: https://en.wikipedia.org/wiki/Omnibus
[the Unix design principles]: https://en.wikipedia.org/wiki/Unix_philosophy
[composable components]: https://en.wikipedia.org/wiki/Composability
[monolithic software]: https://en.wikipedia.org/wiki/Monolithic_application
[Installation and upgrade guides]: http://doc.gitlab.com/ce/install/installation.html
[Docker]: https://hub.docker.com/u/gitlab/
[native Debian packages]: https://wiki.debian.org/GitLab/Packaging
[Google Summer of Code project]: https://fedoraproject.org/wiki/User:Axilleas/GitLab
[omnibus-gitlab repository]: https://gitlab.com/gitlab-org/omnibus-gitlab
[GitLab CE issue tracker]: https://gitlab.com/gitlab-org/gitlab-ce/issues
[Software Architecture Conference]: http://conferences.oreilly.com/software-architecture/engineering-business-us/public/schedule/speaker/228210
