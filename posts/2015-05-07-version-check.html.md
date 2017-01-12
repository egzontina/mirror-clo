---
title: "Version Check Functionality"
date: 2015-05-07
author: Sytse Sijbrandij
author_twitter: sytses
---

We're working on a version check function for GitLab to reduce the problem of outdated servers.
These servers are a security problem, provide a bad user experience and
lead to issues being created with problems that have already been solved.
By making outdated installations visible to its users we hope that people will upgrade sooner.

<!--more-->

## How it'll work

The version check will work in the following way. The `/help` page of GitLab will
load an image from _version.gitlab.com_. This image will show green for an
up to date version, yellow for an out of date version and red for a missing security update.

![No update necessary](/images/version_check/green.png)
![New version out!](/images/version_check/orange.png)
![Update ASAP](/images/version_check/red.png)

The image requests parameters requests will contain the GitLab version and the server hostname.
We'll store each request with a timestamp, the GitLab version and the server hostname.
We will not store the user ip-address.

We will send the server hostname to have more information about where and how GitLab is used.
Loading external images is similar to how the gravatar images of users are used.

### Opt-out

Just like the gravatar images you will be able to to turn off the functionality
if you don't want your GitLab server to connect outside the firewall.
The version check functionality can be disabled in the application settings.

## Trade-off

Providing the new package server and the version check server requires
constant maintenance and operational capacity.
Getting better insight into where and how GitLab is used
will help us improve GitLab for everyone.

We realize that it sending the server
hostname by default is not a trivial action and not everyone will be happy about this.
We think that ensuring the sustainability of GitLab package server and
version check services makes it a good trade-off.
There will always be an option to turn this behavior off.

Please let us know what you think about the above plan in the comments.

## Update

We decided against sending the hostname in the url of the picture request.
But the https picture request itself will have a HTTP referer header.
We can use that to see where and how GitLab is used.
We will still not store the ip-address of the requests.