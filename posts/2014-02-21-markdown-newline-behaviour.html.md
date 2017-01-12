---
title: "Markdown newline behaviour"
date: 2014-02-21 11:47
categories:
community: true
---

Currently GitLab renders line-breaks in markdown files as line-breaks.
We propose to change this behaviour to conform to the [markdown specification](http://daringfireball.net/projects/markdown/syntax#p) and only render line-breaks when you end a line with two or more spaces.
Paragraphs will continue to be rendered as before; when the text is separated by one or more blank lines.

The above change will ensure that markdown files in projects will look the way you expect them to look.
But GitLab has just one markdown engine to render [GitLab Flavored Markdown](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/markdown/markdown.md#newlines).
Since descriptions & comments in both issues & merge requests also use GitLab Flavored Markdown they will also show the new behaviour.
We think this is preferable above introducing different behaviour and rendering code for different cases.
Please let us know what you think.
