---
title: "Building a new GitLab Docs site with Nanoc, GitLab CI, and GitLab Pages"
author: Connor Shea
author_twitter: connorjshea
categories: tutorial
image_title: '/images/blogimages/book.jpg'
description: "How we built the new GitLab Docs portal from the ground up"
---

We recently rebuilt [docs.gitlab.com](https://docs.gitlab.com) from scratch. Where previously the site was generated with a simple Ruby script, we now use a proper static site generator.

Check out the improvements we made, the structure we now use to deploy from specific directories in multiple repositories to a single website, build with [GitLab CI](/gitlab-ci/) and deployed with [GitLab Pages][pages]. Now our documentation has a nicer look and feel, is more pleasant to read through, and simpler and quicker to maintain.

<!-- more -->

- TOC
{:toc}

## Improvements

The old documentation website was pretty much just an HTML file, a stylesheet, and a [Ruby script][genrb] called `generate.rb`. While it worked, it was hard to update and not very flexible. It mostly laid dormant, only occasionally being touched by developers. The docs team really wanted to update the site to use a [static site generator](/2016/06/17/ssg-overview-gitlab-pages-part-3-examples-ci/) and take better advantage of [GitLab Pages][pages].

We chose [Nanoc](http://nanoc.ws/) because it’s fast, it comes with a number of built-in helpers and filters (as well as the ability to create custom ones), and it’s built with Ruby. Overall, we think this was definitely the right choice. The author was very responsive and addressed anything we brought up. Kudos to him on the great project!

Other improvements include syntax highlighting with [Rouge](http://rouge.jneen.net/) (no syntax highlighting was used at all on the old site), breadcrumbs for navigating between pages, and an improved overall design – especially on mobile.

## Requirements

Our documentation site has some unique requirements that I haven’t seen mentioned or solved in any other companies’ blog posts. We have a few products with documentation we want to include in the site: Community Edition, Enterprise Edition, Omnibus GitLab, and GitLab Runner. In the future we’ll likely add more.

Each product has it own repository with its own documentation directory. This allows developers to add documentation in the same merge request they add a new feature or change some behavior, which prevents documentation from becoming outdated.

The site also needed to be flexible enough that we could add versioning to it in the future. Eventually, our goal is to replace the Help section in CE/EE with this Docs site, so we need to maintain older versions of the documentation on the Docs site for users on older versions of GitLab.

## The build process

Given the requirements and separate repositories, we decided we’d just need to clone the repositories as part of the build process.

Inside Nanoc's config file (`nanoc.yml`), we [have defined][nanocyaml] a hash of each of our products containing all the data we need. Here's an excerpt:

```yaml
products:
  ce:
    full_name: 'GitLab Community Edition'
    short_name: 'Community Edition'
    abbreviation: 'CE'
    slug: 'ce'
    index_file: 'README.*'
    description: 'Browse user and administration documentation and guides for GitLab Community Edition.'
    repo: 'https://gitlab.com/gitlab-org/gitlab-ce.git'
    dirs:
      temp_dir: 'tmp/ce/'
      dest_dir: 'content/ce'
      doc_dir:  'doc'

...

  runner:
    full_name: 'GitLab Runner'
    short_name: 'Runner'
    abbreviation: 'RU'
    slug: 'runner'
    index_file: 'index.*'
    description: 'Browse installation, configuration, maintenance, and troubleshooting documentation for GitLab Runner.'
    repo: 'https://gitlab.com/gitlab-org/gitlab-ci-multi-runner.git'
    dirs:
      temp_dir: 'tmp/runner/'
      dest_dir: 'content/runner'
      doc_dir:  'docs'
```

We then have the [Rakefile] where the repos are cloned and the directories that
Nanoc needs are created:

```ruby
desc 'Pulls down the CE, EE, Omnibus and Runner git repos and merges the content of their doc directories into the nanoc site'
task :pull_repos do
  require 'yaml'

  # By default won't delete any directories, requires all relevant directories
  # be empty. Run `RAKE_FORCE_DELETE=true rake pull_repos` to have directories
  # deleted.
  force_delete = ENV['RAKE_FORCE_DELETE']

  # Parse the config file and create a hash.
  config = YAML.load_file('./nanoc.yaml')

  # Pull products data from the config.
  ce = config["products"]["ce"]
  ee = config["products"]["ee"]
  omnibus = config["products"]["omnibus"]
  runner = config["products"]["runner"]

  products = [ce, ee, omnibus, runner]
  dirs = []
  products.each do |product|
    dirs.push(product['dirs']['temp_dir'])
    dirs.push(product['dirs']['dest_dir'])
  end

  if force_delete
    puts "WARNING: Are you sure you want to remove #{dirs.join(', ')}? [y/n]"
    exit unless STDIN.gets.index(/y/i) == 0

    dirs.each do |dir|
      puts "\n=> Deleting #{dir} if it exists\n"
      FileUtils.rm_r("#{dir}") if File.exist?("#{dir}")
    end
  else
    puts "NOTE: The following directories must be empty otherwise this task " +
      "will fail:\n#{dirs.join(', ')}"
    puts "If you want to force-delete the `tmp/` and `content/` folders so \n" +
      "the task will run without manual intervention, run \n" +
      "`RAKE_FORCE_DELETE=true rake pull_repos`."
  end

  dirs.each do |dir|
    unless "#{dir}".start_with?("tmp")

      puts "\n=> Making an empty #{dir}"
      FileUtils.mkdir("#{dir}") unless File.exist?("#{dir}")
    end
  end

  products.each do |product|
    temp_dir = File.join(product['dirs']['temp_dir'])
    puts "\n=> Cloning #{product['repo']} into #{temp_dir}\n"

    `git clone #{product['repo']} #{temp_dir} --depth 1 --branch master`

    temp_doc_dir = File.join(product['dirs']['temp_dir'], product['dirs']['doc_dir'], '.')
    destination_dir = File.join(product['dirs']['dest_dir'])
    puts "\n=> Copying #{temp_doc_dir} into #{destination_dir}\n"
    FileUtils.cp_r(temp_doc_dir, destination_dir)
  end
end
```

The `pull_repos` task inside the Rakefile is pretty self-explanatory if you know
some Ruby, but here's what it does:

1. `nanoc.yml` is loaded since it contains the information we need for the
   various products:

    ```ruby
    config = YAML.load_file('./nanoc.yaml')
    ```

1. The products data are pulled from the config:

    ```ruby
    ce = config["products"]["ce"]
    ee = config["products"]["ee"]
    omnibus = config["products"]["omnibus"]
    runner = config["products"]["runner"]
    ```

1. The needed directories to be created (or deleted) are populated in an array:

    ```ruby
    products = [ce, ee, omnibus, runner]
    dirs = []
    products.each do |product|
      dirs.push(product['dirs']['temp_dir'])
      dirs.push(product['dirs']['dest_dir'])
    end
    ```

1. The empty directories are created:

    ```ruby
    dirs.each do |dir|
      unless "#{dir}".start_with?("tmp")

        puts "\n=> Making an empty #{dir}"
        FileUtils.mkdir("#{dir}") unless File.exist?("#{dir}")
      end
    end
    ```
1. We finally copy the contents of the documentation directory (defined by
   `doc_dir`) for each product from `tmp/` to `content/`:

    ```ruby
    products.each do |product|
      temp_dir = File.join(product['dirs']['temp_dir'])
      puts "\n=> Cloning #{product['repo']} into #{temp_dir}\n"

      `git clone #{product['repo']} #{temp_dir} --depth 1 --branch master`

      temp_doc_dir = File.join(product['dirs']['temp_dir'], product['dirs']['doc_dir'], '.')
      destination_dir = File.join(product['dirs']['dest_dir'])
      puts "\n=> Copying #{temp_doc_dir} into #{destination_dir}\n"
      FileUtils.cp_r(temp_doc_dir, destination_dir)
    end
    ```

   `content/` is where Nanoc looks for the actual site’s Markdown files. To prevent the `tmp/` and `content/` subdirectories from being pushed after testing the site locally, they’re excluded by `.gitignore`.

In the future we may speed this up further by caching the `tmp` folder in CI. The task would need to be updated to check if the local repository is up-to-date with the remote, only cloning if they differ.

Now that all the needed files are in order, we run `nanoc` to build the static sire. Nanoc runs each Markdown file through a series of [filters][nanoc-filters] defined by rules in the [`Rules` file][rules]. We currently use [Redcarpet][] as the Markdown parser along with Rouge for syntax highlighting, as well as some custom filters. We plan on [moving to Kramdown as our Markdown parser in the future](https://gitlab.com/gitlab-com/gitlab-docs/issues/50) as it provides some nice stuff like user-defined Table of Contents, etc.

We also define some filters inside the [`lib/filters/` directory][filtersdir],
including one that [replaces any `.md` extension with `.html`][md2html].

The Table of Contents (ToC) is generated for each page except when it's named `index.md`
or `README.md` as we usually use these as landing pages to index other
documentation files and we don't want them to have a ToC. All this and some
other options that Redcarpet provides [are defined in the `Rules` file][redrules].

For more on the specifics of building a site with Nanoc, see [the Nanoc tutorial](http://nanoc.ws/doc/tutorial/).

## Taking advantage of GitLab to put everything together

The new docs portal is hosted on GitLab.com at <https://gitlab.com/gitlab-com/gitlab-docs>.
In that project we create issues, discuss things, open merge requests in feature
branches, iterate on feedback and finally merge things in the `master` branch.
Again, the documentation source files are not stored in this repository, if
you want to contribute, you'd have to open a merge request to the respective
project.

There are 3 key things we use to test, build, deploy and host the Nanoc site
all built into GitLab: [GitLab CI](/gitlab-ci), [Review Apps](/features/review-apps)
and [GitLab Pages][pages].

Let's break it down to pieces.

### GitLab CI

GitLab CI is responsible of all the stages that we go through to publish
new documentation: test, build and deploy.

Nanoc has a built-in system of [Checks](http://nanoc.ws/doc/testing/), including HTML/CSS and internal/external link validation. With GitLab CI we test with the internal link checker (set to [`allow failure`][allowfail]) and also verify that the site compiles without errors. We also run a [SCSS Linter](https://github.com/brigade/scss-lint) to make sure our SCSS looks uniform.

Our full [`.gitlab-ci.yml`](https://gitlab.com/gitlab-com/gitlab-docs/blob/master/.gitlab-ci.yml) file looks like this. We'll break it down to make it clear what it is doing:

```yaml
image: ruby:2.3

## Cache the vendor/ruby directory
cache:
  key: "ruby-231"
  paths:
  - vendor/ruby

## Define the stages
stages:
  - test
  - deploy

## Before each job's script is run, run the commands below
before_script:
  - ruby -v
  - bundle install --jobs 4 --path vendor

## Make sure the site builds successfully
verify_compile:
  stage: test
  script:
    - rake pull_repos
    - nanoc
  artifacts:
    paths:
      - public
    expire_in: 1w
  except:
    - master
  tags:
    - docker

## Check for dead internal links using Nanoc's built-in tool
internal_links:
  stage: test
  script:
    - rake pull_repos
    - nanoc
    - nanoc check internal_links
  allow_failure: true
  tags:
    - docker

## Make sure our SCSS stylesheets are correctly defined
scss_lint:
  stage: test
  script:
    - bundle exec scss-lint
  tags:
    - docker

## A job that deploys a review app to a dedicated server running Nginx.
review:
  stage: deploy
  variables:
    GIT_STRATEGY: none
  before_script: []
  cache: {}
  script:
    - rsync -av --delete public /srv/nginx/pages/$CI_BUILD_REF_NAME
  environment:
    name: review/$CI_BUILD_REF_NAME
    url: http://$CI_BUILD_REF_NAME.$APPS_DOMAIN
    on_stop: review_stop
  only:
    - branches@gitlab-com/gitlab-docs
  except:
    - master
  tags:
    - nginx
    - review-apps

## Stop the review app
review_stop:
  stage: deploy
  variables:
    GIT_STRATEGY: none
  before_script: []
  artifacts: {}
  cache: {}
  dependencies: []
  script:
    - rm -rf public /srv/nginx/pages/$CI_BUILD_REF_NAME
  when: manual
  environment:
    name: review/$CI_BUILD_REF_NAME
    action: stop
  only:
    - branches@gitlab-com/gitlab-docs
  except:
    - master
  tags:
    - nginx
    - review-apps

## Deploy the static site to GitLab Pages
pages:
  stage: deploy
  environment:
    name: production
    url: https://docs.gitlab.com
  script:
    - rake pull_repos
    - nanoc
    # Symlink all README.html to index.html
    - for i in `find public -name README.html`; do ln -sf README.html $(dirname $i)/index.html; done
  artifacts:
    paths:
    - public
    expire_in: 1h
  only:
    - master@gitlab-com/gitlab-docs
  tags:
    - docker
```

To better visualize how the jobs are run, take a look at how the pipeline
graph looks like for [one of the pipelines][pipeline].

![Pipeline graph example](/images/blogimages/new-gitlab-docs-site/pipeline-graph.png){: .shadow}

Let's see what all these settings mean.

For more information, you can read the [documentation on `.gitlab-ci.yml`][ciyaml].
{: .alert .alert-info}

---

Define the Docker image to be used:

```yaml
image: ruby:2.3
```

[Cache] the vendor/ruby directory so that we don't have to install the
gems for each job/pipeline:

```yaml
cache:
  key: "ruby-231"
  paths:
  - vendor/ruby
```

Define the [stages] the jobs will run:

```yaml
stages:
  - test
  - deploy
```

Before each job's script is run, run the commands that are defined in the
[`before_script`][before_script]. Display the Ruby version and install
the needed gems:

```yaml
before_script:
  - ruby -v
  - bundle install --jobs 4 --path vendor
```

In the `verify_compile` job we make sure the site builds successfully.
It first pulls the repos locally, then runs `nanoc` to compile the site.
The `public/` directory where the static site is built, is uploaded as
an artifact so that it can pass between stages. We define an expire date of
one week. The job runs on all refs except master. The `docker` tag ensures that
this job is picked by the shared Runners on GitLab.com:

```yaml
verify_compile:
  stage: test
  script:
    - rake pull_repos
    - nanoc
  artifacts:
    paths:
      - public
    expire_in: 1w
  except:
    - master
  tags:
    - docker
```

In the `internal_links` job we check for dead internal links using Nanoc's
built-in functionality. We first need to pull the repos and compile the static
site. We allow it to fail since the source of the dead links are in a
different repository, not much related with the current one.
The `docker` tag ensures that this job is picked by the shared Runners
on GitLab.com:

```yaml
internal_links:
  stage: test
  script:
    - rake pull_repos
    - nanoc
    - nanoc check internal_links
  allow_failure: true
  tags:
    - docker
```

The `scss_lint` job makes sure our SCSS stylesheets are correctly defined by
running a linter on them. The `docker` tag ensures that this job is picked by
the shared Runners on GitLab.com:

```yaml
scss_lint:
  stage: test
  script:
    - bundle exec scss-lint
  tags:
    - docker

```

Next, we define the Review Apps.

### Review Apps

When opening a merge request for the docs site we use a new feature called [Review Apps](/features/review-apps/) to test changes. This lets us test new features, style changes, new sections, etc., by deploying the updated static site to a test domain. On every merge request that all jobs finished successfully, we can see a link with the URL to the temporary deployed docs site.

![Review apps](/images/blogimages/gitlab-docs-review-apps-screenshot.png){: .shadow}

We define two additional jobs for that purpose in `.gitlab-ci.yml`:

```yaml
review:
  stage: deploy
  variables:
    GIT_STRATEGY: none
  before_script: []
  cache: {}
  script:
    - rsync -av --delete public /srv/nginx/pages/$CI_BUILD_REF_NAME
  environment:
    name: review/$CI_BUILD_REF_NAME
    url: http://$CI_BUILD_REF_NAME.$APPS_DOMAIN
    on_stop: review_stop
  only:
    - branches@gitlab-com/gitlab-docs
  except:
    - master
  tags:
    - nginx
    - review-apps

review_stop:
  stage: deploy
  variables:
    GIT_STRATEGY: none
  before_script: []
  artifacts: {}
  cache: {}
  dependencies: []
  script:
    - rm -rf public /srv/nginx/pages/$CI_BUILD_REF_NAME
  when: manual
  environment:
    name: review/$CI_BUILD_REF_NAME
    action: stop
  only:
    - branches@gitlab-com/gitlab-docs
  except:
    - master
  tags:
    - nginx
    - review-apps
```

They both run on all branches except `master` since `master` is deployed straight
to production. Once someone with write access to the repository pushes a branch
and creates a merge request, if the jobs in the `test` stage finish successfully,
the `review` job deploys the code of that particular branch to a server. The
server is set up to [use Nginx with Review Apps][nginx-example], and it uses
the artifacts from the previously `verify_compile` job which contain the
`public/` directory with the HTML files Nanoc compiled.

Notice that both jobs rely on [dynamic environments][environments] and with
the `review/` prefix we can group them under the [Environments page](https://gitlab.com/gitlab-com/gitlab-docs/environments).

The `review_stop` job depends on the `review` one and is called whenever we
want to clear up the review app. By default it is called every time the related
branch is deleted, but you can also manually call it with the buttons that can
be found in GitLab.

The trick of this particular set up is that we use the shared Runners provided
in GitLab.com to test and build the docs site (using Docker containers) whereas
we use a specific Runner that is set up in the server that hosts the Review Apps
and is configured with the [shell executor]. GitLab CI knows what Runner to use
each time from the `tags` we provide each job with.

The `review` job has also some other things specified:

```yaml
variables:
  GIT_STRATEGY: none
before_script: []
cache: {}
```

In this case, [`GIT_STRATEGY`][gitstrategy] is set up to `none` since we don't need to
checkout the repository for this job. We only use `rsync` to copy over the
artifacts that were passed from the previous job to the server where Review
Apps are deployed. We also turn off the `before_script` since we don't need it
to run, same for `cache`. They both are defined globally, so you need to pass
an empty array and hash respectively to disable them in a job level.

On the other hand, setting the `GIT_STRATEGY` to `none` is necessary on the
`review_stop` job so that the GitLab Runner won't try to checkout the code after
the branch is deleted. We also define one additional thing in it:

```yaml
dependencies: []
```

Since this is the last job that is performed in the lifecycle of a merge request
(after it's merged and the branch deleted), we opt to not download any artifacts
from the previous stage with passing an empty array in [`dependencies`][deps].

---

See [our blog post on Review Apps](/2016/11/22/introducing-review-apps/) for
more information about how they work and their purpose. Be sure to also check
the [Review Apps documentation][radocs] as well as [how dynamic environments work][environments]
since they are the basis of the Review Apps.

The final step after the site gets successfully built is to deploy to
production which is under the URL everybody knows: <https://docs.gitlab.com>.
For that purpose, we use [GitLab Pages][pages].

### GitLab Pages

[GitLab Pages](https://pages.gitlab.io/) hosts [static websites](https://en.wikipedia.org/wiki/Static_web_page) and can be used with any Static Site Generator, including [Jekyll](https://jekyllrb.com/), [Hugo](https://gohugo.io/), [Middleman](https://middlemanapp.com/), [Pelican](http://blog.getpelican.com/), and of course Nanoc.

GitLab Pages allows us to create the static site dynamically since it just deploys the `public` directory after the GitLab CI task is done. The job responsible for this is named `pages`.

A production environment is set with a url to the of the docs portal.
The script pulls the repos, runs `nanoc` to compile the static site.
The `public/` directory where the static site is built, is uploaded as
an artifact so that it can be deployed to GitLab Pages. We define an expire
date of one hour and the job runs only on the master branch.
The `docker` tag ensures that this job is picked by the shared Runners
on GitLab.com.

```yaml
pages:
  stage: deploy
  environment:
    name: production
    url: https://docs.gitlab.com
  script:
    - rake pull_repos
    - nanoc
    # Symlink all README.html to index.html
    - for i in `find public -name README.html`; do ln -sf README.html $(dirname $i)/index.html; done
  artifacts:
    paths:
    - public
    expire_in: 1h
  only:
    - master@gitlab-com/gitlab-docs
  tags:
    - docker
```

GitLab Pages deploys our documentation site whenever a commit is made to the master branch of the gitlab-docs repository and is run only on the `master` branch of the gitlab-docs project.

Since the documentation content itself is not hosted under the gitlab-docs repository, we rely to a CI job under all the products we build the docs site from. We specifically [make use of triggers][triggers] where a build for the docs site is triggered whenever CI runs successfully on the master branches of CE, EE, Omnibus GitLab, or Runner. If you go to the [pipelines page of the gitlab-docs project][pipelines-docs], you can notice the **triggered** word next to the pipelines that are re-run because a trigger was initiated.

![Pipeline triggers](/images/blogimages/new-gitlab-docs-site/pipelines-triggers.png){: .shadow}

How we specifically use triggers for gitlab-docs is briefly described in the
[project's readme][readme-triggers].

We also use a hack to symlink all `README.html` files into `index.html` so that
they can be viewed without the extension. Notice how the following links point
to the same document:

- <https://docs.gitlab.com/ce/ci/yaml/README.html>
- <https://docs.gitlab.com/ce/ci/yaml/index.html>
- <https://docs.gitlab.com/ce/ci/yaml/>

The line responsible for this is:

```bash
for i in `find public -name README.html`; do ln -sf README.html $(dirname $i)/index.html; done
```

The artifacts are made to [expire in] an hour since they are deployed to the
GitLab Pages server, we don't need them lingering in GitLab forever.

It’s worth noting that GitLab Pages is a [GitLab Enterprise Edition](/products)-only feature, but it’s also available for free on GitLab.com.
{: .alert .alert-info}

## Conclusion

Hopefully this shows some GitLab's power and how having everything integrated into one cohesive product simplifies one's workflow. If you have a complex documentation site you’d like to put together from specific directories in multiple Git repositories, the process described above is the best we've been able to come up with. If you have any ideas to make this system better, let us know!

The documentation website is [open source](https://gitlab.com/gitlab-com/gitlab-docs), available under the MIT License. You’re welcome to take a look at it, submit a merge request, or even fork it to use it with your own project.

Thanks for reading, if you have any questions we’d be happy to answer them in the comments!

<!-- Cover image: https://unsplash.com/photos/G6G93jtU1vE -->

[genrb]: https://gitlab.com/gitlab-com/doc-gitlab-com/blob/master/generate.rb
[nanocyaml]: https://gitlab.com/gitlab-com/gitlab-docs/blob/30f13e6a81bf9baeda95204b5524c6abf980b1e5/nanoc.yaml#L101-149
[Rakefile]: https://gitlab.com/gitlab-com/gitlab-docs/blob/30f13e6a81bf9baeda95204b5524c6abf980b1e5/Rakefile
[md2html]: https://gitlab.com/gitlab-com/gitlab-docs/blob/30f13e6a81bf9baeda95204b5524c6abf980b1e5/lib/filters/markdown_to_html_ext.rb
[redrules]: https://gitlab.com/gitlab-com/gitlab-docs/blob/30f13e6a81bf9baeda95204b5524c6abf980b1e5/Rules#L33-51
[redcarpet]: https://github.com/vmg/redcarpet
[allowfail]: https://docs.gitlab.com/ce/ci/yaml/#allow_failure
[ciyaml]: https://docs.gitlab.com/ce/ci/yaml/
[environments]: https://docs.gitlab.com/ce/ci/environments.html#dynamic-environments
[pipeline]: https://gitlab.com/gitlab-com/gitlab-docs/pipelines/5266794
[nginx-example]: https://gitlab.com/gitlab-examples/review-apps-nginx
[radocs]: https://docs.gitlab.com/ce/ci/review_apps/index.html
[shell executor]: https://docs.gitlab.com/runner/executors/shell.html
[triggers]: https://docs.gitlab.com/ce/ci/triggers/
[pipelines-docs]: https://gitlab.com/gitlab-com/gitlab-docs/pipelines
[readme-triggers]: https://gitlab.com/gitlab-com/gitlab-docs/blob/master/README.md#deployment-process
[gitstrategy]: https://docs.gitlab.com/ce/ci/yaml/#git-strategy
[expire in]: https://docs.gitlab.com/ce/ci/yaml/#artifacts-expire_in
[deps]: https://docs.gitlab.com/ce/ci/yaml/#dependencies
[pages]: https://pages.gitlab.io
[nanoc-filters]: http://nanoc.ws/doc/reference/filters/
[rules]: https://gitlab.com/gitlab-com/gitlab-docs/blob/30f13e6a81bf9baeda95204b5524c6abf980b1e5/Rules
[filtersdir]: https://gitlab.com/gitlab-com/gitlab-docs/tree/30f13e6a81bf9baeda95204b5524c6abf980b1e5/lib/filters
[cache]: https://docs.gitlab.com/ce/ci/yaml/#cache
[stages]: https://docs.gitlab.com/ce/ci/yaml/#stages
[before_script]: https://docs.gitlab.com/ce/ci/yaml/#before_script
