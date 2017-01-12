---
title: "Support for Universal 2nd Factor Authentication"
author: Amara Nwaigwe
author_twitter: its_amaracle
categories: 
image_title: '/images/blogimages/fido-u2f-yubikey.jpg'
---

With the [release of GitLab 8.9](https://about.gitlab.com/2016/06/22/gitlab-8-9-released/), GitLab now supports the FIDO Universal 2nd Factor (U2F) protocol for user authentication with 
the added layer of hardware security from [YubiKey](https://www.yubico.com/products/yubikey-hardware/yubikey4/). We're excited to expand our authentication 
capabilities to include U2F devices. U2F changes the game for online authentication because
it uses public key cryptography and has built-in support to prevent phishing. This higher 
level of authentication enables developers to maintain the security of
their servers, code, sites, and more from a single source.

<!-- more -->

## Importance of account security 

With the steady rise of new devices and the growing capabilities of existing ones, the average
user logs into networks, applications, or platforms from a variety of different devices. While
device flexibility is great from a user perspective, it represents significant security
challenges for organizations and developers. Each new access point makes it tougher to fend off
malicious attacks particularly phishing while maintaining the integrity of accounts and systems.

## Support for U2F YubiKey

YubiKeys reduce the number of steps you have to take to access your accounts,
while still maintaining usability and providing secure authentication with just a touch of the 
YubiKey. With U2F, you can now authenticate by inserting their YubiKey into the
USB port when prompted. You'll activate your YubiKey by simply pressing the button on
the device.

The same U2F YubiKey that works with GitLab also works for logging into a growing number of
other services, including Google, Dropbox, and Dashlane, without any personal data or
encryption secrets shared between service providers. With YubiKeys, there are no drivers or
client software to install.  

## Enabling two-factor authentication via U2F

GitLab has supported two-factor authentication since the release of [GitLab 7.11](https://about.gitlab.com/2015/05/22/gitlab-7-11-released/), adding 
device-enabled 2nd factor authentication provides an additional layer of security. 
If you're interested in enabling two-factor authentication with a U2F device, follow the 
steps in our [documentation](http://docs.gitlab.com/ee/profile/two_factor_authentication.html#log-in-via-u2f-device). Of course, you have the option to choose the 
authentication method that is best for you. 
