---
title: "Packaging GitLab for Fedora: A GSoC 2013 project"
date: 2013-05-28 11:17
categories: gsoc
author: Axilleas Pipinellis
community: true
---

Hi everyone!

It is with great excitement that I announce you the involvement of GitLab in this 
year's Google Summer of Code through the [Fedora][] project.

<!-- more -->

### Whoami

My name is Axilleas Pipinellis, an undergraduate student from Greece. I study 
[Applied Mathematical and Physical Sciences][semfe] in [National and Technical University of Athens][ntua]. 
You can read more info about me [here][aboutme].

### My involvement with GitLab

I have been following GitLab since version 2 and have installed/deployed it 
several times since. Recently, I also started [contributing][] some minor patches,
mainly to the documentation. I have spent several hours contributing not only upstream 
but I also wrote a [wiki article][] for Archlinux, as well as an installation [script][](needs refinement) 
and recently I gave a small [talk] in greek about GitLab during a [hackfest].

### About Fedora and the GSoC proposal

The thought of GitLab being packaged for Fedora and then deployed as an extra service
for [fedorahosted][] isn't new. It was also a proposed idea for GSoC 2012, but
unfortunately it didn't get picked. 

So, this year is the lucky one and the main plan is to package GitLab and all its 
dependencies in `rpm` format, first for Fedora and then for [EPEL][](RedHat, CentOS, etc). 
For a full view of my proposal see [here][proposal] and [there][post] is a post I made 
about this matter two months ago.

I believe this is a huge matter for both parties, as Fedora will be among the officially 
supported platforms and GitLab will benefit from one of the biggest open source 
communities.

Cheers to a fun and productive summer!

[post]: http://axilleas.github.io/en/blog/2013/bringing-gitlab-in-fedora/
[EPEL]: https://fedoraproject.org/wiki/EPEL
[proposal]: https://fedoraproject.org/wiki/GSOC_2013/Student_Application_Axilleas/Gitlab%28463%29
[fedorahosted]: https://fedorahosted.org/web/
[Fedora]: http://fedoraproject.org/
[script]: https://gist.github.com/axilleas/3305554
[hackfest]: https://hackerspace.gr/wiki/Hackfest15 
[talk]: http://www.slid.es/axil/what-is-gitlab 
[wiki article]: https://wiki.archlinux.org/index.php/Gitlab
[contributing]: https://github.com/gitlabhq/gitlabhq/commits/?author=axilleas
[semfe]: http://semfe.ntua.gr/
[ntua]: http://www.ntua.gr/index_en.html
[aboutme]: http://axilleas.github.io/about
