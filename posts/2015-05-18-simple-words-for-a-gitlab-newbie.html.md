---
title: "Simple words for a GitLab Newbie"
date: 2015-05-18
author: Karen Carias
author_twitter: myvineste
image_title: '/images/unsplash/water.jpg'
---

For most of us, when we work with a new tool, there's a process of learning the right vocabulary and the best steps to make things happen; this while we try to keep the best attitude. Not very long ago, I learned how to use Git and GitLab and it was a little bit painful. I read a lot about it, but it was mostly vocabulary that didn't make any sense to me. If you've been there or if you are there now, you'll know what I'm talking about (some people may have it naturally).

So, to make this learning process easier for others, I took many of the basic Git vocabulary and wrote easy definitions for each word. I hope they are useful for you and please share them with your Git and Gitlab newbie friends!

<!--more-->

## Cloud Based Services
What is a cloud based service? It’s a service or resource that is opposed to services that are hosted on the servers inside a company, which is the traditional way of doing it. It helps people and companies lower their costs and be more efficient while helping with different functions such as trannings, storage, etc.
GitLab.com is a cloud based service because it can be hosted both in house and in the cloud.

## Source control or revision control software
What is source control? It’s a system that records and manages changes to projects, files and documents. It helps you recall specific versions later. It also makes it easier to collaborate, because it shows who has changed what and helps you combine contributions.

## Continuous Integration
What is continuous integration? It’s the system of continuously incorporating the work advances with a shared mainline in a project. Git and GitLab together make continuous integration happen.

## Continuous deployment
What is continuous deployment? It means that whenever there is a change to the code, it is deployed or made live immediately. This is in contrast to continous integration, where code is continuously being merged in the mainline and is always ready to be deployed, rather than actually deployed.
When people talk about CI and CD what they usually mean to say is that they are constantly and automatically testing their code against their tests using a tool such as GitLab CI and upon passing to a certain action. That action could be merging the code into a branch (master, production, etc), deploying it to a server or building a package / piece of software out of it.
Non-continuous integration would be everyone working on something and only integrating all the work as the very last step. Obviously, that results in many conflicts and issues, which is why CI is adopted widely nowadays.

## Git
What is Git? Git is a system where you can create projects of different sizes with speed and efficiency. It helps you manage code, communicate and collaborate on different software projects.
Git will allow you to go back to a previous status on a project or to see its entire evolution since the project was created.
You could think of it as a time machine which will allow you to go back in time to whenever you’d like in your project.
With Git, 3 basic issues were solved when working on projects:
1. It became easier to manage large projects.
2. It helps you avoid overwriting the team’s advances and work.
3. With git, you just pull the entire code and history to your machine, so you can calmly work in your own little space without interference or boundaries. It's much simpler and much more light-weight.

## Repository
What is a repository? The place where the history of your work is stored.

## Remote repository
What is a remote repository? It's a repository that is not-on-your-machine, so it's anything that is not your computer. Usually, it is online, GitLab.com for instance. The main remote repository is usually called “Origin”.

## Commit
What is a commit? It’s the way you call the latest changes of source code that you made on a repository. When changes are tracked, commits mark the changes on a document.

## Master
What is a master? It’s how you call the main and definitive branch (the independent line of development of a project).

## Branch
What is a branch? It’s an independent line of development. They are a brand new working directory, staging area, and project history. New commits are recorded in the history for the current branch, which results in taking the source from someone's repository (the place where the history of your work is stored) at certain point in time, and apply your own changes to it in the history of the project.

## Fork
What is a fork? It’s a copy of an original repository (the place where the history of your work is stored) that you can put somewhere else or where you can experiment and apply changes that you can later decide if publishing or not, without affecting your original project.

## Git Clone
What is a clone? It’s to get a copy of a git project to look at or to use the code.

## Git Merge
What is to merge? It’s integrating separate changes that you made to a project, on different branches.

## md: markdown
What is markdown? It’s a plain text format that will make any document easy-to-write and easy-to-read.

## Push a repository
What is to push a repository? It’s to incorporate a local branch (the independent line of development of a project) to a remote repository (online version of your project).

## README.md
What is a README.md? I’t a file in a simple format which summarizes a repository. If there’s also a README (without the .md), the README.md will have priority.

## SSH (secure shell protocol)
What is SSH? It’s how you call the commands that help communicate through a network and that are encrypted and secure. It’s used for remote logins and it helps users connect to a server in a secure way.

## Stage Files
What is to stage a file? It’s how you call the act of preparing a file for a commit (the latest changes of source code in a repository).

## GitLab
What is GitLab? GitLab is an online Git repository manager with a wiki, issue tracking, CI and CD. It is a great way to manage git repositories on a centralized server. GitLab gives you complete control over your repositories or projects and allows you to decide whether they are public or private for free.

### GitLab.com
* GitLab.com hosts your (private) software projects for free.
* It offers free public and private repositories, issue-tracking and wikis.
* It runs GitLab Enterprise Edition and GitLab CI.
* No installation required, you can just sign up for a free account.
Support Package:
* Free subscribers can use the GitLab.com Support Tracker if they have questions.
* GitLab.com Bronze Support will let you email support directly for timely, personal and private answers. This costs $9.99 per user per year for next-business-day response time and is available in packs of 20 users.

### GitLab Community Edition (CE)
* Free, self hosted application where you can get support from the Community
* Feature rich: Git repository management, code reviews, issue tracking, activity feeds and wikis. It comes with GitLab CI for continuous integration and delivery.
* Open Source: MIT licensed, community driven, 700+ contributors, inspect and modify the source, easy to integrate into your infrastructure.
* Scalable: support 25,000 users on one server or a highly available active/active cluster.
* Merge requests with line-by-line comments, CI and issue tracker integrations.

### GitLab Enterprise Edition (EE)
* Self hosted application that comes with additional support.
* Builds on top of the Community Edition and includes extra features mainly aimed at organizations with more than 100 users.
* It has LDAP group sync, audit logs and multiple roles.
* It includes deeper authentication and authorization integration, has fine-grained workflow management, has extra server management options and it integrates with your tool stack.
* GitLab EE runs on your servers.

### GitLab Continuous Integration (CI)
* Free, self hosted application that integrates with GitLab CE/EE. Also availble as SaaS at ci.gitlab.com.
* Easy to set up since it is included in Omnibus packages of GitLab or use it for free on ci.gitlab.com.
* Beautiful interface with a clear menu structure.
* Performant and stable, as tests run distributed on separate machines.
* Will help you receive test results faster with each commit running in parallel on multiple jobs.
* Free to use and completely open source. All CI code is MIT licensed.
