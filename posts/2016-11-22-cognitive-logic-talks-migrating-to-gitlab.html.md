---
title: "Data Startup Cognitive Logic Talks Migrating to GitLab"
author: Emily von Hoffmann
author_twitter: emvonhoffmann
categories: user stories
image_title: '/images/team_gitlab.png'
---

Data analytics startup [Cognitive Logic](http://www.cognitivelogic.com/) helps companies store, share, and examine consumer information without compromising security. I sat down with engineer Johan Brandhorst to learn more about his team, their work, and how GitLab helps.

Three of our offerings in particular drove Cognitive Logic's decision to switch to GitLab:

* Validated Merge Requests
* Easily Configurable CI
* Easy migration from GitHub

<!--more-->

Johan also told me that his team's biggest challenge with GitLab is that it can be difficult to orchestrate CI between repositories; he says they're looking forward to being able to chain testing between repositories. A fix is in the works - in typical fashion, minutes after I posted his query on Slack our Head of Product, [Mark Pundsack](https://twitter.com/MarkPundsack), wrote back that we have [existing functionality](https://docs.gitlab.com/ce/ci/triggers/) that allows one pipeline to trigger another pipeline in a different project. There are also several [issues](https://gitlab.com/gitlab-org/gitlab-ee/issues/933) open to make this better.

**Could you please explain for our readers what the dev team at Cognitive Logic does? What kinds of projects do you work on?**
{: .alert .alert-info}

**Johan:** We’re working on connecting large datasets while maintaining customer privacy. Our platform is built on docker and golang microservices with a React/node.js frontend. We use gRPC for communications between services and protobuffers for backwards compatible messages. We maintain a container for our build environment and compile static binaries which can be run in a minimal docker container. The whole system runs on a cloud service provider.

**You currently have 10 devs using GitLab — could you elaborate on the makeup of the team, and what your workflow is like?**
{: .alert .alert-info}

**Johan:** We have a high focus on engineering; engineers have control over what they want to work on and what they consider the most important to work on at the time. As an engineer, it’s a very liberating and enjoyable experience. We maintain a startup culture with a pool table, a couple of consoles in the meeting room with a 4K TV, board games and company events every now and then. It’s a great place to work (we’re hiring!).

We try to raise issues when features or bugs arise, then triage in a branch, submit a merge request, have it approved by another engineer before being merged back into master. Validated merge requests means we’re not afraid of merging straight into master as we try to do as much testing and validation as possible at merge request time. In the future we are going to try to set up staging environments and merge request environments for complete system validation at merge request time.

**Which features or capabilities of GitLab has your team used the most? Is there anything you feel you can do with GitLab that you can't accomplish with other tools?**
{: .alert .alert-info}

**Johan:** Definitely the validated merge request system. It has helped us ensure consistently passing tests and linting tools to maintain the quality of the codebase. The GitLab docker registry has also been very useful for storing the output of our builds and provide a central point from which to fetch those builds.

**What were the major problems you were trying to solve with your previous version control system, if you used one?**
{: .alert .alert-info}

**Johan:** We were using Github for VCS before moving to GitLab earlier this year. I came from a company where we had rolled our own CI solution while running our own VCS server and I knew how much time it takes to run a system like that reliably, so when I started at Cognitive Logic I was conscious about trying to make good choices for VCS early on. This lead me to look at GitLab as I wanted something with easy CI and validated merge request capabilities to ensure maintained code quality. GitLab was perfect in this regard and we made the switch from Github.com to GitLab.com about 6 months ago. The major difference between GitLab and Github was the easily configurable CI.

**How have developers responded to migrating to GitLab? Have there been any unforeseen challenges or obstacles?**
{: .alert .alert-info}

**Johan:** We started the migration process quite early so there wasn’t much work to be done. I used the “import from Github” tool to get our repositories up and running on GitLab, and it imported all our issues and merge requests without problems. For the developers it took a little getting used to, but being able to sign up with your Google or Github account helped. There hasn’t been any real problems with our transition to GitLab, I’d consider the features of GitLab to be a superset of those available on GitHub, so it was all positive. The currently biggest problem with GitLab to us is that it can be difficult to orchestrate CI between repositories. We would like to be able to chain testing between repositories so that a change in one repo can automatically trigger a merge request in another repo (complete with testing). I know this kind of solution is being worked on and we’re eager to see what the team can deliver.

*If your team uses GitLab and is interested in sharing your story, please fill out this [form]( https://docs.google.com/a/gitlab.com/forms/d/1K8ZTS1QvSSPos6mVh1ol8ZyagInYctX3fb9eglzeK70/edit)  and we’ll get in touch!*

_Read more about [Cognitive Logic](http://www.cognitivelogic.com/), and follow them on [Twitter](https://twitter.com/cognitivelogic)._

_Tweet [@GitLab](https://twitter.com/gitlab) and check out our [job openings](https://about.gitlab.com/jobs/)._

