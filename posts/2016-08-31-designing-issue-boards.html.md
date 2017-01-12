---
title: "Feature Highlight: Designing Issue Boards"
author: "Taurie Davis"
author_twitter: tauried
categories: GitLab
image_title: '/images/blogimages/designing-issue-boards/header-image.png'
description: 'Feature Highlight: Learn how the UX team worked together on the creation of Issue Boards.'
twitter_image: '/images/tweets/designing-issue-boards.png'
---

Accurate planning and coordination of each release at GitLab is critical to shipping useful features on time.In order to improve our planning process, not only ourselves but also for everyone who uses GitLab, we took a look at our existing features that help teams organize issues. From here, we determined that our current [Milestone Board](/2016/08/05/feature-highlight-set-dates-for-issues/#milestones) was not powerful enough for larger teams or more complex projects. The team then began to brainstorm ideas for designing and implementing a new type of board that allows users to visually plan issues.

<!--more-->

## The Proposal

At GitLab, we believe that the speed of innovation for our organization and product is constrained by the total complexity we've added so far. Creating [boring solutions](/handbook/#boring-solutions) and simplifying our product to its absolute minimum allows us to ship faster and make iterations based on real user feedback. With this in mind, our team began determining basic principles that would help guide us during the creation process of the new Issue Board feature.

We knew we wanted the product to be able to:

- Provide an overview of issues in a more visual way
- Allow for a workflow with multiple intermediate steps
- Use existing metadata that would keep the same sorting and filtering tools that already exist

    
Knowing this, the team was able to craft a [proposal](https://gitlab.com/gitlab-org/gitlab-ce/issues/17907) that began to come to life with requirements, user stories, and wireframes.

![wireframe](/images/blogimages/designing-issue-boards/wireframe.png){: .shadow}

## Feedback & Challenges

Here at GitLab we are able to gather feedback early by posting our proposals as issues that are publicly available to team members, contributors, customers, and users. With over 100 participants, the Issue Boards proposal recieved a lot of responses that validated many of our assumptions, addressed concerns, and provided insight for future improvements.

Some concerns included:

- **Using labels as lists.** The drawback being that it can be confusing to use labels for issues, as well as creating lists. However, we believe that the flexibility of using labels for lists outweighs the downsides. Users will have the same metadata available throughout GitLab, as well as be able to use all the same sorting and filtering tools that already exist.
- **Assigning multiple list labels to one issue.** We believe that managing boards should be up to the user. If a user assigns three list labels to the same issue, the issue will display in all three corresponding lists and the labels will change if you drag the issue from one column to another. As a user [mentioned](https://gitlab.com/gitlab-org/gitlab-ce/issues/17907#note_12602314): *"Being able to display the same issues in multiple ways to track needs differently for different user-types through different work flows would be hugely valuable."*  We definitely agree!
- **Only having one Issue Board per project.** The current scope of this feature for [GitLab 8.11](/2016/08/22/gitlab-8-11-released/) allowed only a single board per project. However, we understand the benefit of having multiple boards per project. We also recognize that many teams work across repositories and want to see Issue Boards available at a group level. These are improvements we are planning for a future release. :)

## Refining through Collaboration

After addressing participants' concerns, the UX team started further refining UI elements and polishing interactions. Every member of the UX team worked on the design at some stage of the process and we came to the final product through iteration and collaboration.

We worked on creating a board that turned issues into draggable cards, provided an easy way to create default lists, and took advantage of the metadata that labels gave us by keeping the same filtering options that are available throughout the site. We also determined that the default Backlog list could contain an unmanageable number of issues, so we added a search functionality in order to find issues more easily.

The design, development, and product teams all worked closely throughout the creation process and met up once a week to discuss challenges, status, and overall excitement for the launch of this feature. 

![issue-board](/images/blogimages/designing-issue-boards/issue-board.gif){: .shadow}

## What's next

The [GitLab Issue Board](/solutions/issueboard) was created as a flexible tool that can be used for various workflows and tasks. We lean towards light-weight, flexible implementations so we can ship quickly, see real use cases, and make informed iterations. We are super excited to [continue working](https://gitlab.com/gitlab-org/gitlab-ce/issues/21365) on Issue Boards in the upcoming releases; from multiple and cross-project boards to searching through all lists and creating an issue directly from the board view. If you have further ideas for future improvements, let us know by [making an issue](https://gitlab.com/gitlab-org/gitlab-ce/issues/new?issue)!

## Join our webcast 
If you want to see a live demo of the Issue Board and see some of the other great features in [GitLab 8.11](/2016/08/22/gitlab-8-11-released/), join our webcast on September 1st. [Register now](https://page.gitlab.com/IssueBoardWebcast_LandingPage.html).  

