---
title: "Innersourcing, using the open source workflow to improve collaboration within an organization"
date: 2014-09-05 11:27:30 +0200
author: Sytse Sijbrandij
categories: 
---

Open source development has shown that volunteers can produce amazing software such as the Linux kernel that runs both on smartphones and supercomputers.
The workflow used by open source projects helps to explain why these worldwide communities of volunteers are able to cooperate so effectively.
Similarly, in large organizations software developers are spread out across many departments and they do not frequently meet in person nor do they report to the same boss.
To improve collaboration within the enterprise some companies are starting to take advantage of the same workflow used by open source projects.
Tim O’Reilly [coined the term “inner-sourcing”](http://www.oreillynet.com/pub/a/oreilly/ask_tim/2000/opengl_1200.html) and defines it as the use of open source development techniques within the corporation.

The 7 most important open source workflow practices for enterprises are:

1. Visibility: all software projects are by default visible to all employees
1. Forking: everyone who can see the code, can create a copy (fork) where they can make changes freely; these forks are visible for everyone.
1. Pull/merge requests: even people outside the project are able to suggest changes and you can have a conversation about the code with line comments.
1. Testing: software includes unit- and integration-tests so that changes can be made with less fear of causing problems.
1. Continuous Integration: every proposed change is automatically tested and the result is shown with the change.
1. Documentation: all software projects include a readme that describes what the software does, why that is important, how run it and how to develop it.
1. Issue tracker: there is a public issue tracker in which everyone can submit a bug or ask a question

Most of these workflow improvements are made possible by distributed version control and modern tooling.
In the past a developer had to use word of mouth to find out what other projects were available within the organization and than had to hunt down someone able to give them access to it.
Adding someone to a project to make changes required a leap of faith on part of the responsible team.
This hurt collaboration across departments and led to a duplication of effort.
With a modern workflow the developers can reuse work from colleagues and help projects outside their department without first having to ask for permissions and authorizations.

Many enterprises use GitLab to enable this workflow internally.
At their request we have introduced a third visibility level for projects.
Instead of just public projects (visible to the whole world) or private projects (visible only to the participants) you can also mark a project as internal.
Internal projects are visible to everyone that is logged into the on-premises GitLab server.
This way all employees can reuse software, fork it and contribute back.
With GitLab an organization can quickly benefit from all open source workflow practices while keeping their code secure.

To learn more about innersourcing please see this [list of articles about innersourcing](http://www.inner-sourcing.com/wiki/inner-source-wiki/), [email us](mailto:contact@gitlab.com) or ask a question in the comments below.