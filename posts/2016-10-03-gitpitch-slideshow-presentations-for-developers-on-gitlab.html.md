---
title: "GitPitch Slideshow Presentations for Developers on GitLab"
author: David Russell
author_twitter: gitpitch
categories: integration
image_title: '/images/blogimages/gitpitch-slideshow-presentations-for-developers-on-gitlab/cover.png'
description: "Learn how PITCHME.md can help you present your ideas and code to any audience."
twitter_image: '/images/tweets/gitpitch-slideshow-presentations-for-developers-on-gitlab.png'
---

Today I would like to introduce [GitPitch](https://gitpitch.com), a slideshow presentation service for developers on [GitLab](https://about.gitlab.com).
GitPitch supports building, sharing, and presenting online and offline slideshow presentations. Presentations powered entirely by Markdown and Git.

<!-- more -->

As developers and advocates, we often need to communicate with diverse audiences about our code.
We find ourselves needing to present everything from designs and best practices, to code snippets and complete frameworks.
Our audiences include colleagues, clients, customers, end-users, and sometimes meetups and conferences.

With GitPitch, we no longer need to turn to external toolsets like Keynote or Powerpoint to prepare for these kinds of presentations.
In fact, now the only tools we need are the tools we live in, our preferred code editor and a GitLab repo.
And with these tools we can quickly create compelling, responsive, online and offline slideshow presentations.

![Slideshow-Master](/images/blogimages/gitpitch-slideshow-presentations-for-developers-on-gitlab/slideshow-master.jpg){: .shadow}

## How GitPitch Works

As GitLab users, we are already familiar with the convention of adding a **README.md** to our projects.
GitPitch introduces a new convention for GitLab users, called **PITCHME.md**.

As soon as we add a **PITCHME.md** markdown file to the root directory of our GitLab.com project, GitPitch instantly creates an online slideshow presentation based on the content in that file.
That slideshow presentation is then automatically made available at its public URL:

```
https://gitpitch.com/user/project/branch?grs=gitlab
```

Here `user` and `project` matches our GitLab.com user and project names respectively and `branch` matches the repository branch where we commited our **PITCHME.md** file.
Note, the `/branch` can be omitted from the slideshow URL if we are referencing the `master` branch.

## GitPitch In 60 Seconds

To experience just how simple it is to create a GitPitch slideshow presentation follow along with this short tutorial.

### Step 1: Create **PITCHME.md**

Using the [GitLab web editor](https://gitlab.com/help/user/project/repository/web_editor.md), or your preferred code editor, create a file called **PITCHME.md** in the root directory of your repo, then add and save the following Markdown content:

```
# Flux

An application architecture for React

#HSLIDE

### Flux Design

- Dispatcher: Manages Data Flow
- Stores: Handle State & Logic
- Views: Render Data via React

#HSLIDE

![Flux Explained](https://facebook.github.io/flux/img/flux-simple-f8-diagram-explained-1300w.png)
```

Before moving on to the next step it's worthwhile to note the following:

1. The **PITCHME.md** file name is case sensitive.
1. The **PITCHME.md** file content is [standard Markdown](https://daringfireball.net/projects/markdown/syntax).
1. The `#HSLIDE` markdown fragment acts as a delimiter between slides.

Using `#HSLIDE` is another GitPitch convention, acting as a delimiter to denote the separation between content on different slides in your presentation.
You can use [custom delimiters](https://github.com/gitpitch/gitpitch/wiki/Custom-Slide-Delimiters) if you prefer.
For this example, when GitPitch processes the Markdown content it will result in a simple presentation with just three slides.


### Step 2: Commit **PITCHME.md**

If you used the GitLab web editor in step 1 then go directly to step 3.
Otherwise, manually add this file to the root directory of your Git repo and push to GitLab:

```
git add PITCHME.md
git commit -m "Added my first GitPitch slideshow content."
git push
```

### Step 3: Done!

Your GitPitch slideshow presentation is now waiting for you to share or present at its public URL.
To see a live demonstration of this slideshow presentation [click here](https://gitpitch.com/gitpitch/in-60-seconds?grs=gitlab).
Your own presentation should look a lot like this:

![Slideshow-In-60-Seconds](/images/blogimages/gitpitch-slideshow-presentations-for-developers-on-gitlab/slideshow-in-60-seconds.jpg){: .shadow}

Immediately you can [download](https://github.com/gitpitch/gitpitch/wiki/Slideshow-Offline) your slideshow for offline presentation, [print](https://github.com/gitpitch/gitpitch/wiki/Slideshow-Printing) it as a PDF document, or [share](https://github.com/gitpitch/gitpitch/wiki/Slideshow-Sharing) it on social media.
But first, you might want to apply some personal touches using GitPitch customization, the topic we'll look at next.

Note that beyond support for standard Markdown on presentation slides, GitPitch delivers a number of features tailored for developers, including support for [code blocks](https://github.com/gitpitch/gitpitch/wiki/Code-Slides), [GitHub GIST](https://github.com/gitpitch/gitpitch/wiki/GIST-Slides), [math formulas](https://github.com/gitpitch/gitpitch/wiki/Math-Notation-Slides) along with [image](https://github.com/gitpitch/gitpitch/wiki/Image-Slides), and [video](https://github.com/gitpitch/gitpitch/wiki/Video-Slides) support.
The full set of GitPitch features are documented on the [GitPitch Wiki](https://github.com/gitpitch/gitpitch/wiki).
To see a live slideshow demonstration of these features try out the GitPitch [Kitchen Sink](https://gitpitch.com/gitpitch/kitchen-sink?grs=gitlab).


## GitPitch Customization


As with any presentation, a GitPitch presentation not only needs to capture and render compelling content, it also needs to be able to reflect the style, image or brand of the associated project, product or organization.
To help us develop a strong visual identity for our slideshow presentations, GitPitch offers six distinct visual themes out-of-the-box.
See the [GitPitch Themes](https://github.com/gitpitch/gitpitch/wiki/Theme-Setting) Wiki page to learn more.

![Slideshow-Night-Theme](/images/blogimages/gitpitch-slideshow-presentations-for-developers-on-gitlab/slideshow-night-theme.jpg){: .shadow}

Building on these base themes we can further [customize the look and feel](https://github.com/gitpitch/gitpitch/wiki/Slideshow-Settings) of our slideshow presentations using background images, our own logo, and even custom CSS to bend the pixels to our needs.

![Slideshow-Custom-Bg](/images/blogimages/gitpitch-slideshow-presentations-for-developers-on-gitlab/slideshow-custom-bg.jpg){: .shadow}

## GitPitch and GitLab Workflow

The **PITCHME.md** markdown for our slideshow presentation becomes just another file in our GitLab project repo.
Therefore all of the benefits we currently enjoy when working with GitLab Workflow apply equally when developing our slideshow presentations.

Given GitPitch can render a slideshow presentation for any branch within a public GitLab repo, using feature branches also offers an excellent way to customize a presentation's content for different target audiences. For example:

1. Branch to tailor code snippets for a Scala rather than Java audience.
2. Branch to adjust the presentation focus for a dev-ops audience.
3. Branch to emphasize participation of a partner or customer for a specific conference.

Some common, in-person workflows are also greatly improved when working with GitPitch presentations.
For example, how often have you heard this simple request following a successful presentation:

> Can you please send me your slides?

If our presentation lives outside of our GitLab project it is very easy to misplace or forget to follow up.
With GitPitch, a simple answer is always at hand:

> The slideshow presentation is part of the project on GitLab, just click on the [GitPitch Badge](https://github.com/gitpitch/gitpitch/wiki/Slideshow-GitHub-Badge) found in the project **README.md**.


## Going Faster from Idea to Presentation


GitLab champions new, modern development tools and practices that foster collaboration and information sharing to help developers go [faster from idea to production](/2016/08/22/announcing-the-gitlab-issue-board/#gitlab-from-idea-to-production).
GitPitch embraces and extends this approach by helping individuals, teams and organizations to promote, pitch and present their ideas and code to ever wider audiences.

Note, by default the GitPitch service on [GitPitch.com](https://gitpitch.com) integrates with [GitLab.com](https://gitlab.com).
If you are interested in using GitPitch with your own GitLab server see [this note](https://github.com/gitpitch/gitpitch/wiki/Git-Repo-Services) on the GitPitch Wiki.

Like GitLab, GitPitch itself is an [open source project](https://gitlab.com/gitpitch/gitpitch), built on some wonderful open source software.
See the [GitPitch website](https://gitpitch.com/#gitpitch-about) for details. And remember, getting started couldn't be easier.
GitPitch requires no sign-up. And no configuration. Just add **PITCHME.md** ;)

## About Guest Author

David Russell is a freelance developer, consultant for-hire, [open source contributor](https://github.com/onetapbeyond) and the creator of [GitPitch](https://gitpitch.com).
You can reach David on Twitter [@gitpitch](https://twitter.com/gitpitch).
