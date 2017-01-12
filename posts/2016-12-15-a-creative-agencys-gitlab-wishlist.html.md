---
title: "A creative agency's GitLab wishlist"
author: Emily von Hoffmann
author_twitter: emvonhoffmann
categories: user stories
image_title: '/images/blogimages/a-creative-agencys-gitlab-wishlist.jpg'
description: "A Lukkien developer shares his team's challenges with Git and GitLab for their UX designs, and requests a few tweaks they'd find useful."
twitter_image: '/images/tweets/default-blog-image.png'
---
[Wouter van Kuipers](https://twitter.com/wvkuipers) is an engineer at [Lukkien](https://www.lukkien.com/en/), a creative agency that produces online media, photography, film, apps, CGI, and graphic design. His team currently works on a platform aimed at parents and healthcare professionals. They've used a combination of Jenkins and GitLab, although they are switching to GitLab CI for testing. He told me his team tends to use the collaboration tools of GitLab the most. Before GitLab, they used SVN, and ultimately decided on GitLab instead of a competitor because they needed to host on-premises for security reasons. Our service engineer [Lee Matos](https://twitter.com/leematos) sat down with Wouter to learn about how GitLab can help.

<!--more-->

Here are some items discussed below and requested by the Lukkien team:

* A view that will let you see changes over builds, and how builds are affected over time.  
* Notifications around CI builds, so if there are any related tickets, those get updated as well.
* Versioning for Photoshop and InDesign files.

**Wouter:** We struggle as a team and company to find a good versioning system for our (UX) designs. Right now we create separate folders and label the versions of our InDesign and Photoshop files. We want to know the latest version, but also want to have a clear visual representation of the changes between versions. Is there any planning for tooling like that in GitLab in the (near) feature?
{: .alert .alert-info}

**Lee:** Frankly, this is on our dream feature list. I think everybody on our team wants to be able to version Photoshop and InDesign documents, but we don’t have a good solution for those files right now that's going to work smoothly. It looks like Adobe is getting into the versioning space for files like these, so there’s a silver lining here in that once Adobe solves that problem, we’ll probably do something similar quickly thereafter.

**Wouter:** My next question is that we are hosting GitLab using a Docker setup, this works quite well but we are not sure if this will create limitations in the long run, for example if we want to use Mattermost in the future? My team has 8-10 developers, but we use the setup for all our teams, we’re all in the same GitLab instance. So that’s 100-120 developers.
{: .alert .alert-info}

**Lee:** That's what I would call GitLab Small/Medium-sized. As it stands, we think that will be fine, there are no limitations even with Mattermost and we don’t expect there to be any problems. Obviously if there are, we’ll explore that with you and figure it out. Our product team leads aren't aware of running GitLab in Docker at a big scale (1000+) – most of those clients are running it directly in a VM or Bare Metal. We feel that obviously Docker is the future so we need to find the answer to these questions. If you run into anything, please bring it up in an issue. And the same goes for Docker in Mattermost, we don’t expect anything different.

**Wouter:** Finally, in what way does GitLab want to position itself in the long run compared to GitHub?
{: .alert .alert-info}

**Lee:** The best way to think about it, for me, is we are actually more like Atlassian. Our end goal is to build what Atlassian ended up with by acquiring the little pieces, by instead building those parts and making them 100 percent cohesive. So it’s more about building an end-to-end development tool that allows your team to work together and converse and go. Our buzz phrase at this point is "From idea to production", so we want to cover everything over that process, and make it faster, whatever you’re using GitLab for. That’s even our goal internally as well, so it excites me because we’re actually using GitLab to build it.

I think GitHub is positioning itself as more of a core component, they see Git and code as the core thing that needs to be solved, and are leaving integrations up to the third parties. We have integrations and we see the value in them, but we want to build something that allows you to start making things work out of the box. Instead of saying "You need to go buy Drone CI, you need to use Waffle.io, and need to wire them all up and read 10 different documentations to figure it out." We want that process to be as easy as possible.

Image ["Lightroom Preset Balloon Release"](https://www.flickr.com/photos/lennykphotography/26687024535/in/photolist-GEeYCF-hUAGKL-nQCwXy-Emhqdz-HRUzeG-EeGxU4-p2KCQa-Eroe6z-e4BpVm-dcZWfj-mQnNTJ-atd2f5-DSYEyA-DSqqGk-DFXwUA-aHPQVk-GucZJZ-EDGjje-CS8FYi-rymZ62-EBjtSY-DSfzQT-avJQMx-aYtqkR-CztMC7-dTRM3q-EPK3hD-DpeasQ-f2hdPB-eRwBGC-EoaxPD-b18F74-9sd1No-bkNuRx-byvPzZ-hxRZyb-D7F1xM-EVqmsh-CVBJBa-9pnw9W-eBWbNx-ftZrun-DXtJuT-p8As5e-DWQhdR-bkNdg7-oQCcaJ-b3JagT-8VoF1U-cgzLCU) by [Lenny K Photography](https://www.flickr.com/photos/lennykphotography/) is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/legalcode).

_We want you to ask us anything! If you're a user interested in sharing your story on our blog, please fill out this [form]( https://docs.google.com/a/gitlab.com/forms/d/1K8ZTS1QvSSPos6mVh1ol8ZyagInYctX3fb9eglzeK70/edit)  and we’ll get in touch!_

_Tweet us [@GitLab](https://twitter.com/gitlab) and check out our [job openings](https://about.gitlab.com/jobs/)._
