---
title: "Big changes coming to GitHost"
date: 2015-12-30
author: Patricio Cano
author_twitter: suprnova32
image_title: '/images/unsplash/fireworks.jpeg'
---

Today we are announcing two big changes to the GitHost platform and to its plans and pricing. The changes are intended
to offer a better product with greater features and easier to use configuration options, to better reflect the storage
and memory needs organizations have for a hosted instance of GitLab, and to make it sustainable for us to offer a service
like GitHost. Please read on for all the details.

<!-- more -->

## Pricing changes

As of today, December 30th, 2015, the following changes will take effect:

### New GitHost plans with greater capacity

We have added three new plans: Business (80GB SSD), Business Pro (160GB SSD), and Corporate (320GB SSD) to provide
organizations greater storage and memory capacity. We have also replaced two of our smaller plans (Starter and
Developer) with one plan: Developer (30GB SSD) to meet the needs of smaller teams.

We also still have the Startup plan (60GB SSD) which offers a suitable mid-range for medium-sized teams.

![Plans](/images/githost/plans.png)

We wanted to increase the choices available, and to raise the price compared to our older plans in order to make GitHost
sustainable. We plan on offering this service for a long time to come, and the old prices did not cover our cost to
keep the platform running.

**What does this mean if you’re an existing subscriber?**

For current GitHost subscribers, you will be grandfathered for 2 years on your current plan and price. We also will
extend a 40% discount off current prices, if you should choose to upgrade your plan at anytime within this 2 year period.

As of January, 2018 the new pricing for GitHost will apply to existing subscribers.

If you have questions about the changes or about pricing in general, please [contact us](https://about.gitlab.com/sales/).

## New Features

### GitLab Enterprise Edition is now available

We are making GitLab Enterprise Edition available within GitHost. Organizations needing deeper authentication and
authorization integration, fine-grained workflow management, extra server management options, and integration with their
tool stack can now easily deploy an EE instance in minutes. Use of the Enterprise Edition requires you to have a valid
license. If you would like to purchase GitLab Enterprise Edition, you may do so by going to
[https://about.gitlab.com/pricing/](https://about.gitlab.com/pricing/).

![CE & EE](/images/githost/ce-ee.png)

### Omniauth Providers

With today's upgrade we are releasing a feature that will allow all users to configure any Omniauth provider supported
by GitLab in the easiest way possible. Simply click on the icon of the provider you want to activate, fill in the
details required and save your changes. You no longer need to edit the `gitlab.rb` file manually.

After editing these details, a reconfigure of your instance will be required. To do this, simply click on the **Reconfigure**
button on your instance view and all the configuration changes you made will be applied.

![Omniauth Provider](/images/githost/omniauth.png)

### LDAP

Easy LDAP configuration has also been added to GitHost. The configuration is pretty similar to the Omniauth configuration,
and if you have an Enterprise Edition instance, you can add more than one.

Like with Omniauth, changes will not be automatically applied. You will need to run a manual reconfigure for changes to
take effect. This can be done in the main instance view.

![LDAP Server](/images/githost/ldap.png)

### Redesign

As you can see from the screenshots above, the overall look and feel of [GitHost.io](https://githost.io) has also been
improved, making it cleaner, sleeker and easier on the eyes. All the changes we are announcing today will help us grow,
improve our platform and ultimately offer all our customers a better service. Thank you for your continued support!
