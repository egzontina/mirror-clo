---
title: "GitLab 6.2.3 and 5.4.1 security releases"
date: 2013-11-04 19:00
author: Jacob Vosmaer
categories:
community: true
---
### GitLab CE 6.2 and 5.4 security releases

We have just released GitLab CE 6.2.3, CE 5.4.1 and [EE 6.2.0](http://www.gitlab.com/2013/11/04/gitlab-ee-6-2-security-release/). 
These releases fix two critical security issues that allow remote code execution. 
Both remote code injection attacks are only possible if you are logged in as a user on the GitLab server.
We advise everyone to upgrade immediately or apply the two workarounds described below.
When you are on 6.2 you can use the [universal update guide for patch versions](https://github.com/gitlabhq/gitlabhq/blob/master/doc/update/patch_versions.md) to upgrade.

<!--more-->

# Remote code execution vulnerability in the code search feature of GitLab

There is a remote code execution vulnerability in the code search feature of GitLab. This vulnerability has been assigned the CVE identifier CVE-2013-4489.

Versions affected: 5.2, 5.3, 5.4, 6.0, 6.1, 6.2

Not affected: 5.1 and earlier

Fixed Versions: 5.4.1, 6.2.3

### Impact
The Grit gem which serves as the Git backend for GitLab has an unsafe code path for internal use which allows strings to be evaluated by the Bourne shell. In affected versions, the GitLab code search feature exposes this unsafe code path to user input from the search box. Code search in GitLab is only available for authenticated users.

All users running an affected release should upgrade immediately or disable code search using the workaround below.

### Releases
The 5.4.1 and 6.2.3 releases are available from https://github.com/gitlabhq/gitlabhq and https://gitlab.com/gitlab-org/gitlab-ce .

### Workarounds
If you are unable to upgrade, you can disable code search by deleting the following line from `app/contexts/search_context.rb` and restarting GitLab:

<pre>
result[:blobs] = project.repository.search_files(query, params[:repository_ref]) unless project.empty_repo?
</pre>

### Credits
Thanks to joernchen of [Phenoelit](http://www.phenoelit.org/) for reporting the vulnerability to us.

# Remote code execution vulnerability in the SSH key upload feature of GitLab

There is a remote code execution vulnerability in the SSH key upload feature of GitLab. This vulnerability has been assigned the CVE identifier CVE-2013-4490.

Versions affected: 5.0, 5.1, 5.2, 5.3, 5.4, 6.0, 6.1, 6.2

Not affected: 4.2 and earlier

Fixed versions: 5.4.1, 6.2.3

### Impact
The gitlab-shell SSH access endpoint manages the authorized_keys file for the git user. When a user adds a public key using the GitLab web interface a gitlab-shell command is invoked to add the public key to authorized_keys. In affected versions, the public key text entered by the user is exposed to the Bourne shell in a way that can be exploited to achieve code execution as the git user. Only authenticated users can upload an SSH key.

All users running an affected release should upgrade gitlab-shell immediately.

### Releases
Gitlab-shell 1.7.4, available from https://github.com/gitlabhq/gitlab-shell, fixes the vulnerability and has been tested with GitLab 5.4.1 and GitLab 6.2.3.

### Workarounds
If you are using GitLab 5.0 or newer and you cannot upgrade to GitLab 5.4.1 or GitLab 6.2.3 you should apply the following edit to gitlab-shell.

<pre>
--- a/lib/gitlab_keys.rb
+++ b/lib/gitlab_keys.rb
@@ -29,8 +29,7 @@ class GitlabKeys
   def add_key
     $logger.info "Adding key #{@key_id} => #{@key.inspect}"
     cmd = "command=\"#{ROOT_PATH}/bin/gitlab-shell #{@key_id}\",no-port-forwarding,no-X11-forwarding,no-agent-forwarding,no-pty #{@key}"
-    cmd = "echo \'#{cmd}\' >> #{auth_file}"
-    system(cmd)
+    open(auth_file, 'a') { |file| file.puts(cmd) }
   end
 
   def rm_key
</pre>

### Credits
Thanks to Nigel Kukard of [AllWorldIT](http://www.allworldit.com/) for reporting the vulnerability to us.
