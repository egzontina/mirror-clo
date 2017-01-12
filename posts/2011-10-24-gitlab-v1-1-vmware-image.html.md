--- 
title: gitlab v1.1 vmware image
wordpress_id: 8
wordpress_url: http://blog.gitlabhq.com/?p=7
date: 2011-10-24 12:17:18 +00:00
comments: false
---
<h3>1. Download (501 MB)
<a title="ubuntu server 10.04" href="http://downloads.gitlabhq.com/gitlab-ubuntu-server-10.04-amd64.zip">http://downloads.gitlabhq.com/gitlab-ubuntu-server-10.04-amd64.zip</a>
</h3>


<h3>2. Access to virtual machine:</h3>
user: notroot
pass: gitlabhq

<h3>3. Important! After login - rebuild ssh keys</h3>

<code>ssh-keygen -t rsa
sudo -H -u git gitosis-init &lt; ~/.ssh/id_rsa.pub</code>

<h3>4. Login via web. Admin login details for webUI</h3>

user: admin@local.host
pass: 5iveL!fe

<hr/>


<em>VirtualBox also support</em>
