---
title: "How to set up GitLab Runner on DigitalOcean"
date: 2016-04-19 10:00
author: Achilleas Pipinellis
author_twitter: _axil
categories: runner,digitalocean
image_title: /images/unsplash/runners.jpg
---

### Introduction

GitLab has [built-in continuous integration][doc-ci] to allow you to run a
number of tasks as you prepare to deploy your software. Typical tasks
might be to build a software package or to run tests as specified in a
YAML file. These tasks need to run by something, and in GitLab this something
is called a [Runner][doc-runners]; an application that processes builds.

In March we introduced [GitLab Runner 1.1][1_1] with the cool feature of
autoscaling and a week later we announced that all [shared Runners on GitLab.com
use autoscaling][autoscale-post]. The shared Runners can be used for free by
any user with a GitLab.com account.

In this tutorial we will explore how easy it is to install and set up your own
Runner on [DigitalOcean]; a Runner that will be 'specific' to your projects as
we say in the GitLab lingo.

## Prerequisites

We will use the Docker executor since it has the most supported features
according to the [GitLab Runner executor compatibility chart][chart]. For this,
we will need to install Docker on the server that will host the GitLab Runner.

Fortunately, DigitalOcean has a [one-click image with Docker][one-docker]
pre-installed on Ubuntu 14.04 and this is what we will use.

>**Note:**
You are free to use any Linux distribution supported by DigitalOcean, even
FreeBSD. GitLab Runner is supported on all Operating Systems.

## Create a droplet

[Login to DigitalOcean][cloud] and from the Control Panel, click on the "Create
Droplet" button that is visible from any page.

![Create Droplet](/images/blogimages/how-to-set-up-gitlab-runner-on-digitalocean/create-droplet-shadow.png)

Under the "Choose an image" section, select the "One-click Apps" tab and click
the "Docker" image (the version might differ).

![Droplet app](/images/blogimages/how-to-set-up-gitlab-runner-on-digitalocean/select-docker-shadow.png)

The next step is to choose the droplet size and the region you would like to use.
You are advised to use the **1 GB** / **1 CPU** droplet for quicker builds.

![Hardware](/images/blogimages/how-to-set-up-gitlab-runner-on-digitalocean/hardware-shadow.png)

Add any SSH Keys, select any settings you'd like to use, and click "Create" at
the bottom.

![Finalize creation](/images/blogimages/how-to-set-up-gitlab-runner-on-digitalocean/finalize-shadow.png)

Your Docker droplet will be created and available in a few minutes!

## Install the GitLab Runner

First, login to the new droplet via SSH and verify that Docker is installed with:

```bash
docker info
```

This should show a bunch of information about the Docker version, the number of
images and containers, etc. With that set, we're ready to install GitLab
Runner.

GitLab provides a repository where you can easily install and update GitLab
Runner. The supported distros as Debian, Ubuntu and CentOS. Let's install the
repository with this one-line:

```bash
curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-ci-multi-runner/script.deb.sh | bash
```

Feel free to read the script before you execute it if you want.

Now let's install GitLab Runner:

```bash
apt-get install gitlab-ci-multi-runner
```

And verify it's installed:

```bash
gitlab-runner --version
```

Excellent! We're now ready to start using it.

> **Note:**
For other installation methods and Operating Systems, see the
[installation documentation][doc-install].

## Register the GitLab Runner

Registering a Runner is the process of tying it with a specific GitLab project.
Each project on GitLab has a unique token that is used by the Runner in order
to be able to talk to GitLab via its API.

When we installed GitLab Runner in the previous step, we installed GitLab Runner
the service. Each GitLab Runner service can spawn as many Runner processes you
want, so you can eventually register multiple Runners in a single droplet, each
of which can be tied to a separate project.

To register a Runner we first need to know the project's token. Go to your
newly created project or pick one that already uses GitLab.com's shared Runners.
Navigate to the project's **Settings > Runners** and notice that the shared
Runners are enabled. In the left side you get detailed information on the steps
needed to register a new Runner.

![Runners settings](/images/blogimages/how-to-set-up-gitlab-runner-on-digitalocean/runners-shadow.png)

Now, let's get back to the droplet and start registering a Runner:

```
gitlab-runner register
```

The command above is interactive, so you will be asked the information needed to
register a new Runner.

- **the gitlab-ci coordinator URL:** Enter `https://gitlab.com/ci`.
- **the gitlab-ci token for this runner:** The token in the previous image.
- **the gitlab-ci description for this runner:** This is for your own accord,
  in case you have multiple Runners and want something to remind you what the
  Runner is about. If you don't enter a description, the hostname of the
  droplet will be used.
- **the gitlab-ci tags for this runner:** You can use tags in your
  `.gitlab-ci.yml` to limit jobs to specific Runners. Useful if for example
  you are running tests on different OSes. Enter `docker,digitalocean` for this
  example.
- **enter the executor:** Our executor will be `docker`.
- **enter the default Docker image:** The default Docker image that will be
  used if you don't specify it in `.gitlab-ci.yml`.

Once answered all questions, you can verify that the Runner is registered with:

```
gitlab-runner list
```

Now if you head back in your project's **Settings > Runners** you will see that
the Runner appeared in the list.

![Runner](/images/blogimages/how-to-set-up-gitlab-runner-on-digitalocean/runner-shadow.png)

You can now start using this specific Runner for your project and you may
disable the shared Runners.

---

When you register a Runner via the `gitlab-runner register` command, the answers
you give get written in the Runner's configuration file, which is located at
`/etc/gitlab-runner/config.toml`. If we open this file after we registered the
above Runner, here's what we see:

```
concurrent = 1

[[runners]]
  name = "docker-1gb-ams2-01"
  url = "https://gitlab.com/ci"
  token = "467f75b3123e08417b1df75b3e9b3d"
  executor = "docker"
  [runners.docker]
    tls_verify = false
    image = "ruby:2.1"
    privileged = false
    disable_cache = false
    volumes = ["/cache"]
  [runners.cache]
    Insecure = false
```

You can read all about `config.toml` in the [official documentation][toml].

## Update the GitLab Runner

Updating the GitLab Runner is as easy as updating your Ubuntu system:

```
apt-get update
apt-get install gitlab-ci-multi-runner
```

## Conclusion

In this brief tutorial we explored how to install and set up our own GitLab
Runner on DigitalOcean. Following the steps from top to bottom shouldn't take
more than 10 minutes. If you stumble upon any issues while your project builds,
make sure to read the [troubleshooting FAQs][faq].

For a more detailed tutorial on GitLab Runner and CI, be sure to check a
previous tutorial on
[Setting up GitLab Runner For Continuous Integration][runci] which provides a
detailed real world example.

If you are new to GitLab CI, you can follow our [Quick start guide][guide] to
get you started.

[![Powered by DigitalOcean](/images/blogimages/powered-by-do-badge-gray.png)](https://www.digitalocean.com)

[doc-runners]: http://doc.gitlab.com/ce/ci/runners/README.html
[doc-ci]: /gitlab-ci
[1_1]: /2016/03/29/gitlab-runner-1-1-released/
[autoscale-post]: /2016/04/05/shared-runners/
[digitalocean]: https://www.digitalocean.com
[one-docker]: https://www.digitalocean.com/features/one-click-apps/docker/
[chart]: https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/README.md#compatibility-chart
[cloud]: https://cloud.digitalocean.com
[doc-install]: https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/tree/master/docs/install
[toml]: https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/configuration/advanced-configuration.md
[runci]: /2016/03/01/gitlab-runner-with-docker/
[guide]: http://doc.gitlab.com/ce/ci/quick_start/README.html
[faq]: https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/faq/README.md
