This style guide is specifically for blog posts on GitLab.com. 

Refer to our [official documentation style guide](http://doc.gitlab.com/ce/development/doc_styleguide.html#documentation-styleguide) which covers formatting. 
Everything included in this guide is an addendum or blog-specific override to that guide. 

Table of contents

- [Philosophy](#philosophy)
- [Header](#header)
- [Structure](#structure)
- [Markup and formatting](#formatting)
- [Person](#person)
- [Formality](#formality)
- [Images](#images)
- [GitLab Specific Terms and Points](#gitlab-specific-terms)

## Philosophy

Even before writing, GitLab articles start with two things:

- A target audience. Who is this reader? What is their prior experience and main problem?
- An objective. What will the reader be able to do by following this tutorial?
Why should they continue reading?

Right from the start of the article make those things clear to the reader as 
concisely as possible before the break or jump.  

Be clear in the article who the audience is, what their experience is and what their 
current problem is. 
Use text to describe the problem the article is solving because this will aid in searching.
State the problem as the reader might experience it.
Use error messages they would have encountered.

Be clear in the objective for your article. 
What will notivate the reader to continue reading the article? 
What will they gain from reading the article?

Long lists of steps are hard to follow and refer back to. 
Chunk tasks into steps in the article and use headings for these steps. 

The article should be thorough. 
If all the prerequisite steps cannot be covered in the scope of the article,
link to another GitLab article or documentation where all the prerequisites
are covered. 
If that article or documentation doesn't yet exist, considering writing *that* 
article or contributing *that* documentation first. 

Some information should be left to documentation. 
Documentation should be the map. 
The articles and tutorials should be guided tour of key landmarks. 
Details about requirements, supported technologies, and so forth. 
If it's not already in documentation please contibute it to GitLab CE or EE. 
Alternatively, make an [issue for missing documentation](https://gitlab.com/gitlab-com/doc-gitlab-com).
This is more sustainable, since documentation is maintained. 

**Important security point:** Do not expose your personal details by using your real tokens or 
security credentials.
Use placeholders such as `[project's CI token]` stub instead.

## Header

Make sure the date of the post matches the filename on the post.
The timestamp is the server time, or GMT +1.
The time indicated on the post will control the order of the posts.

```
---
layout: post
title: This is the title
date: 2016-03-21 17:00
comments: true
author: Firstname Lastname
author_twitter: userID
image_title: /images/unsplash/cat-in-the-box.jpg
---
```

## Structure 

This is an example outline of a typical article. 

- Introduction. State the problem, audience and purpose of the article. 
- `<!-- more -->` break
- Use h2 ## for headings and subheadings in the articles.
- Concepts they need to understand
- Configuration or set up required to begin the tutorial
- Tutorial broken down into steps. 
- Steps are broken down into tasks.
- What did you learn during writing this, teach the user something interesting.
- Conclusion to summarize the article

If the article is part of a series, make sure to link back among all articles
in the series to each one after they get published. 

**The break**: In blog posts use the more comment line to mark where the jump is. 

> `<!-- more -->`

This will break the introduction which gets displayed on the [blog listing page][blogpage].

## Formatting

See references directly in the documentation style guide. Of particular use:

- [Writing text][doctext]
- [Formatting text][docformatting]
- [Links in text][doclinks]

Code blocks should be formatted with a line space before the code block and
three back ticks before and after the code block

<pre>

 ```
  code 
 ```
 
</pre>

## Person

The point of view or person you write in will depend on the content you are writing. 

Generally in blog posts, it's normal to write from first person singular point of view. 
"I've found" or "I think" are common when writing an opinion piece.  
If you are writing an opinion piece, use first person. 

However in technical tutorials we should use first person plural "we" and second person "you." 

Instead of... 

> In this post I will..  

Use

> In this post we will... 

## Formality

GitLab tutorial blog posts should be written in a friendly style, but free of 
jargon or memes.
Avoid using cultural idioms and references that could exclude or confuse readers. 

## Images

### Creating images

Static images should be used to illustrate concepts, provide diagrams, elements of the UI or orient the reader.
Images should not be used to render commands or configuration which would prevent
someone being able to copy and paste. 

Animated GIFs can be used sparingly where you need to show a process or some event
happening over the course of time or several actions.
Animated GIFs should not replace text descriptions or instructions. 

### Preparing images

For the blog, images should also be formatted in a 700 x 490 pixel *proportion* 
so the image doesn't get clipped when displayed as a lead image in the blog list.
Compress the image, for example using [TinyPNG.com][tinypng] or any other image editor.

### Where to place images

Images used to illustrate articles should be placed in the `/source/images/blogimages` directory. 
Unless they are 'free to use' lead images from [Unsplash][unsplash]. 
Those should be placed in the `/source/images/unsplash` directory.

### Including images in the document

For including the image in the markdown text, refer to "Inside the document"
guidelines in the [Documentation style guide][docimages].

## GitLab Specific Terms 

**GitLab** is always spelled with a capital L. 

If you're writing about the CI feature, it's not a separate product. 
For example don't refer to "Gitlab CI's runner" please refer to "GitLab Runner."

**GitLab, Inc.** is the company. 

We refer to **GitLab team members** instead of staff. 

************

Credit where credit is due: Some of the guidelines are inspired by the 
[Digital Ocean tutorial style guide][dostyleguide].

[blogpage]: https://about.gitlab.com/blog
[unsplash]: https://unsplash.com/
[tinypng]: https://tinypng.com/
[doctext]: http://doc.gitlab.com/ce/development/doc_styleguide.html#text 
[docformatting]: http://doc.gitlab.com/ce/development/doc_styleguide.html#formatting
[doclinks]: http://doc.gitlab.com/ce/development/doc_styleguide.html#links
[docimages]: http://doc.gitlab.com/ce/development/doc_styleguide.html#images
[dostyleguide]: https://www.digitalocean.com/community/tutorials/how-to-write-an-article-for-the-digitalocean-community)