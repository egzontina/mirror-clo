---
title: "Feature Highlight: LDAP Integration"
date: 2014-07-10
categories:
author: Job van der Voort, Jacob Vosmaer
---

GitLab is a massive open source project with over 600 contributors, all working together to create an amazing platform to collaborate on code. Every month on the 22nd, a new version of GitLab is released, and every month new features are added.
To make you aware of the power of GitLab, we walk through some of its features in these blog posts.

Previously, [we looked at GitLab Groups](https://about.gitlab.com/2014/06/30/feature-highlight-groups/). This time, we're looking at a GitLab Enterprise Edition feature.
In [GitLab Enterprise Edition](https://about.gitlab.com/gitlab-ee/) it is possible to sync your GitLab groups with your LDAP groups, making it super easy to manage access to projects.

![LDAP Group Sync](/images/feature_ldap_sync/select_group_cn.png)

<!--more-->

LDAP group synchronization in GitLab Enterprise Edition allows you to synchronize the members of a GitLab group with a given LDAP group.

### Setting up LDAP group synchronization

Suppose we want to synchronize the GitLab group 'example group' with the LDAP group 'Engineering'.

1. As an owner, go to the group settings page for 'example group'.

![LDAP group settings](/images/feature_ldap_sync/select_group_cn.png)

As an admin you can also go to the group edit page in the admin area.

![LDAP group settings for admins](/images/feature_ldap_sync/select_group_cn_admin.png)

2. Enter 'Engineering' as the LDAP Common Name (CN) in the 'LDAP Group cn' field.

3. Enter a default group access level in the 'LDAP Access' field; let's say Developer.

![LDAP group settings filled in](/images/feature_ldap_sync/select_group_cn_engineering.png)

4. Save your changes to the group settings.

Now every time a member of the 'Engineering' LDAP group signs in, they automatically become a Developer-level member of the 'example group' GitLab group. Users who are already signed in will see the change in membership after up to one hour.

### Locking yourself out of your own group

As an LDAP-enabled GitLab user, if you create a group and then set it to synchronize with an LDAP group you do not belong to, you will be removed from the grop as soon as the synchronization takes effect for you.

If you accidentally lock yourself out of your own GitLab group, ask a GitLab administrator to change the LDAP synchronization settings for your group.

### Non-LDAP GitLab users

Your GitLab instance may have users on it for whom LDAP is not enabled.
If this is the case, these users will not be affected by LDAP group synchronization settings: they will be neither added nor removed automatically.

### ActiveDirectory nested group support

If you are using ActiveDirectory, it is possible to create nested LDAP groups: the 'Engineering' LDAP group may contain another LDAP group 'Software', with 'Software' containing LDAP users Alice and Bob.
GitLab will recognize Alice and Bob as members of the 'Engineering' group.

### LDAP documentation

Find this and further LDAP documentation in our [integration documentation](http://doc.gitlab.com/ee/integration/ldap.html).

