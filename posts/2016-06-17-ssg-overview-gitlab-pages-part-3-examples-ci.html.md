---
layout: post
title: "SSGs Part 3: Build any SSG site with GitLab Pages"
date: 2016-06-17
comments: true
categories: technical overview
author: Marcia Ramos
author_twitter: virtuacreative
image_title: '/images/blogimages/ssg-gitlab-pages-series/ssg-overview-gitlab-pages-part-3-cover.jpg'
---

Which **Static Site Generators** (SSGs) can I use with **GitLab Pages**? How to setup GitLab CI to build
my SSG site? Where can I find some examples?

If these questions ring a bell, this **series of posts** is for you! We prepared three articles around
the same theme "**Static Site Generators (SSGs)**".

This is **Part 3: Build any SSG site with GitLab Pages**, where we'll show you some examples of SSGs
using distinct GitLab CI configurations, so you can understand it and adjust it to your needs.

Read through the previous posts:

- [**Part 1: Dynamic vs Static Websites**][part-1]
- [**Part 2: Modern Static Site Generators**][part-2]

**Note:** For this series, we assume you are familiar with web development, curious about Static Site Generators,
and excited to see your site getting deployed with GitLab Pages.
{: .note}

<!-- more -->

----------

### What's in this page?
{:.no_toc}

- TOC
{: toc}

----

## Build any SSG site with GitLab Pages

In the previous articles of this series on Static Site Generators, we explained the difference between
[static and dynamic websites][part-1], and provided a general [overview on Modern SSGs][part-2]. Now let's
understand how can we use them with [GitLab Pages][pages].

You can use [GitLab Pages][pages] to host and build **any** [SSG][ssgs] available!
You can also use custom domains, SSL/TLS certificates, create as many sites as you want,
and deploy your site from **private repositories**. And that's all **for free** on GitLab.com!
If you are not familiar with GitLab Pages, you might want to read the article "[Hosting on GitLab.com with GitLab Pages][post-pages]",
where you will find this information and a detailed step-by-step guide to walk you through the process.
See also the [quick start guide][pages] and the [official documentation][pages-ee] for further information.

## SSGs examples

On the following tables you can explore some examples of SSGs sites **built with
GitLab Pages** and hosted on GitLab.com. Some of them came from contributions from our community.
We'll be very happy to have [your contribution] too!

The key for [building your site with GitLab Pages][ci-for-pages] is the GitLab CI configuration
file, called `.gitlab-ci.yml`.

To make GitLab CI work for this specific purpose is necessary creating a job called `pages`, and generate your
compiled site to a `public` folder. Everything else is adjustable to your needs.

On the tables below, there are some examples we've gathered for you, organized by their respective environments.

### Environment: [Ruby]

| SSG | Website URL | Project URL | Configuration |
| --- | ----------- | ----------- | -------------- |  
| [Jekyll] | [Default Theme][j-2-web] | [Source on GitLab][j-2-pro] | [Building Jekyll 3.1.2 with Bundler][j-2-ci] |
| [Middleman] | [Default Theme][middle-prev] | [Source on GitLab][middle-proj] | [Default + Bundler `ENV=PRODUCTION`][middle-ci] |
| [Nanoc] | [Default Theme][nanoc-prev] | [Source on GitLab][nanoc-proj] | [Default][nanoc-ci] |
| [Octopress] | [Default Theme][octo-prev] | [Source on GitLab][octo-proj] | [Default][octo-ci] |

### Environment: [Node JS][node]

| SSG | Website URL | Project URL | Configuration |
| --- | ----------- | ----------- | -------------- |
| [Hexo] | [Hueman Theme][hexo-prev] | [Source on GitLab][hexo-proj] | [Default + `test` job][hexo-ci] |
| [Brunch] | [Default Skeleton][brunch-prev] | [Source on GitLab][brunch-proj] | [Default][brunch-ci] |
| [Harp] | [Default Theme][harp-prev] | [Source on GitLab][harp-proj] | [Default][harp-ci] |
| [Metalsmith] | [Default Theme][metal-prev] | [Source on GitLab][metal-proj] | [Default][metal-ci] |
| [GitBook] | [Default Theme][book-prev] | [Source on GitLab][book-proj] | [Default][book-ci] |

### Environment: [Python]

| SSG | Website URL | Project URL | Configuration |
| --- | ----------- | ----------- | -------------- |
| [Pelican] | [Default Theme][pelican-prev] | [Source on GitLab][pelican-proj] | [Default][pelican-ci] |
| [Lektor] | [Default Theme][lektor-prev] | [Source on GitLab][lektor-proj] | [Default][lektor-ci] |
| [Hyde] | [Default Theme][hyde-prev] | [Source on GitLab][hyde-proj] | [Default + `test` job][hyde-ci] |
| [Nikola] | [Default Theme][nikola-prev] | [Source on GitLab][nikola-proj] | [Default][nikola-ci] |

### Environment: [Go Lang][go]

| SSG | Website URL | Project URL | Configuration |
| --- | ----------- | ----------- | -------------- |
| [Hugo] | [Lanyon Theme][hugo-prev] (Default) | [Source on GitLab][hugo-proj] | [Default][hugo-ci] |

### More Examples
{: #groups}

On the following GitLab groups you can find even more examples.

| Group | Environment | SSGs |
| ----- | ----------- | ---- |
| [Pages][ci-examples] (Official) | Ruby, Node, Python, etc. | All SSGs presented on this post |
| [Jekyll Themes][jekyll-examples] | Ruby | Jekyll |
| [Middleman Themes][middle-examples] | Ruby | Middleman |
| [Themes and Templates][themes-templates] | Miscellaneous | Miscellaneous |

**Note:** these themes, templates, and SSGs were casually chosen, and listed on this post to provide you with
some distinct GitLab CI configurations.
{: .note}

## FAQ: which SSG should I get started with?

This is a tricky question, and there is no easy answer for it. Perhaps the best way
to choose an SSG is installing three or four of them locally and give them a try. [This list][ssgs-more] might help too.

However, if you don't know where to start, and you never used any Static Site Generator
before, I suggest you to get started with [Jekyll]. Why?

- It's very well documented
- If you search the web for information you'll find plenty
- Its template engine is rigid. Meaning, there's no chance to mess up the code
- It is easy to learn

But this was merely a suggestion. There are better ways to choose. For example,
if you are a programmer, you could choose the SSG according to the language it's
written in (Ruby, JavaScript, Python, etc), picking up one you're familiar with.
If you are a PHP developer, you might want to choose an SSG with a PHP template engine. And so on.

## Getting Help

If you need some help regarding GitLab Pages on GitLab.com,
feel free to use one of [our channels][get-help]. You can also
open an issue on the [Pages][pages-issues] group.

## Conclusion

With this post we end up this series on SSGs. Hopefully, we got you inspired to start working with Static Site
Generators, and by now you comprehend what they are and how they work.

You are more than welcome to contribute with new SSGs, or with your cool themes and
templates, to the [groups](#groups) mentioned earlier.

If you already work with an SSG, please let us know which one you prefer (click on the image below).
It's a quick survey that will only take a minute, and your participation means a lot to us! [Share it] with your friends too!

[![Survey - SSGs on GitLab Pages](/images/blogimages/ssg-gitlab-pages-series/part-3-survey-ssgs-on-gitlab-pages.png)][CTA]

Don't you have an account on [GitLab.com][sign-up] yet? Let's create one!
Remember, we can use GitLab Pages to [build any SSG][post-pages] for us and host it for free on GitLab.com!

Follow [@GitLab][twitter] on Twitter and stay tuned for updates!

<!-- Cover photo: https://unsplash.com/photos/bphc6kyobMg -->

<!-- IDENTIFIERS -->

<!-- SSGs series -->

[part-1]: /2016/06/03/ssg-overview-gitlab-pages-part-1-dynamic-x-static/
[part-2]: /2016/06/10/ssg-overview-gitlab-pages-part-2/

<!-- GitLab -->

[CTA]: http://goo.gl/forms/9CKIkYqa4xQup1DF3

[about-gitlab-com]: https://about.gitlab.com/
[ci-for-pages]: https://about.gitlab.com/2016/04/07/gitlab-pages-setup/#gitlab-ci
[your contribution]: https://gitlab.com/pages/pages.gitlab.io/blob/master/CONTRIBUTING.md
[get-help]: https://about.gitlab.com/getting-help
[gitlab-com]: https://about.gitlab.com/gitlab-com/
[pages]: https://pages.gitlab.io
[pages-ee]: http://doc.gitlab.com/ee/pages/README.html
[pages-issues]: https://gitlab.com/pages/pages.gitlab.io/issues
[post-pages]: https://about.gitlab.com/2016/04/07/gitlab-pages-setup/
[Share it]: https://twitter.com/intent/tweet?hashtags=GitLabPages&original_referer=http%3A%2F%2Flocalhost%3A4567%2F2016%2F06%2F17%2Fssg-overview-gitlab-pages-part-3-examples-ci%2F&ref_src=twsrc%5Etfw&related=gitlab&text=SSGs%20on%20GitLab%20Pages&tw_p=tweetbutton&url=http%3A%2F%2Fgoo.gl%2Fforms%2F9CKIkYqa4xQup1DF3&via=gitlab
[sign-up]: https://gitlab.com/users/sign_in "Sign Up!"
[twitter]: https://twitter.com/gitlab

<!-- SSGs -->

[blosxom]: http://blosxom.sourceforge.net/
[Brunch]: http://brunch.io/
[GitBook]: https://www.gitbook.com/
[Harp]: http://harpjs.com/
[Hexo]: https://hexo.io/
[Hyde]: http://hyde.github.io/
[Hugo]: https://gohugo.io/
[Jekyll]: https://jekyllrb.com
[Lektor]: https://www.getlektor.com/
[Metalsmith]: http://www.metalsmith.io/
[Middleman]: https://middlemanapp.com/
[Nanoc]: http://nanoc.ws/
[Nikola]: https://getnikola.com/
[Octopress]: http://octopress.org/
[Pelican]: http://blog.getpelican.com/

[hexo-struc]: https://hexo.io/docs/setup.html
[jekyll-struc]: https://jekyllrb.com/docs/structure/
[middle-struc]: https://middlemanapp.com/basics/directory-structure/

[jek-sitemap]: https://github.com/jekyll/jekyll-sitemap
[middle-sitemap]: https://middlemanapp.com/advanced/sitemap/
[hexo-sitemap]: https://github.com/hexojs/hexo-generator-sitemap

[SSGs]: https://www.staticgen.com/
[ssgs-more]: https://iwantmyname.com/blog/2014/05/the-updated-big-list-of-static-website-generators-for-your-site-blog-or-wiki

<!-- Languages, preprocessors, libraries and frameworks -->

[animate.css]: https://daneden.github.io/animate.css/
[Bootstrap]: http://getbootstrap.com
[CoffeeScript]: http://coffeescript.org/
[Foundation]: http://foundation.zurb.com/
[go]: https://golang.org/
[haml]: http://haml.info/
[html5-boiler]: https://html5boilerplate.com/
[jquery]: http://code.jquery.com/
[kramdown]: http://kramdown.gettalong.org/
[liquid]: https://shopify.github.io/liquid/
[markdown]: https://en.wikipedia.org/wiki/Markdown
[modernizr]: https://modernizr.com/
[node]: https://nodejs.org/en/
[normalize]: https://necolas.github.io/normalize.css/
[Python]: https://www.python.org/
[rdiscount]: http://dafoster.net/projects/rdiscount/
[redcarpet]: https://github.com/vmg/redcarpet
[redcloth]: http://redcloth.org/
[Ruby]: https://www.ruby-lang.org/
[Sass]: http://sass-lang.com/
[skeleton]: http://getskeleton.com/
[Slim]: http://slim-lang.com/
[Stylus]: http://stylus-lang.com/
[swig]: http://paularmstrong.github.io/swig/
[twig]: http://twig.sensiolabs.org/

<!-- Groups -->

[ci-examples]: https://gitlab.com/groups/pages
[jekyll-examples]: https://gitlab.com/groups/jekyll-themes
[middle-examples]: https://gitlab.com/groups/middleman-themes
[themes-templates]: https://gitlab.com/themes-templates

<!-- Examples -->

[j-2-web]: https://jekyll-themes.gitlab.io/default-bundler/ "The default Jekyll Theme"
[j-2-pro]: https://gitlab.com/jekyll-themes/default-bundler
[j-2-ci]: https://gitlab.com/jekyll-themes/default-bundler/blob/master/.gitlab-ci.yml

[j-3-web]: https://jekyll-themes.gitlab.io/grayscale/ "A single page Jekyll template"
[j-3-pro]: https://gitlab.com/jekyll-themes/grayscale
[j-3-ci]: https://gitlab.com/jekyll-themes/grayscale/blob/master/.gitlab-ci.yml

[hugo-prev]: https://pages.gitlab.io/hugo/
[hugo-proj]: https://gitlab.com/pages/hugo
[hugo-ci]: https://gitlab.com/pages/hugo/blob/master/.gitlab-ci.yml

[middle-prev]: https://middleman-themes.gitlab.io/middleman/
[middle-proj]: https://gitlab.com/middleman-themes/middleman
[middle-ci]: https://gitlab.com/middleman-themes/middleman/blob/master/.gitlab-ci.yml

[hexo-prev]: https://themes-templates.gitlab.io/hexo/
[hexo-proj]: https://gitlab.com/themes-templates/hexo
[hexo-ci]: https://gitlab.com/themes-templates/hexo/blob/master/.gitlab-ci.yml

[brunch-prev]: https://pages.gitlab.io/brunch/
[brunch-proj]: https://gitlab.com/pages/brunch
[brunch-ci]: https://gitlab.com/pages/brunch/blob/master/.gitlab-ci.yml

[harp-prev]: https://pages.gitlab.io/harp/
[harp-proj]: https://gitlab.com/pages/harp
[harp-ci]: https://gitlab.com/pages/harp/blob/master/.gitlab-ci.yml

[metal-prev]: https://pages.gitlab.io/metalsmith/
[metal-proj]: https://gitlab.com/pages/metalsmith
[metal-ci]: https://gitlab.com/pages/metalsmith/blob/master/.gitlab-ci.yml

[lektor-prev]: https://pages.gitlab.io/lektor/
[lektor-proj]: https://gitlab.com/pages/lektor
[lektor-ci]: https://gitlab.com/pages/lektor/blob/master/.gitlab-ci.yml

[hyde-prev]: https://pages.gitlab.io/hyde/
[hyde-proj]: https://gitlab.com/pages/hyde
[hyde-ci]: https://gitlab.com/pages/hyde/blob/master/.gitlab-ci.yml

[nanoc-prev]: https://pages.gitlab.io/nanoc/
[nanoc-proj]: https://gitlab.com/pages/nanoc
[nanoc-ci]: https://gitlab.com/pages/nanoc/blob/master/.gitlab-ci.yml

[pelican-prev]: https://pages.gitlab.io/pelican/
[pelican-proj]: https://gitlab.com/pages/pelican
[pelican-ci]: https://gitlab.com/pages/pelican/blob/master/.gitlab-ci.yml

[book-prev]: https://pages.gitlab.io/gitbook/
[book-proj]: https://gitlab.com/pages/gitbook
[book-ci]: https://gitlab.com/pages/gitbook/blob/pages/.gitlab-ci.yml

[octo-prev]: https://pages.gitlab.io/octopress/
[octo-proj]: https://gitlab.com/pages/octopress
[octo-ci]: https://gitlab.com/pages/octopress/blob/master/.gitlab-ci.yml

[nikola-prev]: https://pages.gitlab.io/nikola/
[nikola-proj]: https://gitlab.com/pages/nikola
[nikola-ci]: https://gitlab.com/pages/nikola/blob/master/.gitlab-ci.yml
