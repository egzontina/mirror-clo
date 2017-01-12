---
title: "Security Webcast with Yubico"
author: Amara Nwaigwe
author_twitter: its_amaracle
categories: integration
image_title: '/images/blogimages/fido-u2f-yubikey.jpg'
description: "GitLab and Yubico discuss security best practices for Git users."
twitter_image: '/images/tweets/gitlab-and-yubico-security-webcast.png'
---

{::options parse_block_html="true" /}

Git is distributed, meaning that people can maintain a copy of the source code. While Git’s distributed nature is what makes it so
popular amongst developers, it is also what makes it a security concern to enterprises. The concern is that your source code is only
as secure as the machine it’s been copied. Each of these devices could be a point of exposure. We understand how important it
is to maintain the integrity of your source code.

With the release of [GitLab 8.9][8.9] we announced that we partnered with [Yubico][youb-home] to help
customers strengthen their authentication process with YubiKeys. YubiKeys are a single key providing universal 2nd factor
authentication into an unlimited number of applications. After [our announcement][yub], we asked Yubico to join us on a webcast. In this
webcast, we talked about common security threats and how you can use GitLab and Yubico to protect your private data
and maintain a secure Git repo as a single source of truth.

<!-- more -->

## In this Webcast

- Top security threats
- Inside look at how YubiKeys work
- Demo of setting up and using a YubiKey with GitLab
- Demo GitLab’s additional security capabilities beyond authentication
- Industry best practices for securing your Git repository

## Recording & Slides

<figure class="video_container">
  <iframe src="https://www.youtube.com/embed/pO9-7R3N5Ok" frameborder="0" allowfullscreen="true"> </iframe>
</figure>

<br>

<figure class="video_container">
<iframe src="https://docs.google.com/presentation/d/175zQz9CcQf3fQ65rbYFH_ysgllEkXrtnjYpAH_CDcrc/embed?start=false&loop=false&delayms=5000" frameborder="0" width="1280" height="749" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>
</figure>

## Key Takeaways

If you don’t have time to watch the full video, here are the highlights.

<div class="panel panel-info">
**Definition of a YubiKey**
{: .panel-heading}
<div class="panel-body">
A [YubiKey][what-is] is a small hardware device that offers two-factor authentication with a simple touch of a button.
</div>
</div>

<div class="panel panel-success">
**Reasons YubiKeys are preferred over 2FA via SMS**
{: .panel-heading}
<div class="panel-body">
From a security standpoint, push notifications and SMS codes (a form of [One-time Passwords][1-t-pass]) are all
vulnerable to phishing attacks and replay attacks. Getting a bit technical here, if you are using the U2F protocol
with the YubiKey, a properly implemented U2F registration flow contains Origin (phishing protection!) information
as well as TLS Channel Identification information (Man in the Middle attack protection). Finally, the
challenge-response piece of the U2F protocol provides complete replay attack protection.
</div>
</div>

<div class="panel panel-gitlab">
**GitLab + YubiKey** 
{: .panel-heading}
<div class="panel-body">
Our goal is to secure our customer’s work with proven, seamless solutions. The YubiKey provides
[one-touch authentication][touch], reducing the number of steps users have to take to access their accounts.
Remembering and entering passwords or pins can be a cumbersome process. Hopefully, YubiKeys can reduce some
of that friction and encourage more teams to secure their GitLab instance.
</div>
</div>

<div class="panel panel-danger">
**GitLab's additional security capabilities beyond authentication**
{: .panel-heading}
<div class="panel-body">
- Access and permissions: control who has access to your repositories
- Workflow management: control what changes are being made to your repositories
- Audit trail: keep a record of what happened within you GitLab instance
</div>
</div>

<div class="panel panel-gitlab-purple">
**Nine security best practices**
{: .panel-heading}
<div class="panel-body">
Of course there are many more than just nine. These were the ones that stuck out to us but for more resources
take a look at [InfoSec’s article on security best practices for Git users][post] and you can also check out
the [security section][hand] of our employee handbook.

1. Assign strong passwords and store in an encrypted vault (e.g., [1Password][1-pass]).
2. Never reuse your passwords across accounts.
3. Ensure proper user identity by restricting the use of shared or system accounts.
4. Enforce two-factor authentication.
5. Maintain a single secure repository.
6. Assign and review the proper access and permissions levels to projects.
7. Only use HTTPS or SSH to access git repositories, git repository management software, CI systems and ticketing / bug tracking systems.
8. Enforce integrity checks on all incoming objects by setting `transfer.fsckObjects`, `fetch.fsckObjects` and `receive.fscObjects` to `true`.
9. Enforce usage of `.gitignore` files by providing a proper `.gitignore` file content to all current and future projects.
</div>
</div>

As always, if you have any questions feel free to comment on this post or [tweet at us].

<!-- identifiers -->

[1-pass]: https://1password.com/
[1-t-pass]: https://en.wikipedia.org/wiki/One-time_password
[8.9]: https://about.gitlab.com/2016/06/22/gitlab-8-9-released/
[hand]: https://about.gitlab.com/handbook/security/
[post]: http://resources.infosecinstitute.com/security-best-practices-for-git-users/
[touch]: https://www.yubico.com/2015/11/yubico-docker-codesign/
[tweet at us]: https://twitter.com/gitlab
[what-is]: https://www.yubico.com/faq/yubikey/
[yub]: https://about.gitlab.com/2016/06/22/gitlab-adds-support-for-u2f/
[youb-home]: https://www.yubico.com/

<!-- custom styles -->

<style>
.panel-gitlab {
  border-color: rgba(252,163,38,.3);
}
.panel-gitlab > .panel-heading {
  color: rgb(226,67,41);
  background-color: rgba(252,163,38,.3);
  border-color: rgba(252,163,38,.3);
}
.panel-gitlab-purple {
  border-color: rgba(107,79,187,.3);
}
.panel-gitlab-purple > .panel-heading {
  color: rgb(107,79,187);
  background-color: rgba(107,79,187,.3);
  border-color: rgba(107,79,187,.3);
}
</style>
