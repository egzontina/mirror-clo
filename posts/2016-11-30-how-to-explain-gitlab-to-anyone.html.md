---
title: "How to explain GitLab to anyone"
author: Rebecca Dodd
author_twitter: reberoodle
categories: GitLab workflow
image_title: '/images/blogimages/explain-gitlab-cover.jpg'
twitter_image: '/images/blogimages/explain-gitlab-cover.jpg'
---

How do you explain what GitLab is and how it works to a non-technical person?

This is a challenge I’m facing right now, as I try to describe the company I just joined to my family and friends. <!-- more --> Initial conversations were not very successful:


Me: “It’s an open source workflow solution...”

Them: “What’s a workflow?”

Me:

Them:

Me:


I’ve been getting closer (“We help people who write code to collaborate on projects”), but it’s still hard to drive the idea home in a way that really speaks to people – especially if they have only a vague idea of what coding is.

In a team meeting we tried to come up with some real-world examples of how GitLab works, from using files on a computer, to DropBox, to Google Docs. But what if you’re talking to someone who’s not that comfortable with computers?

## Let’s bring it back to something relatable, paper!

Say I’m a newspaper journalist collaborating with my team on a big story about a concert. We’ve been given a brief, but we each have different aspects of the story to cover: someone will interview the performers, someone else will provide some background about the venue.

If we all worked on that original brief, we might end up writing over each other’s contributions and it would be hard to see what each person is working on. We have a meeting to divide up the work and establish what each team member’s task is and how we will approach it. To make things more efficient, we make photocopies of the brief so that each team member has their own copy that they can start adding to. We all have other articles we’re working on at the same time, so we spend some time prioritising tasks.

I write a draft, and when I’m happy with my contribution, it needs to be fact checked and edited for spelling and grammar. Once a sub-editor gives it the go-ahead, I approach my editor to add my piece (currently on the photocopied brief) to the main story. My editor reviews my work, approves it for the story and includes it in the original. When this is done we create a mock-up of the newspaper page with the article so we can see how it will look.

My colleagues go through the same process until all of their work is visible too – this happens every time a change is made, no matter how small, so we know that each new part of the story has been reviewed and checked for errors. When the deadline comes, we send the newspaper to the printers and then it gets distributed. We might get some responses to our story from readers who write in: someone might suggest some information that would have been useful to include in the article, so we update the online version of the article on our website and the new addition is visible right away. Other reader feedback might be useful for improving what we write about next time.

![Brief to Print](/images/blogimages/brief-to-print.png)

## This is how GitLab works!

The process I described above is a [workflow in which everyone collaborates to bring an idea to production](https://about.gitlab.com/2016/10/25/gitlab-workflow-an-overview/), and it’s a process that works just as well for developers making software as it does for my imaginary newspaper team.

![Idea to Production](/images/blogimages/idea-to-production.png)

In GitLab, we start with an Idea (the main article that everyone will work on), then break it up into Issues (each team member’s tasks). To help us plan, we have an Issue Board to organize Issues into order of priority, just as the journalists had to work out how they were going to approach their tasks in amongst the other articles they are working on. To make sure we don’t overwrite each other’s work, we make our own ‘photocopies’ of the original idea: we call these Branches.

Then, we code! This is like that first draft of my contribution to the story. When the code is ready, we Commit it, like a final draft. The sub-editor checking the work before updating the article is part of what we call Continuous Integration – a system by which the project is updated throughout the day, and those updates are automatically, continually checked for any problems. When I ask the editor to approve my contribution, we do this in the form of a Merge Request, and when that’s been approved, we can preview the changes in Staging, just like the newspaper team did with the mock-up of the page. If everything looks good, it goes into Production, the equivalent of going off to the printers.

The last stage of the cycle is feedback: our ‘reader letters’ might be comments from colleagues or users, or data from analytics, and we use it to make sure we’re always improving. If there’s something we can change immediately, Continuous Deployment ensures the project is always up to date (like the newspaper’s website can show a change or addition to an article right away), and other feedback is used to do better next time.

Image: "[The Deptford Project — Newspaper](https://www.flickr.com/photos/eivind1983/4703991995/in/gallery-94794587@N03-72157635294619645/)" by [Eivind Z. Molvær](https://www.flickr.com/photos/eivind1983/) is licensed under [CC BY 2.0](https://creativecommons.org/licenses/by/2.0/)
