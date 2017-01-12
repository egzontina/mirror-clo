---
title: GitLab High Availability Solutions
date: December 17, 2013
author: Marc Radulescu
---

We've just published an overview of [GitLab High Availability Solutions](https://www.gitlab.com/high-availability/). The subject of high availability (HA) has come up frequently with our customers. GitLab is a business-critical service for some of our users. We want to meet their concerns in keeping GitLab continuously available.

This web-page gives you a rough idea on what kind of HA setups to expect from us. So whether you are already interested in the topic, or only now realize it might be something worth looking into, we advise you to read it.

We aim to highlight the big trade-off between increasing uptime and accepting complexity/cost. The more uptime you want, the more complex the setup. And the more complex the setup, the costlier to maintain. Consequently, we've structured it starting with the simplest solution out there, which is a basic server back-up. We gradually add levels of complexity, going through manual and automated snapshots, dedicated servers, slaves, and finally discussing clustered/master-master filestore configurations. Fair warning though, there is no one-size-fits-all when it comes to high availability. Our page is by no means a go-to guide for setting up your HA GitLab installation. Use it as a step to start considering your options.

As always, feedback is more than welcome. Let us know how you feel about the page and our solutions. If there is something we missed, don't hesitate to point it out.
