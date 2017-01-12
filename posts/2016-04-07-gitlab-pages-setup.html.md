---
title: "Hosting on GitLab.com with GitLab Pages"
date: 2016-04-07 10:00:00
categories: tutorial
author: Marcia Ramos
author_twitter: virtuacreative
image_title: '/images/blogimages/gitlab-pages-setup-cover.jpg'
twitter_image: '/images/tweets/gitlab-pages-setup.png'
description: "Learn how to host your website on GitLab.com with GitLab Pages"
---

In this article we provide you with detailed information about using [GitLab Pages][pages] to
host your website for free on [GitLab.com][sign-up].

We've prepared a step-by-step tutorial on creating a new project for GitLab Pages so you won't get lost in the process.

GitLab Pages supports [static websites][wiki-static-websites] and builds **any** [Static Site Generator (SSG)][SSGs],
such as [Jekyll], [Hugo], [Hexo], [Middleman] and [Pelican].

We are assuming that you are familiar with [Git][git] and with the web development process, from creation to publishing.

<!-- more -->

----------

### What's in this tutorial?
{: .no_toc}

- TOC
{:toc}

----

## Getting Started

There are two ways of getting started with GitLab Pages: either you fork an existing project, or you create a new one for yourself.

On the [GitLab Pages Quick Start Guide][pages], which is, by the way, a site built with [Middleman],
you will find the steps for forking an existing project from a list of examples prepared for you.
There are some popular SSGs, like Jekyll, Hugo, Hexo, Bruch, etc.

However, if you want to understand the process of creating a new project from scratch, this post is for you.

On the official documentation you can learn about [GitLab Pages][pages-work], but here we will focus on the **steps** 
for creating your own project.

**Note:** [GitLab Pages was introduced in GitLab EE 8.3][pages-introduced].
It is available for [GitLab.com][sign-up] and [GitLab Enterprise Edition][gitlab-ee] users.
{: .note}

## Website Types

In general, you are allowed to create and host two sorts of websites with GitLab Pages:

1. User/Group Websites - a single site per user or group
1. Project Websites - as many sites you want

You can find out more about them on the [docs][pages-work].

### A note regarding GitLab Groups and Namespaces
{: #group-websites}

Creating a [group][doc-groups] on GitLab is very useful when you have several projects with the same subject.
A group has its own **namespace**, which is unique for each group (and for each user).

The important matter is, when you create your account on GitLab, it's better to choose a username for
yourself as a person, not as a company. You can create your "company username" later, as a group
namespace. For example, let's say your name is "John Doe" and your company is called "Foo Master".
First, register yourself as `johndoe` and later create a group called Foo Master within the namespace of
`foomaster`. This will allow you to separate your personal projects from your company ones.

If you follow this tip, you will be able to access your personal site under `https://username.gitlab.io`
and your company site under `https://groupname.gitlab.io`.

## About GitLab CI for GitLab Pages
{: #gitlab-ci}

The key to having everything up and running as expected is the [**GitLab CI** configuration file][doc-ciconfig], called `.gitlab-ci.yml`.

This file [configures][ee-yaml-ci] how your website will be built by a _[Runner][doc-config-runners]_.
It is written in [YAML], which has its own syntax, so we recommend you
follow this [quick start guide] before setting it up.
It needs to be placed at your root directory.

The most important fact is that with GitLab CI, **you** take control over your builds.
They won't be in an invisible black box where you don't know what is going on!
You can actually **see** any build running live by navigating to your project's **Pipelines > Builds > Build ID**.
You can also add any command to your script. This is far beyond useful as it allows you to do
pretty much anything you do on your local machine!

For example, you can add any [Jekyll Plugin] to your Jekyll site,
you can require any `gem` you need in your `Gemfile`, run `npm`, run `bundle` and much more.
Bottom line, it's as handy as having your own command line on your GitLab UI.

Additionally, you can have a distinct `.gitlab-ci.yml` for each repository - even for each branch.
This means you can test your script in parallel branches before pushing to your `master` branch.
If the build succeeds, you merge. If it doesn't, you can make adjustments and try building
again without messing up your `master` branch.

Before you push any `.gitlab-ci.yml` to your project, you can
validate its syntax with the tool called [CI Lint][ci-lint].
You need to be logged into your account to have access to this tool.
It's found by navigating to your project's **Pipelines**: there is a button at the top-right of your screen.

![CI-Lint](/images/blogimages/gitlab-pages/gitlab-ci-lint.png)

You can read through the [full documentation for `.gitlab-ci.yml`][ee-yaml-ci] for more information.

## Creating new GitLab Pages projects
{: #creating-new-pages-projects}

Here is an overview of the steps we'll take, assuming you already have your GitLab.com account:

1. Create a new project
1. Add the configuration file (`.gitlab-ci.yml`)
1. Upload your website content
1. Add your custom domain _(optional)_
1. Done!

## Step-by-step

Now we will go through this process step-by-step.

### Step 1: Create a new project
{: #creating-new-project}

This is as straight-forward as you can imagine:

- On your **dashboard** you will see a big green button called **+ New Project**. Click on it.
- Set the first things up:
   - **Project path** - your project's name, accessed via `https://gitlab.com/namespace/projectname`
   - **Privacy** - choose if you want your project to be visible and accessible just for you (`private`),
   just for GitLab.com users (`internal`) or free to anyone to view, clone, fork and download it (`public`)

**Note**: you can host your website on [GitLab.com][gitlab-com] even if it is stored in a private repository.
If you do so, you can have your project protected - only the static site will be visible
to the public - via "Inspect Element" or "View-Source" from their web browsers.
{: .note}

### Step 2: Add the configuration file: `.gitlab-ci.yml`
{: #add-gitlab-ci}

Now we can have some fun! Let's tell GitLab CI how to build the site.
You will see a few examples below (options A, B, and C) to understand how they work.

### Option A: GitLab CI for plain HTML websites
{: .no_toc}

In order to build your [plain HTML site][pages-ci-html] with GitLab Pages,
your `.gitlab-ci.yml` file doesn't need much:

```yaml
pages:
  stage: deploy
  script:
  - mkdir .public
  - cp -r * .public
  - mv .public public
  artifacts:
    paths:
    - public
  only:
  - master
```

What this code is doing is creating a _[job][doc-jobs]_ called _[pages][doc-contents-ciconfig]_
telling the _[Runner][doc-shared-runners]_ to _[deploy][doc-stages]_ the website _[artifacts][doc-artifacts]_
to a _[public path][doc-contents-ciconfig]_,
whenever a commit is pushed _[only][doc-only]_ to the `master` branch.

All pages are created after the build completes successfully
and the artifacts for the pages job are uploaded to GitLab.

### Option B: GitLab CI for Jekyll websites
{: .no_toc}

Jekyll is so far the most popular [Static Site Generator (SSG)][SSGs] available, that's why we'll use it as a first example
for configuring our GitLab CI. On the next section you'll find more [examples](#examples) for SSGs already tested with GitLab Pages.

Jekyll is written in [Ruby] and generates static blog-aware websites.
Blog-aware means a website generator will create blog-style content, such as lists of
content in reverse chronological order, archive lists, and
other common blog-style features.

We can write dynamically with [Liquid], [Markdown] and [YAML] and
Jekyll builds the static site (HTML, CSS, JS) for us.
You will find the same functionality for every SSG,
yet each of them uses its own environment, template system, markup language, etc.

If you want GitLab Pages to [build your Jekyll website][pages-ci-jekyll],
you can start with the simple script below:

```yaml
image: ruby:2.1

pages:
  script:
  - gem install jekyll
  - jekyll build -d public/
  artifacts:
    paths:
    - public
  only:
  - master
```

This code requires the _[script][doc-script]_ to run on
the _[environment][doc-images]_ of [Ruby] 2.1.x,
installs the Jekyll gem, and builds the site
to the _[public path][doc-contents-ciconfig]_.
The result affects _[only][doc-only]_ the master branch.
For building a regular Jekyll site, you can just
copy this code and paste it into your `.gitlab-ci.yml`.

If you are familiar with Jekyll, you will probably want to use [Bundler] to build your Jekyll site.
We've prepared an [example][jekyll-proj] for that. Also, if you want to use a specific Jekyll version, you can
find an [example][jekyll-253-example] in the [Jekyll Themes][jekyll-examples]
group I set up for the purposes of this post.
And of course, since you are the one who controls how GitLab CI builds your site,
you are free to use any [Jekyll Plugins][Jekyll Plugin]. _Yep!_

### Option C: GitLab CI for Hexo websites
{: .no_toc}

Let's see another example. [Hexo] is a powerful blog-aware framework built with [NodeJS][node],
a server-side JavaScript environment based on [Google V8] high-performance engine.

To build our Hexo site, we can start with this `.gitlab-ci.yml`:

```yaml
image: node:4.2.2

pages:
  cache:
    paths:
    - node_modules/

  script:
  - npm install hexo-cli -g
  - npm install
  - hexo deploy
  artifacts:
    paths:
    - public
  only:
    - master
```

Note that the [Docker image][node-422] we require is `node:4.2.2`.
We are archiving `npm` modules into the `cache`, installing `hexo-cli` and deploying
our `hexo` site to the default `public` directory, uploaded to GitLab as `artifacts`.
The `pages` job is `only` affecting the `master` branch.

On the [Pages][ci-examples] group you will find a default [Hexo site][pages-hexo]
deployed with GitLab Pages, and on [this group][themes-templates], another [example][hexo-proj]
with a slightly different configuration.

### Step 3: Upload your website content
{: #upload-content}

Push the content to your remote project and keep an eye on the build!

**Don't forget:** when you are using GitLab Pages with a Static Site Generator,
do not upload the directory which your SSG generated locally,
otherwise you'll have duplicated contents and you might face build errors.
For example, do not commit the `_site` directory ([Jekyll]) or the `build` directory
([Middleman]) or the `public` directory ([Hexo]). You can do this automatically by adding
them to a `.gitignore` file, placed at your project's root directory.

E.g., if you are building a Jekyll site, your `.gitignore` will have this line:

```
_site
```

A `.gitignore` is very useful to avoid uploading to your remote repository any file or folder within your project.
If you want to know more about it, check the [`.gitignore` official docs][git-docs-gitignore].

### Step 4: Add your custom domain
{: #custom-domains}

**Note:** Custom CNAMEs with TLS support were introduced in [GitLab EE 8.5][EE-85].
{: .note}

If you want, you are free to [add your own domain(s) name][pages-custom-domain] to your website hosted by GitLab.com.
It's not required though, you can always use the standard GitLab Pages subdomain accessed under `https://mynamespace.gitlab.io`.

_Features_

- Besides including your own domain, you can add your custom **subdomain** to your GitLab Pages project (e.g., `subdomain.example.com`)
- You can enter more than one domain alias **per project** (e.g., `example.com`,
`example.net` `my.example.org` and `another-example.com` pointing to your project under `mynamespace.gitlab.io` or
`mynamespace.gitlab.io/myproject`). A domain alias is like having multiple front doors to one location.
- If you want to enable an HTTPS secure connection to your domains, you can affix your own SSL/TLS digital
certificate to **each** custom domain or subdomain you've added to your projects.

_Steps to set up a custom domain_

- From your project's dashboard, go to **Settings** (<i class="fa fa-cog" aria-hidden="true"></i>) **> Pages > New Domain**
- Add your domain to the first field: `mydomain.com`
- If you have an SSL/TLS digital certificate and its key, add them to their respective fields.
If you don't, just leave the fields blank.
- Click on **Create New Domain**.
- Finally, access your domain control panel and create a new [DNS `A` record][dns-A] pointing
to the [IP of GitLab Pages server][pages-settings]:

```
mydomain.com A 104.208.235.32
```

Alternatively, a similar procedure can be applied for **custom subdomains**:

- Add the subdomain to the first field: `subdomain.mydomain.com`

- Then create a new [DNS `CNAME` record][dns-cname] pointing to `myusername.gitlab.io`:

```
subdomain.mydomain.com CNAME myusername.gitlab.io
```

Repeat these steps for any additional domain aliases.

Note that how you set up your DNS records will depend upon which company you
used to register your domain name. Every company has its own methods for DNS Zone Management.
On this link you can find an [overview for some providers][dns-zone-examples],
it might help you to follow through. Please contact your provider directly if you need some extra help.

Ordinarily, DNS propagation needs some time to take effect, so don't worry if you can't access your
website under your custom domain instantaneously. Wait a few minutes and check it again.

## Examples

Check out the [Pages][ci-examples] official group for a list of example projects,
where you can explore some good options for Static Site Generators for Ruby, NodeJS and Python environments.
You can also find more specific examples on the following groups, which I prepared for the purposes of this post:

- [Jekyll Themes][jekyll-examples] (Ruby/Jekyll)
- [Middleman Themes][middle-examples] (Ruby/Middleman)
- [Themes and Templates][themes-templates] (Miscellaneous)
- [HTML Themes][html-examples] (plain HTML)

**Note:** these themes, templates and SSGs were casually chosen and listed on this
post to provide you with some distinct GitLab CI configurations.
{: .note}

## FAQ

### Is all of this really free to use?
{: .no_toc}

Yes, it is! On [GitLab.com][sign-up] you can create your free account
and enjoy all its [features][gitlab-com], including unlimited private repositories,
projects, websites, and contributors. Also, you'll have 10GB disk space per project, [1GB per Pages artifacts][pages-settings],
and unlimited total disk space. Awesome, isn't it? Why don't you take a peek at the [public projects][explore]?

### Where is the `public` folder?
{: .no_toc}

When a build succeeds, you'll find your static site at your project's **Pipelines > Builds > Build ID > Browse**.
You can download the artifacts from the same screen.

![Build Artifacts - Browse or Download](/images/blogimages/gitlab-pages/gitlab-browse-download-artifacts.png)

### Can I really use any Static Site Generator?
{: .no_toc}

Yes, you can use any [Static Site Generator][SSGs] available.

### Can I use free SSL/TLS digital certificates?
{: .no_toc}

Yes, absolutely! Need a suggestion? Try [StartSSL] or [Let's Encrypt][lets-encrypt].

### Can I contribute to the themes?
{: .no_toc}

Sure! You are very welcome to contribute to the groups mentioned above.
To do that, please set your website up and make sure it's working as you expected.
Then, add an issue to the [group](#examples) you're interested in. Don't forget to include a link to your project.
After a brief evaluation, we'll be glad to fork your project and present your theme to our community!

### Can I use `.php` pages and connect databases with my sites?
{: .no_toc}

No. GitLab Pages hosts static websites only (HTML, CSS and JS).

## Getting Help

If you need some help regarding GitLab Pages on GitLab.com, 
feel free to use one of [our channels][get-help]. You can also open an issue on the [Pages][pages-issues] group.

<a name="conclusions"></a>

## Conclusion
{: #conclusions}

Hopefully now you understand how **[GitLab Pages][pages]** works and how to create your new site.

Follow [@GitLab][twitter] on Twitter and stay tuned for updates!

We're looking forward to seeing your sites!

**Note:** this post has been updated (June 17th, 2016) to match the new GitLab UI.
{: .note}

## About guest author Marcia Ramos
{: .no_toc}

[Marcia] is a back-end developer specialized in WordPress and Jekyll sites at [Virtua Creative],
though she does some front-end too. Her daily work is based on version-controlled systems for almost 15 years.
She is driven by her thirst for knowledge and her eagerness to continuously expand her horizons.
When she is not coding, she is writing articles, studying, teaching or contributing to open source projects here and there.

[doc-artifacts]: http://doc.gitlab.com/ee/ci/yaml/README.html#artifacts
[doc-ciconfig]: http://doc.gitlab.com/ee/ci/quick_start/README.html#creating-a-.gitlab-ci.yml-file
[doc-config-runners]: http://doc.gitlab.com/ee/ci/quick_start/README.html#configuring-a-runner
[doc-contents-ciconfig]: http://doc.gitlab.com/ee/pages/README.html#explore-the-contents-of-.gitlab-ci.yml
[doc-groups]: http://doc.gitlab.com/ee/workflow/groups.html
[doc-images]: http://doc.gitlab.com/ee/ci/yaml/README.html#image-and-services
[doc-jobs]: http://doc.gitlab.com/ce/ci/yaml/README.html#jobs
[doc-only]: http://doc.gitlab.com/ee/ci/yaml/README.html#only-and-except
[doc-runners]: http://doc.gitlab.com/ee/ci/runners/README.html#sts=Runners
[doc-script]: http://doc.gitlab.com/ee/ci/yaml/README.html#script
[doc-shared-runners]: http://doc.gitlab.com/ee/ci/quick_start/README.html#shared-runners
[doc-stages]: http://doc.gitlab.com/ce/ci/yaml/README.html#stages
[ee-yaml-ci]: http://doc.gitlab.com/ee/ci/yaml/README.html
[pages]: https://pages.gitlab.io
[pages-ee]: http://doc.gitlab.com/ee/pages/README.html
[pages-introduced]: https://about.gitlab.com/2016/04/04/gitlab-pages-get-started/
[pages-issues]: https://gitlab.com/pages/pages.gitlab.io/issues
[pages-work]: http://doc.gitlab.com/ee/pages/README.html#getting-started-with-gitlab-pages
[pages-user]: http://doc.gitlab.com/ee/pages/README.html#user-or-group-pages
[pages-project]: http://doc.gitlab.com/ee/pages/README.html#project-pages
[pages-ci-html]: http://doc.gitlab.com/ee/pages/README.html#how-.gitlab-ci.yml-looks-like-when-the-static-content-is-in-your-repository
[pages-ci-jekyll]: http://doc.gitlab.com/ee/pages/README.html#how-.gitlab-ci.yml-looks-like-when-using-a-static-generator
[pages-custom-domain]: http://doc.gitlab.com/ee/pages/README.html#add-a-custom-domain-to-your-pages-website
[pages-settings]: https://about.gitlab.com/gitlab-com/settings/#gitlab-pages
[quick start guide]: http://doc.gitlab.com/ee/ci/quick_start/README.html

[about-gitlab-com]: https://about.gitlab.com/
[ci-lint]: https://gitlab.com/ci/lint "Try me!"
[cname-issue]: https://gitlab.com/gitlab-org/gitlab-ee/issues/134
[ee-85]: https://gitlab.com/gitlab-org/gitlab-ee/merge_requests/173
[explore]: https://gitlab.com/explore
[get-help]: https://about.gitlab.com/getting-help
[gitlab83]: https://about.gitlab.com/2015/12/22/gitlab-8-3-released
[gitlab-com]: https://about.gitlab.com/gitlab-com/
[gitlab-ee]: https://about.gitlab.com/features/#enterprise
[sign-up]: https://gitlab.com/users/sign_in "Sign Up, it's free!"
[twitter]: https://twitter.com/gitlab

[Brunch]: http://brunch.io/
[Bundler]: http://bundler.io/
[Coffee Script]: http://coffeescript.org/
[dns-A]: https://support.dnsimple.com/articles/a-record/
[dns-cname]: https://en.wikipedia.org/wiki/CNAME_record
[dns-zone-examples]: http://docs.businesscatalyst.com/user-manual/site-settings/site-domains/updating-dns-records-with-a-domain-registrar-external-dns
[git]: https://git-scm.com/about
[git-docs-gitignore]: https://git-scm.com/docs/gitignore
[go]: https://golang.org/
[Google V8]: https://developers.google.com/v8/
[Harp]: http://harpjs.com/
[Hexo]: https://hexo.io/
[Hyde]: http://hyde.github.io/
[Hugo]: https://gohugo.io/
[Jekyll]: https://jekyllrb.com
[Jekyll Documentation]: http://jekyllrb.com/docs/home/
[Jekyll Plugin]: https://jekyllrb.com/docs/plugins/
[Lektor]: https://www.getlektor.com/
[lets-encrypt]: https://letsencrypt.org/
[Liquid]: https://github.com/Shopify/liquid/wiki
[Markdown]: http://daringfireball.net/projects/markdown/
[Metalsmith]: http://www.metalsmith.io/
[Middleman]: https://middlemanapp.com/
[Nanoc]: http://nanoc.ws/
[node]: https://nodejs.org/en/
[node-422]: https://hub.docker.com/_/node/
[Pelican]: http://blog.getpelican.com/
[Python]: https://www.python.org/
[Ruby]: https://www.ruby-lang.org/
[Sass]: http://sass-lang.com/
[SSGs]: https://www.staticgen.com/
[StartSSL]: https://startssl.com/
[wiki-static-websites]: https://en.wikipedia.org/wiki/Static_web_page
[YAML]: http://yaml.org/
[Marcia]: https://gitlab.com/u/virtuacreative
[Virtua Creative]: https://virtuacreative.com.br/en/

[ci-examples]: https://gitlab.com/groups/pages
[html-examples]: https://gitlab.com/groups/html-themes
[jekyll-examples]: https://gitlab.com/groups/jekyll-themes
[middle-examples]: https://gitlab.com/groups/middleman-themes
[themes-templates]: https://gitlab.com/themes-templates

[jekyll-proj]: https://gitlab.com/jekyll-themes/default-bundler
[jekyll-253-example]: https://gitlab.com/jekyll-themes/carte-noire
[hexo-proj]: https://gitlab.com/themes-templates/hexo
[pages-hexo]: https://gitlab.com/pages/hexo
