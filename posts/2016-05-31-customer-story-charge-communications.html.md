---
title: "Customer Story: Charge"
author: GitLab
author_twitter: gitlab
categories: 
image_title: /images/blogimages/Charge-customer-story/person-on-phone.jpg
---

We always like to hear how our customers are using GitLab. In this post we will share how [Charge](https://charge.co/), 
a telecommunications company uses GitLab. 

<!-- more -->

- **Industry:** Data-only telecommunications
- **Company Size:** 5
- **Development Team:** 5
- **Location:** San Francisco

## Overview

Charge, the San Francisco-based startup, is looking to change the way we pay for our phone 
service. They offer simple pay-as-you-go plans for data, text, and calls on LTE devices. Charge 
runs lean with a small team of five. This mighty team of five is working on a solution to rival the telecommunications giants. 
Their mission to provide simple mobile phone service that puts consumers in control is no small undertaking. 
With their ambitious goal in mind, they quickly realized that their team couldn’t afford any missteps.

![](/images/blogimages/Charge-customer-story/person-on-phone-2.jpg)

Charge needed to find a distributed version control solution that would help improve their engineering workflow, speed up 
their development process, and withstand industry security requirements. After looking into a number 
of different tools across the market, the team decided that GitLab Community Edition was the 
best solution for their needs. Since Charge migrated to GitLab they have already 
seen decreased development times and increased confidence in the code they’re deploying.  

## Looking for a secure alternative

Before GitLab, Charge was using raw git with git+ssh for access. They didn’t have a web interface for repo management 
or code review. Feeling like they had the opportunity to drastically improve their engineering workflow, 
the Charge team decided to look for a product to support their 25 repositories and 5 developers. However, 
the team could not go with just any solution. They needed one with a specific set of features that would 
align with their strict industry regulations.

Charge’s CTO, Chris Goddard, explains: "When working with telecom carriers like we do, there are legal 
requirements concerning customer information (called CPI) and the software that interacts with customer 
information that we must adhere to.” The need to keep customer information secure is one of the primary 
reasons that Chris considered GitLab’s self-hosted Community Edition. Chris added, "privacy is very important 
to us generally. And we like to be in control of the software that we use for system-critical work. Being able 
to self-host things that store important company secrets is paramount, which is why we love GitLab!" 

## Decreased deployment time and increased confidence

GitLab is currently Charge's sole code review tool, hosting all of their 25 internal git repositories. 
The team runs GitLab using an on-host database (Postgres), with daily backups. Charge uses 
Google OAuth integration, a feature that was crucial to the team when they were searching for 
the right software for their needs. The five-strong development team also use both webhooks 
and git hooks for integration with their build server. 

For Chris, Charge’s CTO, GitLab has been an amazing revelation to the team’s engineering workflow. 
Chris comments on the positive changes that he and the team have witnessed, stating that they are 
extremely pleased with their new code review process. He continues: "But the biggest change was in deployment time. 
GitLab allowed us to easily integrate with our build server and automate deployments. Before, deployment 
was an hour-long disaster-prone mess. After, we've got it down to a couple minutes and can deploy with confidence."

## Conclusion

GitLab Community Edition is enabling Charge to meet their goal of simplifying data for mobile devices. 
GitLab is helping Charge to take on large telecommunications providers by offering a secure and consumer-friendly
pay-as-you-go model. Thanks to GitLab CE, Charge is experiencing an improved engineering workflow with dramatically faster 
deployment time and adherence to strict industry security requirements.  

## Tell us your story

Is your team using Gitlab? We’d love to hear from you.
Email us at community@gitlab.com if you’re interested in sharing.
