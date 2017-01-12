---
title: "'GitLab is a Slam Dunk': One Team Lead Weighs His Options"
author: Emily von Hoffmann
author_twitter: emvonhoffmann
categories: user stories
image_title: '/images/default-blog-image.png'
description: "Developer Warren Postma shares his opinions on VCS, after years of trying out all the alternatives."
twitter_image: '/images/tweets/why-bare-metal.png'
---

Warren Postma is a team lead and "de facto DevOps guy" at [RamSoft](https://www.ramsoft.com/), but like so many he's gotten hooked on [contributing](https://gitlab.com/warren.postma) to GitLab in his spare time. After becoming familiar with GitHub, Atlassian, and Mercurial in previous jobs, he felt strongly that Git and GitLab were the best choice for his current team. Since reaching that conclusion, he's also assisted his peers and former colleagues in their switch to GitLab, so I wanted to hear his opinions - they're both strong and numerous, which made for a fun conversation.

<!--more-->

Here are some highlights:
* In a team distributed across timezones and languages, the decentralized nature of Git and GitLab is a huge win.
* If you pair people for code review who are in the same timezone, you can prevent having merge requests stay open for days or weeks.
* When switching to GitLab CI, the biggest barrier is training and removing ingrained habits - especially if people are also new to Git.

**Can you briefly describe the kinds of projects you use GitLab for?**
{: .alert .alert-info}

**Warren:** I use it for both personal projects and for my job. I switched a team at a small healthcare company from Subversion to Git, taught some of the team members their first steps in Git, and I switched from preferring Mercurial (another DVCS) to preferring Git, chiefly because I really like GitLab. There is nothing like GitLab for Mercurial although there is a project called RhodeCode and its fork Kallithea that comes close.  I spun up our private GitLab instance and taught our IT people how to maintain it (not hard really).

I also have counseled other people to switch to GitLab, and I'm generally most active in doing so among peers. I know a guy who runs a small software company and I'm helping him switch his team over to GitLab. It feels like I could be finding my niche.

**What is the makeup of your team at RamSoft, and what is your workflow like?**
{: .alert .alert-info}

**Warren:** Our workflow and culture is evolving rapidly. My team is multi-cultural, multi-language, multi-everything, in multiple physical sites.  One part of our team is in Toronto, another part is in Vietnam. The decentralized nature of Git and GitLab is a major win for us. We have two merge request (MR) pipelines. We have all Toronto devs code-review via MR with someone in the same timezone because our MRs should be short-lived MRs, reviewed and merged quickly.  We don't have MRs that stay open for days or weeks.  We don't use WIP much yet, but I am starting to advocate for WIP merge requests for collaborative feature development. Since we're in the same office, we can mostly work in pairs when our work requires it. GitLab provides a history of our work, and our reviews, and MRs are like a project history.

**How did you decide to get started with GitLab?**
{: .alert .alert-info}

**Warren:** It was easy, I chose Ubuntu (I can't remember if it was 12 or 14) LTS and it was around GitLab 8.0, September 2015 or so, and I simply copied the installation commands from the website and pasted it into terminal.  I needed a bit of help from my IT guy to set up LDAP to our ActiveDirectory, and we were good.
Our company is 99% composed of Windows-only technical people, I'm a Linux guy working in a Windows company.  I'd say that in many companies this is a significant barrier to getting up and running.  If I could suggest something, it would be to provide a Hyper-V and a VMWare image of a working private GitLab, which can be downloaded and run by anyone. I think that should be done in-house as opposed to via Bitnami. I have used Bitnami products, and I have nothing against them, but I see the opportunity for GitLab to provide technical support even to smaller corporations as a significant opportunity to GitLab, that it should be taking on.

**Is there anything you feel you can do in GitLab that you can't do with other tools?**
{: .alert .alert-info}

**Warren:** GitLab is about integration of tools. I don't want to set everything up separately. GitLab provides an all-in-one version control server, bug tracker (issues), kanban board (issues in progress, completed, in production), merge request handling (code reviews). All those tools exist in many flavors, but none so well integrated, and I can self-host.

Your closest competitor is Bitbucket, in my opinion, which can be run privately but the private Bitbucket is closed-source I believe, and you can't get it for free, so GitLab CE is really without peer. Since I don't work in very large companies, GitLab EE is something I haven't spent much time on, but I can see that even a serious small company might want to buy GitLab EE because having support is a major feature. If I wasn't working at my current company, the level of Linux knowledge in house would take a major dive, and they'd probably want to buy a support contract to fix their GitLab if it went down, or help diagnose major issues.

Privately Hosted (on my computer or VM) + Free + OpenSource = Made of Win. I can't see choosing anything else. I see GitHub as problematic, something I [blogged about]( http://linuxcodemonkey.blogspot.ca/2016/11/gitlab-all-things.html)


**What is the main reason you would recommend GitLab to another dev?**
{: .alert .alert-info}

**Warren:** Once the choice is made to use Git, to me, GitLab is a slam dunk decision. Software companies, whether small, medium, or large, and even single developers who are professionals who get paid, should be hosting their own in-house GitLab, and perhaps having that back up to some off-site repo (say Bitbucket or GitLab.com). Single developers could be quite happy with Bitbucket also. I happen to still love Bitbucket, but happen to distrust GitHub. I only use GitHub when I have to use it, which is to make MRs to projects that are on GitHub.

People who I have talked to, and I have even given presentations to people at user groups, are usually interested in GitLab because:

1. It lets you host your own private Git server.
2. It has a pretty impressive set of features, issue tracking, merge request handling, and continuous integration server built in.

I am working on a community blog post on switching a small healthcare software company from Jenkins to GitLab CI. So far, I have found that the only difficulty is in training team members. Moving ingrained practices and working against ingrained tendencies is the hardest thing. We previously had a single-branch trunk-based monorepo culture, and switching to Git, to me, was only sensible if we changed our practices to work how Git is meant to be used.

A pet peeve of mine can be summed up in the saying "When all you have is a hammer, everything looks like a nail." In the world of Subversion and Git, what I see over and over is people who take a 10 - 50 GiB Subversion monorepo and then just "import all 50 GiB, and all 500,000 svn commit revs into Git". They are seldom impressed with the results of this, and it seldom occurs to them to question their initial preconception that this was the right and obvious way to move from SVN to Git. I am not sure if there exists a comprehensive re-education plan for Subversion users, but I think perhaps I should write one. There was a start towards this when Joel Spolsky tried something called "[hginit.com](http://hginit.com/)", retraining Subversion victims in how to work with Mercurial. A similar practice for corporate teams moving from Subversion to Git would be a great educational resource that I think GitLab could provide. Some pretty good material in that vein is already on the internet and is provided by Atlassian, as part of their Bitbucket docs.

In terms of companies and products that I consider to be almost "peers" of GitLab, perhaps Bitbucket is closest. I prefer GitLab because the product is open source, the people are great, and the growing community around GitLab is also great. Oh and the product is growing at a fantastic pace. Just watching it from mid 2015 to today, the pace of innovation has been boggling. I have also collaborated with GitLab community members to create add-ons and tools. One guy made a Python-based tool that uses the GitLab API to [expire and delete old artifacts](https://github.com/JonathonReinhart/gitlab-artifact-cleanup) *site-wide*. Another guy made a Go-based tool that copies Issues and Issue labels from one project to another. All great plugins from the community!

_If your team uses GitLab and is interested in sharing your story, please fill out this [form]( https://docs.google.com/a/gitlab.com/forms/d/1K8ZTS1QvSSPos6mVh1ol8ZyagInYctX3fb9eglzeK70/edit)  and we’ll get in touch!_

_Follow Warren on [Twitter](https://twitter.com/warrenpostma)_

_Tweet [@GitLab](https://twitter.com/gitlab) and check out our [job openings](https://about.gitlab.com/jobs/)._
