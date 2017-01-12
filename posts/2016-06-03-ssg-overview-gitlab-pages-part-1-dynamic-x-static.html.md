---
layout: post
title: "SSGs Part 1: Static vs Dynamic Websites"
date: 2016-06-03
comments: true
categories: technical overview
author: Marcia Ramos
author_twitter: virtuacreative
image_title: '/images/blogimages/ssg-gitlab-pages-series/part-1-static-x-dynamic-cover.jpg'
---

What is the difference between **static** and **dynamic** websites? What are the advantages of one over another? Which ones can I use with **GitLab Pages**? What about **Static Site Generators**?

If these questions ring a bell, this **series of posts** is for you! We are preparing three articles around the same theme "**Static Site Generators (SSGs)**".

This is **Part 1: Dynamic vs Static Websites**, where we go over their differences, pros and cons.

Stay tuned for the next two posts:

- **[Part 2: Modern Static Site Generators][part-2]**
- **[Part 3: Build any SSG site with GitLab Pages][part-3]**

**Note:** For this series, we assume you are familiar with web development, curious about Static Site Generators, and excited to see your site getting deployed with GitLab Pages.
{: .note}

<!-- more -->

----------

### What's in this page?
{:.no_toc}

- TOC
{: toc}

----

## Static and Dynamic Websites

Static websites are a combination of HTML markup (the text we see written on web pages), CSS (Cascading Style Sheets), which are the styles and layouts applied to that pages, and JavaScript, a programing language that defines their behavior (e.g., fade in and fade out, hover effects, etc.). These pages are stored as simple files, usually in a [VPS][wiki-vps], which are then served by a web server. When we type in our web browsers the URL for a web page like that, our browser (called _client_) is making an _HTTP request_ to that server, which identifies which files are being requested, and send them back to our browsers via an _HTTP response_.

Dynamic websites are more complicated than that. Besides the markup, the styles and the behavior, they do more things that our **web browsers** can identify. For example, if you are buying something online, it's easy to understand that the prices and the availability of that item are _dynamically_ recovered from some data, generally stored in _databases_. This process of recovering data and processing it _before_ responding to our browsers as web pages containing that information, is called _server-side_ processing.

Now let's take a better look into these processes to be able to understand how those things work, how important they are, and why this information is useful for us. How about starting from the beginning?

### A glance at the history

About 25 years ago, in 1990, [Tim Berners-Lee][tim-bl] [published][first-site-1990] the [first website in history][first-website]. It was a plain [static webpage] with a few tags and links. Three years later, in 1993, the birth of the [dynamic web] took place, when the [Common Gateway Interface (CGI)][wiki-cgi] was [first introduced][first-cgi]. CGI was a way to let a website run scripts on the web server and display the output.
From then on, the evolution was huge.

With the advent of processing server-side scripts, came forward the [Web Content Management Systems (WCMS)][wcms], allowing us to create and maintain databases connected to the internet. Websites with such server-side processing, which provide high-level interactivity with the user, are commonly referred as [web applications][web-apps]. [GitLab] is one of them. Some notable examples are [WordPress], [Joomla!], [Drupal], [Magento], [Ghost], and [many others][cms-list].

Besides connecting websites with databases, the dynamic web is an important asset to work with [template systems][template-sys]. By using them, developers write fast, update websites faster, and reduce mistakes (provoked by repetition).

Unfortunately, with the growing popularity of server-side based websites, came together their [vulnerabilities][common-vulnerabilities]. [Security issues] are common among them, and there are a lot of [measures][security-web-apps] we need to take to prevent attacks of uncountable natures. We need to protect our users, our site, and our server. Everything in between is subjected to attacks.

An intelligent counter-measure for avoiding those security threats and, at the same time, maintaining the benefits of templating systems, was the creation of **Static Site Generators (SSGs)**. With them, we write dynamically and publish statically.

SSGs came out on the early 2000's, with [Blosxom] in 2003, and [WebGen] in 2004. In 2008, [Tom Preston-Werner][tom-pw] released [Jekyll], by far the [most popular SSG][ssgs-list] up to now. The interest for Static Site Generators have increased considerably in the last few years, as you can see at the chart below, from [Google Trends]:

![Static Site Generators - Google Trends](/images/blogimages/ssg-gitlab-pages-series/part-1-ssg-google-trends.png)

## Server processing

Let's take a look at the image below and see [how static pages and dynamic pages][static-x-dynamic-video] communicate with the web server.

**Web server** software, such as [Apache], [NGINX] and [IIS], are able to store and read static files only: HTML, CSS and JavaScript. **Application server** software, as [PHP], [Cold Fusion] or [ASP.NET] to name a few, are the only ones able to interpret dynamic scripting.

Every browser (known as _client_) communicates with **web servers only**, via HTTP _(HyperText Transfer Protocol)_, with a URL _(Uniform Resource Locator)_.

![Static vs Dynamic server processing](/images/blogimages/ssg-gitlab-pages-series/part-1-dynamic-x-static-server.png)

**Scheme A:** the client (web browser) sends an **HTTP request** to the web server with a URL. The HTML _(HyperText Markup Language)_ file requested, stored in the web server, is immediately returned to the client with an **HTTP response**, and its content is interpreted by the browser and then displayed to the user. This is known as _client-side processing_.

**Scheme B:** the client sends an **HTTP request** to the **web server**, which dispatches the request to the **application server**. The application server may **request data from a database** first, and then **constructs the HTTP response** based on the data recovered from the database. This response is passed back to the **web server**, which returns the HTML file, constructed by the application server, to the client, via **HTTP response**. This is called _server-side processing_.

The main difference is, dynamic webpages are not served as-is by the web server as static pages are. They are constructed for every HTTP request sent by each client.

These additional steps, necessary for dynamic websites, increase the time for the user to receive the HTTP response from the server with the requested page (URL). And nobody likes waiting.

Server resources are also affected by dynamic websites as for each HTTP request, the same content needs to be constructed again and again.

There's another main advantage of static over dynamic sites. Static pages don't process user data, circumventing a major security issue related to dynamic web applications: user privacy. If the users don't send any data to your server, there is no data to be stolen.

## Conclusion

Fully-featured server providers (Scheme B) have the capability of processing server-side scripts for web applications. Their structure is more complex and naturally more expensive, whereas static web servers (Scheme A), which only handle static pages, can be maintained with less cost. With [GitLab Pages][pages] you can host your site for **free**.

The majority of web developers don't write static sites anymore. It does take a lot more time, both to write and update, than dynamic ones. But, as previously commented, SSGs resolve this problem. We can code dynamically and the SSG outputs only static webpages for us. That's the content uploaded to our web server, in this particular case, **GitLab Pages**, which runs on NGINX.

Stay tuned for the next article of this series, in which we will provide you with an overview on **[Modern Static Site Generators][part-2]**, explaining how they work, what they support, and why should we really consider using SSGs for our sites.

See you there!

Don't you have an account on [GitLab.com][sign-up] yet? Let's create one!

Follow [@GitLab][twitter] on Twitter and stay tuned for updates!

<!--
Cover image: https://pixabay.com/en/ball-http-www-crash-administrator-63527/
Other images:
App server: https://pixabay.com/en/computer-database-network-server-156948/
Web server: https://pixabay.com/en/computer-network-proxy-server-156950/
Database: https://pixabay.com/en/database-data-storage-information-309919/
Man at the computer: http://publicdomainvectors.org/en/free-clipart/Vector-illustration-of-man-at-computer/3839.html
Illustration (Static x Dynamic Websites): Marcia Ramos for GitLab, Inc.
-->

<!-- IDENTIFIERS -->

[part-2]: /2016/06/10/ssg-overview-gitlab-pages-part-2/
[part-3]: /2016/06/17/ssg-overview-gitlab-pages-part-3-examples-ci/

<!-- Alphabetical, miscellaneous -->

[blosxom]: http://blosxom.sourceforge.net/
[cms-list]:  https://en.wikipedia.org/wiki/List_of_content_management_systems
[common-vulnerabilities]:  https://www.toptal.com/security/10-most-common-web-security-vulnerabilities
[dynamic web]:  https://en.wikipedia.org/wiki/Dynamic_web_page
[first-cgi]:  //royal.pingdom.com/2007/12/07/a-history-of-the-dynamic-web/
[first-site-1990]:  http://www.telegraph.co.uk/technology/internet/12061803/The-worlds-first-website-went-online-25-years-ago-today.html
[first-website]: http://info.cern.ch/hypertext/WWW/TheProject.html
[GitLab]: https://about.gitlab.com/ "GitLab.com, GitLab CE, GitLab EE"
[google trends]: //www.google.com.br/trends/explore?hl=en-US#q=%22static+site+generator%22&cmpt=q&tz=Etc/GMT%2B3&tz=Etc/GMT%2B3
[Jekyll]: https://jekyllrb.com
[security issues]: https://www.cs.columbia.edu/~smb/classes/f06/l09.pdf
[security-web-apps]: https://msdn.microsoft.com/en-us/library/zdh19h94.aspx
[ssgs-list]: https://staticsitegenerators.net/
[static webpage]: https://en.wikipedia.org/wiki/Static_web_page
[static-x-dynamic-video]: https://www.youtube.com/watch?v=zC03bcuVZHY
[template-sys]: https://en.wikipedia.org/wiki/Web_template_system
[tim-bl]: https://en.wikipedia.org/wiki/Tim_Berners-Lee
[tom-pw]: https://en.wikipedia.org/wiki/Tom_Preston-Werner
[wcms]: https://en.wikipedia.org/wiki/Web_content_management_system
[web-apps]: https://en.wikipedia.org/wiki/Web_application
[webgen]: http://webgen.gettalong.org/news.html#webgen-0-1-0-released
[wiki-cgi]:  https://en.wikipedia.org/wiki/Common_Gateway_Interface
[wiki-vps]: https://en.wikipedia.org/wiki/Virtual_private_server "Virtual Private Server"
<!-- GitLab -->

[pages]: https://pages.gitlab.io
[sign-up]: https://gitlab.com/users/sign_in "Sign Up!"
[twitter]: https://twitter.com/gitlab

<!-- Server software -->

[Apache]: //www.apache.org/
[NGINX]: https://www.nginx.com/
[IIS]: //www.iis.net/
[PHP]: //php.net/
[Cold Fusion]: https://www.adobe.com/products/coldfusion/
[ASP.NET]: http://www.asp.net/

<!-- CMS -->

[drupal]: https://www.drupal.org/
[ghost]: https://ghost.org/
[joomla!]: https://www.joomla.org/
[magento]: https://magento.com/
[wordpress]: https://wordpress.org/
