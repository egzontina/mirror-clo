---
title: "Feature Highlight: User preferences to customize GitLab behavior"
date: 2015-11-05
author: Drew Blessing
author_twitter: drewblessing
---

In GitLab 8.0 we worked hard to refine the UI so it is really enjoyable
to use. After the release we received a lot of positive feedback. However,
users requested a few customizations to help the UI better fit their daily use.
We considered all of this feedback and are happy to share some new user preferences
in GitLab 8.1.

Among these new user preferences are the ability to choose between a fluid or fixed
width layout and the option to choose activity as the default dashboard instead of
the project list.

<!-- more -->

## Layout width

GitLab 8.0 introduced a fixed width layout in an attempt to make content
easier to follow. The fixed width layout on large monitors
will have a gray negative space on either side of content.

![Fixed width wide screen](/images/user_preferences/fixed_width_wide_screen.png)

Some users still like the idea of the fluid layout and now they
have a choice.

From the GitLab dashboard, go to 'Profile Settings' and then 'Preferences'.

Scroll down to the 'Behavior' section and choose 'Fluid' from the 'Layout width'
dropdown. Save changes and you will now take full advantage of your large screen.

![Fluid width wide screen](/images/user_preferences/fluid_width_wide_screen.png)

## Default Dashboard

Another change in GitLab 8.0 was that the old dashboard containing both the
project list and activity were split out in to two different pages - 'Projects'
and 'Activity'. By splitting them out we are able to add some additional scopes
to each page, such as a tab for starred projects and starred projects' activity.
Beginning in 8.1 users can choose between four different default dashboard views.

From the GitLab dashboard, go to 'Profile Settings' and then 'Preferences'.

Scroll down to the 'Behavior' section and choose one of four options from the
'Default Dashboard' dropdown.

* **Your Projects** This view is the default and shows a list of all projects in which you are a
member.
* **Starred Projects** This view shows a list of projects that you have starred. If you are a member
of many projects you may want to star a few so this list will display your
most common projects.
* **Your Projects' Activity** This view shows activity for all projects in which you are a member. This is
similar to the previous activity on the dashboard prior to 8.0.
* **Starred Projects' Activity** This view will show activity only for those projects that you star. Again,
if you are involved in many projects you may want to star a few so your
activity is not so crowded.

## Project view

Although not new for GitLab 8.1, it's also worth sharing the 'Project view'
user preference. By default, a project's main page will display the Readme
file. This is great for first-time visitors who are not familiar with the project.
However, project members that frequent this page may be more interested in the
recent activity.

From the GitLab dashboard, go to 'Profile Settings' and then 'Preferences'.

Scroll down to the 'Behavior' section and choose either 'Readme' or 'Activity'
in the 'Project view' dropdown.

### Readme View

![Project Readme View](/images/user_preferences/project_readme.png)

### Activity View

![Project Activity View](/images/user_preferences/project_activity.png)

## Documentation

We hope these new user preferences allow users to customize GitLab in a way that
best fits their daily use. See the [GitLab 8.1 release post](https://about.gitlab.com/2015/10/22/gitlab-8-1-released/)
for information on upgrading so you can take advantage of these features today.
Users on GitLab.com can take advantage of these features immediately.
