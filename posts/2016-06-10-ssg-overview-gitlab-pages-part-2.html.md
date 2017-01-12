---
layout: post
title: "SSGs Part 2: Modern Static Site Generators"
date: 2016-06-10 08:00:00
comments: true
categories: technical overview
author: Marcia Ramos
author_twitter: virtuacreative
image_title: '/images/blogimages/ssg-gitlab-pages-series/ssg-overview-gitlab-pages-cover.jpg'
---

What are Static Site Generators? What are they for? Why should I use them? Do they have
limitations? How can I use them with **GitLab Pages**?

If these questions ring a bell, this **series of posts** is for you! We are preparing
three articles around the same theme "**Static Site Generators (SSGs)**".

This is **Part 2: Modern Static Site Generators**, where we provide you with an overview on
the subject.

The previous post was [**Part 1: Dynamic x Static Websites**][part-1], where we briefly explained
the differences between them, and their pros and cons.

Stay tuned for the next post: **[Part 3: Build any SSG site with GitLab Pages][part-3]**!

**Note:** For this series, we assume you are familiar with web development, curious about
Static Site Generators, and excited to see your site getting deployed with GitLab Pages.
{: .note}

<!-- more -->

----------

### What's in this overview?
{:.no_toc}

- TOC
{: toc}

----

## Benefits of Modern Static Site Generators

Static Site Generators (**[SSGs]**) are software created to automate web development to
**output** static sites from **dynamic** writing. So, we code dynamically and publish
statically. No pain, all gain.

The most fascinating thing of any SSG is the ability to code fast, save money (on web
hosting), and incredibly [decrease the page loading time][page-load]
(compared to server-side dynamic webpages). Also, if we have a lot of visitors at the same
time, our [static sites have less chance to crash][server-crash] due to server overload
[than dynamic ones][site-down].

**Note:** if you want to know more about it, read the introductory article for this series:
"[SSGs Part 1: Static x Dynamic Websites][part-1]".
{: .note}

## Structure of SSGs

The structure of SSGs is a combination of features to make static sites development faster
and less repetitive. Let's take a quick look at the list below, then describe them one by one.

- Environment
- Template engine
- Markup language
- Preprocessors
- Directory structure

### <i class="fa fa-terminal fa-fw" style="color:rgb(226,67,41); font-size:.85em"></i> Environment
{: #environment}

The **environment**, also called **platform**, consists essentially on the [programming language]
the SSG was written in. It will make difference on the configuration, customization, and performance
of the SSG. Examples: [Ruby], [Python], [Node JS][node].

<a name="template-engine"></a>

### <i class="fa fa-cogs fa-flip-horizontal fa-fw" style="color:rgb(107,79,187); font-size:.85em" aria-hidden="true"></i> Template engine
{: #template_engine}

The **template engine** is very important we understand, since all the dynamic structure of our sites
will depend on that. It's essential that we choose an SSG with a [templating system][template-sys]
that we can use comfortably. Examples: [Liquid], [Haml] and [Slim]  (Ruby), [Twig]  (PHP),
[Swig]  (JavaScript).

To give you a picture, let's see an example for an HTML file, in which we are using the
[Liquid Templating Engine][liquid]:

```html
<!DOCTYPE html>
<html lang="en">
	{% include head.html %}
<body>
	{% include header.html %}
	<main class="content">
		{{ content }}
	</main>
	{% include footer.html %}
</body>
</html>
```

As you may have guessed, we have three files for the content that **repeats** sitewide (head, header
and footer), which are included to every page using this template. The only thing that is different
is the `{{ content }}` of that page, which is written in a separate file, and also included
dynamically to the template with this tag. Finally, all the files will be **compiled** to regular
HTML pages **before** being stored in the web server. This process is called **build**. GitLab Pages
**builds** any SSG.

_Advantages over flat HTML_

- Minimize typography errors ("typos"): all files are considerably reduced, improving readability
- Avoid repetition: every block repeated sitewide would be included to every page, equivalently
- Update faster: if we change something in the file `footer.html`, it will affect the entire site

### <i class="fa fa-pencil fa-flip-horizontal fa-fw" style="color:rgb(226,67,41); font-size:.85em"></i> Markup language
{: #markup-language}

**[Markup language]** is a system to write documents making them somehow syntactically distinguishable
from text. [Lightweight markup languages][wiki-markup] have a simplified and unobtrusive syntax, designed to be
easily written within any text editor. That's what we'll use to write our content.

The majority of SSGs use **markdown engines** for this purpose. But there are many more
lightweight markup languages used likely, such as [AsciiDoc], [Textile] and [ReStructuredText].

Among those SSGs which use markdown markup, generally we are allowed to choose which markdown engine
we want to use. It is setup on the site configuration.
For example, in Ruby there are a handful of Markdown implementations:
[Kramdown], [RDiscount], [Redcarpet], [RedCloth].

A blog **post** or a **page** written in [markdown] will most likely start with a **front matter**
section containing information about that page or post, and then comes the content just below it.
This is an `example.md` file used in a [Jekyll] site, and also an `example.html.md` file for
a [Middleman] site:

```markdown
---
# front matter (between three-dashes block)
title: "Hello World" # post or page title
date: YYYY-MM-DD HH:MM:SS # date and time, e.g. "2016-04-30 11:00:00"
author: "Foo Bar" # a common variable to exemplify
---

# An h1 heading

Some text.
```

The front matter variables, which are `title`, `date` and `author` for our example above,
can be called with template tags all over the site. With Liquid, if we write:

```liquid
<h2>Title: {{ page.title }}</h2>
<p>Date: {{ page.date }}</p>	 
<p>By {{ page.author }}</p>
```

The output would be:

```
<h2>Title: Hello World</h2>
<p>Date: 2016-04-30 11:00:00</p>
<p>By Foo Bar</p>
```

The content for our example would output simply:

```html
<h1>An h1 heading</h1>
<p>Some text.</p>
```

### <i class="fa fa-puzzle-piece fa-fw" style="color:rgb(107,79,187); font-size:.85em" aria-hidden="true"></i> Preprocessors
{: #preprocessors}

The **preprocessors** are made to speed up our development process too. They simplify
the way we code, and then compile their own files into standard ones. Examples: [Sass]
and [Stylus] for CSS, [CoffeeScript] for JavaScript.

Again, just to give you a picture, check a CSS code block written in CSS directly, and
the other written in Sass:

CSS:

```css
h1 {
  color: #333;
  padding-top: 30px;
}
p {
  color: #333;
}
```

Sass:

```sass
$clr = #333
h1
  color: $clr
  padding-top: 30px
p
  color: $clr
```

In a large-scale styling, saving all curly brackets `{ }` and semi-colons `;` makes a lot
of difference for who is typing. Also, with Sass variables (e.g., `$clr` above), we can
define some standards and apply them all over our stylesheets. In the end, everything
will be compiled to regular CSS. There are more interesting features and advantages of 
preprocessors, but that's not in focus on this post. 

By the way, the given Sass example will be compiled exactly to the CSS code above it.

### <i class="fa fa-folder-open-o fa-fw" style="color:rgb(226,67,41); font-size:.85em"></i> Directory structure
{: #directory-structure}

The **directory structure** is different for each SSG. It's important to study the file
tree before we start working with an SSG, otherwise we might face odd build errors that
we won't understand solely because we didn't use its structure accordingly.
Examples: [Hexo structure][hexo-struc], [Middleman structure][middle-struc],
[Jekyll structure][jekyll-struc]. So, just make sure you add new files to the correct directories.

## SSGs built-in features

In addition to their standard components, there are also a number of built-in features
that make building and previewing static sites easier - and faster. For example:

- Most of SSGs have a pre-installed server for previewing the sites locally
- Some of them also contain in their installation package a LiveReload plugin, so we
don't need to refresh the page in our browser every time we save it
- Most of them provide us with built-in compilers for their supported preprocessors

## Blog-Aware SSGs

One of the most attractive features for the majority of modern SSGs is the ability to manage
blog content without the need of storing posts, or post contents,
in databases or in server-side-only processed files.

A blog-aware website generator will create blog-style content, such as lists of content in
reverse chronological order, archive lists, and other common blog-style features.
How would an SSG do that?

With their file tree and their template engine. The file tree defines the specific
directory for `posts` and the template engine calls the posts dynamically.

With a `for` loop through the posts, they can be displayed in a single page, as
illustrated below (with [Liquid]):

```liquid
  <ul>
    {% for post in site.posts %}
      <li>
        <span>{{ post.date }}</span>
        <h2>
          <a class="post-link" href="{{ post.url }}">{{ post.title }}</a>
        </h2>
      </li>
    {% endfor %}
  </ul>
```

This code means that, **for each post** within the **site posts**
(`{% for post in site.posts %}`), all of them would be displayed as items of an
unordered list of posts, within links for their respective paths.

Of course, we can adapt the HTML structure according to our needs. Also, we can use
the blog-aware structure to create different kinds of dynamic insertion. For example,
we could use them to display multiple things within the same category, as a collection
of photos, books, etc. So, each time we add a new item, the SSG uses it's template
engine to bring our collections together.

## Supported content

Static servers fully support any language or script interpreted by browsers, known as
[**client-side** processing][part-1]. Let's just remember that a static site is essentially
composed of three components: the structure (HTML), the layout and styles (CSS),
and the behavior (JavaScript).

_Supported languages and file extensions_

- Common file extensions: `.html` / `.css` / `.js` / `.xml` / `.pdf` / `.txt`
- Common media files: [images], [audio], [video], [SVG]

_Supported interactive services (examples)_

- Commenting Systems (e.g., [Disqus], [Facebook Comments], and [many others][comment-systems])
- Live Chat (e.g., [JivoChat], [Tawk.to])
- [PayPal Payments Standard]
- [Facebook Social Plugins]
- [Twitter Kit]
- Google Apps (e.g., [Analytics], [Adwords], [AdSense], etc)
- Site Search Engine (e.g., [Google Search][google-cse], [Swiftype], [Tipue])
- Mailing lists and blog subscriptions (e.g., [MailChimp])

_Supported utilities (examples)_

- HTML/CSS/JS frameworks and libraries. E.g, [Bootstrap], [Foundation], [Normalize], [Modernizr], [Skeleton], [jQuery], [HTML5 Boilerplate][html5-boiler], [Animate.css]
- [Schema.org] markup, making [search engines][schema-seo] to understand our site content better. This is [one of the numerous SEO][seo] techniques
- [Sitemaps], important for [SEO][seo-sitemaps] too. E.g., [Jekyll Sitemap plugin][jek-sitemap], [Middleman Sitemap][middle-sitemap], [Hexo Sitemap plugin][hexo-sitemap]

## Limitations of SSGs

We've just described what we **can do** with SSGs. Now let's see what we **cannot**.

- Register users
- Have admin access
- Send emails via `mail()` function
- Use any server-side language or script

These kinds of actions depend necessarily on server-side processing, which are not handled
by static-only web servers, as we explained in the [first post of this series][part-1].

### Overcoming the limitations

_User Authentication_

Despite not having the ability to register users, nor having admin access for ourselves,
with tools like [Firebase] we can power-up our static site with
[user authentication][firebase-user-auth]. Find more [cool stuff][firebase-cool-stuff] here,
from the same source.

_Content management_

We can edit the content of our SSGs directly from the web browser with [Teletext.io]. We can't
create new pages, but we can edit pages' content easily. Follow the [Teletext.io tutorial] to learn
how to implement this for your own website.

_Contact Forms_

Yes, we can offer contact forms in our static websites. We can't process the **server-side**
script in our static-server, but there are some third-party services we can use for that.
For example, you can try [Formspree], [FormKeep], [Wufoo], [FoxyForm], [Google Forms] or any
other related service . However, if you want to take control over your mail script, you can
try the [parse method with SendGrid][sendgrid-parse].

_JavaScript disabled_

Everything based on JavaScript is allowed to be added to our static sites. However, if
JavaScript is disabled on the user's browser, those scripts will not work. But there is
something we can do to minimize this issue. We can add a [`<noscript>`][no-script] tag
to our web pages, containing a message that will be displayed only if JavaScript disabled:

```html
<noscript>Please enable JavaScript on your browser for a better experience with this website!</noscript>
```

## Conclusion

Hopefully now you understand the logic of Static Site Generators, how we can use them wisely,
and what we can and cannot do with them. Dynamic websites are great, for sure. 
But if we don't need all their functionality, SSGs are certainly wonderful alternatives.

In the [third post][part-3], which is the last chapter of this series, we will bring you a lot of examples
for SSGs already running on GitLab Pages. Therefore, we're confident you'll be able to see and 
understand different GitLab CI configurations, and create your own.

We already have prepared a bunch of SSGs example projects, you'll find them in the
[GitLab Pages][ci-examples] official group. You are very welcome to [contribute][pages-contribute]
with new SSGs.

Don't you have an account on [GitLab.com][sign-up] yet? Let's create one! Remember, we can
use GitLab Pages to [build any SSG][post-pages] for us and host it for free!

Follow [@GitLab][twitter] on Twitter and stay tuned for updates!

### Useful links

- [GitLab Pages Quick Start][pages] - learn how to get started with GitLab Pages by forking an existing project
- [GitLab Pages on GitLab.com][post-pages] - learn how to setup a GitLab Pages project from strach
- [GitLab Pages Docs][pages-ee] - the official documentation with all the details you might be interested in
- [SSGs Part 1: Static vs Dynamic Websites][part-1] - the first post of this series
- [SSGs Part 3: Build any SSG site with GitLab Pages][part-3] - the third post of this series

<!-- Cover image: https://unsplash.com/photos/6g0KJWnBhxg -->

<!-- IDENTIFIERS -->

<!-- Alphabetical, miscellaneous -->

[part-1]: /2016/06/03/ssg-overview-gitlab-pages-part-1-dynamic-x-static/
[part-3]: /2016/06/17/ssg-overview-gitlab-pages-part-3-examples-ci/

[AdSense]: https://support.google.com/adsense/answer/181950
[Adwords]: https://support.google.com/adwords/answer/6331314
[Analytics]: https://developers.google.com/analytics/devguides/collection/analyticsjs/
[AsciiDoc]: https://en.wikipedia.org/wiki/AsciiDoc
[audio]: http://www.w3schools.com/html/html5_audio.asp
[comment-systems]: http://brianshim.com/webtricks/add-a-comment-wall-to-your-website/
[Disqus]: https://disqus.com/
[Facebook Comments]: https://developers.facebook.com/docs/plugins/comments
[Facebook Social Plugins]: https://developers.facebook.com/docs/plugins
[firebase]: https://www.firebase.com/
[firebase-cool-stuff]: https://www.firebase.com/docs/web/examples.html
[firebase-user-auth]: http://jsfiddle.net/firebase/a221m6pb/
[FormKeep]: https://formkeep.com/
[Formspree]: https://formspree.io/
[foxyform]: http://www.foxyform.com/
[google-cse]: https://support.google.com/customsearch/answer/4513751?hl=en&ref_topic=4513742&rd=1
[Google Forms]: https://www.google.com/forms/about/
[HTML5]: http://www.w3schools.com/html/html5_intro.asp
[images]: http://vormplus.be/blog/article/using-images-in-your-html5-document
[Jekyll]: https://jekyllrb.com
[JivoChat]: https://www.jivochat.com/
[MailChimp]: http://mailchimp.com/
[Markup language]: https://en.wikipedia.org/wiki/Markup_language
[no-script]: http://www.w3schools.com/tags/tag_noscript.asp
[page-load]: https://www.smashingmagazine.com/2015/11/modern-static-website-generators-next-big-thing/#dynamic-websites-and-caching
[PayPal Payments Standard]: https://developer.paypal.com/docs/classic/button-manager/integration-guide/SOAP/ButtonMgrOverview
[programming language]: https://en.wikipedia.org/wiki/Programming_language
[Schema.org]: http://schema.org/
[schema-seo]: http://schema.org/docs/gs.html
[sendgrid-parse]: https://sendgrid.com/blog/send-email-static-websites-using-parse/
[SEO]: http://www.wordstream.com/blog/ws/2014/03/20/schema-seo
[seo-sitemaps]: http://www.webconfs.com/importance-of-sitemaps-article-17.php
[server-crash]: http://noahveltman.com/static-dynamic/
[sitemaps]: https://support.google.com/webmasters/answer/156184?hl=en
[site-down]: http://www.sitepoint.com/wordpress-vs-jekyll-might-want-make-switch/#2-wordpress-struggles-under-heavy-load
[SSGs]: https://www.staticgen.com/
[svg]: https://en.wikipedia.org/wiki/Scalable_Vector_Graphics
[swiftype]: https://swiftype.com/
[Tawk.to]: https://www.tawk.to/
[teletext.io]: https://teletext.io/
[teletext.io tutorial]: https://medium.com/teletext-io-blog/empower-your-static-generated-jekyll-site-with-instant-content-management-capabilities-82ce5569d7fb#.v2vo6pp2n
[template-sys]: https://en.wikipedia.org/wiki/Web_template_system
[tipue]: http://www.tipue.com/
[Twitter Kit]: https://dev.twitter.com/web/overview
[video]: http://www.w3schools.com/html/html5_video.asp
[wiki-markup]: https://en.wikipedia.org/wiki/Lightweight_markup_language
[Wufoo]: http://www.wufoo.com/

<!-- GitLab -->

[get-help]: https://about.gitlab.com/getting-help
[gitlab-com]: https://about.gitlab.com/gitlab-com/
[pages]: https://pages.gitlab.io
[pages-ee]: http://doc.gitlab.com/ee/pages/README.html
[pages-issues]: https://gitlab.com/pages/pages.gitlab.io/issues
[post-pages]: https://about.gitlab.com/2016/04/07/gitlab-pages-setup/
[sign-up]: https://gitlab.com/users/sign_in "Sign Up!"
[twitter]: https://twitter.com/gitlab

<!-- SSGs -->

[hexo-struc]: https://hexo.io/docs/setup.html
[jekyll-struc]: https://jekyllrb.com/docs/structure/
[Middleman]: https://middlemanapp.com/
[middle-struc]: https://middlemanapp.com/basics/directory-structure/

[jek-sitemap]: https://github.com/jekyll/jekyll-sitemap
[middle-sitemap]: https://middlemanapp.com/advanced/sitemap/
[hexo-sitemap]: https://github.com/hexojs/hexo-generator-sitemap

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
[restructuredtext]: https://en.wikipedia.org/wiki/ReStructuredText
[Ruby]: https://www.ruby-lang.org/
[Sass]: http://sass-lang.com/
[skeleton]: http://getskeleton.com/
[Slim]: http://slim-lang.com/
[Stylus]: http://stylus-lang.com/
[swig]: http://paularmstrong.github.io/swig/
[textile]: https://en.wikipedia.org/wiki/Textile_(markup_language)
[twig]: http://twig.sensiolabs.org/

<!-- Groups -->

[ci-examples]: https://gitlab.com/groups/pages
[jekyll-examples]: https://gitlab.com/groups/jekyll-themes
[middle-examples]: https://gitlab.com/groups/middleman-themes
[pages-contribute]: https://gitlab.com/pages/pages.gitlab.io/blob/master/CONTRIBUTING.md
[themes-templates]: https://gitlab.com/themes-templates
