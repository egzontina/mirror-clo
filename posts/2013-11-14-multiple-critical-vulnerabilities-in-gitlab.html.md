---
title: "Multiple critical vulnerabilities in GitLab"
date: 2013-11-14 15:00
author: Jacob Vosmaer
categories:
community: true
---
### Multiple critical vulnerabilities in GitLab
New critical vulnerabilities recently discovered in GitLab enable unauthenticated API access, remote code execution, local file inclusion and unauthorized access to private repositories. All users should update GitLab and gitlab-shell immediately.

_Update (18 November 2013): added CVE numbers._

<!--more-->

### Releases
GitLab 5.4.2 and GitLab CE 6.2.4 are available from https://gitlab.com/gitlab-org/gitlab-ce and https://github.com/gitlabhq/gitlabhq; update instructions can be found in https://github.com/gitlabhq/gitlabhq/blob/master/doc/update/patch_versions.md . For more information about GitLab EE 6.2.1 see [our blog post on GitLab.com](http://www.gitlab.com/2013/11/14/multiple-security-vulnerabilities-in-gitlab/).

Gitlab-shell 1.7.8 is available from https://gitlab.com/gitlab-org/gitlab-shell and https://github.com/gitlabhq/gitlab-shell . To upgrade gitlab-shell it suffices to run `sudo su git -c 'git fetch && git checkout v1.7.8'` in /home/git/gitlab-shell .

### Credits
Thanks to joernchen of [Phenoelit](http://www.phenoelit.org/) for reporting these vulnerabilities to us.

# Unauthenticated API access to GitLab when using MySQL
There is an unauthenticated API access vulnerability in all version of GitLab. This vulnerability has been assigned CVE identifier CVE-2013-4580.

Versions affected: all

Fixed versions: 5.4.2, Community Edition 6.2.4, Enterprise Edition 6.2.1

### Impact
On GitLab installations which use MySQL as their database backend it is possible for an attacker to assume the identity of any existing GitLab user in certain API calls. This attack can be performed by unauthenticated users.

This vulnerability has been fixed in GitLab 5.4.2, GitLab Community Edition 6.2.4 and GitLab Enterprise Edition 6.2.1.

### Workarounds
If you are unable to upgrade you should apply the following patch and restart GitLab.

<pre>
--- a/lib/api/helpers.rb
+++ b/lib/api/helpers.rb
@@ -6,19 +6,23 @@ module API
     SUDO_PARAM = :sudo
 
     def current_user
-      @current_user ||= User.find_by_authentication_token(params[PRIVATE_TOKEN_PARAM] || env[PRIVATE_TOKEN_HEADER])
+      private_token = (params[PRIVATE_TOKEN_PARAM] || env[PRIVATE_TOKEN_HEADER]).to_s
+      @current_user ||= User.find_by_authentication_token(private_token)
       identifier = sudo_identifier()
</pre>

# Remote code execution vulnerability via Git SSH access in GitLab
There is a remote code execution vulnerability via Git SSH access in GitLab. This vulnerability has been assigned CVE identifier CVE-2013-4581.

Versions affected: 5.0 and newer

Not affected: 4.2 and older

Fixed versions: 5.4.2, Community Edition 6.2.4, Enterprise Edition 6.2.1 (running gitlab-shell 1.7.8)

### Impact
In affected versions an attacker can execute arbitrary code on a GitLab server by pushing carefully crafted changes via Git over SSH. This attack requires a GitLab user with an associated SSH key.

This vulnerability has been fixed in gitlab-shell 1.7.8, which is known to work with GitLab 5.4 and newer. All users should update gitlab-shell to version 1.7.8 immediately.

### Workarounds
If you are unable to upgrade, please apply the following patch in `/home/git/gitlab-shell`.
<pre>
--- a/lib/gitlab_config.rb
+++ b/lib/gitlab_config.rb
@@ -48,12 +48,12 @@ class GitlabConfig
     if redis.empty?
       # Default to old method of connecting to redis
       # for users that haven't updated their configuration
-      "env -i redis-cli"
+      %W(env -i redis-cli)
     else
       if redis.has_key?("socket")
-        "#{redis['bin']} -s #{redis['socket']}"
+        %W(#{redis['bin']} -s #{redis['socket']})
       else
-        "#{redis['bin']} -h #{redis['host']} -p #{redis['port']}"
+        %W(#{redis['bin']} -h #{redis['host']} -p #{redis['port']})
       end
     end
   end

--- a/lib/gitlab_update.rb
+++ b/lib/gitlab_update.rb
@@ -1,5 +1,6 @@
 require_relative 'gitlab_init'
 require_relative 'gitlab_net'
+require 'json'
 
 class GitlabUpdate
   attr_reader :config
@@ -53,7 +54,8 @@ class GitlabUpdate
   end
 
   def update_redis
-    command = "#{config.redis_command} rpush '#{config.redis_namespace}:queue:post_receive' '{\"class\":\"PostReceive\",\"args\":[\"#
-    system(command)
+    queue = "#{config.redis_namespace}:queue:post_receive"
+    msg = JSON.dump({'class' => 'PostReceive', 'args' => [@repo_path, @oldrev, @newrev, @refname, @key_id]})
+    system(*config.redis_command, 'rpush', queue, msg, err: '/dev/null', out: '/dev/null')
   end
 end
</pre>

# Local file inclusion vulnerability in GitLab
There is a local file inclusion vulnerability in GitLab. This vulnerability has been assigned CVE identifier CVE-2013-4582.

Versions affected: 5.0 and newer

Not affected: 4.2 and older

Fixed versions: 5.4.2, Community Edition 6.2.4, Enterprise Edition 6.2.1 (running gitlab-shell 1.7.8)

### Impact
In affected versions an attacker can include the contents of a local file in the metadata of a Git repository hosted on the server via the GitLab web interface. This vulnerability can only be exploited by authenticated GitLab users.

This vulnerability has been fixed in gitlab-shell 1.7.8, which is known to work with GitLab 5.4 and newer. All users should update gitlab-shell to version 1.7.8 immediately.

### Workarounds
If you are unable to upgrade you should apply the following patch in `/home/git/gitlab-shell`.

<pre>
--- a/lib/gitlab_projects.rb
+++ b/lib/gitlab_projects.rb
@@ -48,7 +48,7 @@ class GitlabProjects
   def create_branch
     branch_name = ARGV.shift
     ref = ARGV.shift || "HEAD"
-    cmd = %W(git --git-dir=#{full_path} branch #{branch_name} #{ref})
+    cmd = %W(git --git-dir=#{full_path} branch -- #{branch_name} #{ref})
     system(*cmd)
   end
 
@@ -61,7 +61,7 @@ class GitlabProjects
   def create_tag
     tag_name = ARGV.shift
     ref = ARGV.shift || "HEAD"
-    cmd = %W(git --git-dir=#{full_path} tag #{tag_name} #{ref})
+    cmd = %W(git --git-dir=#{full_path} tag -- #{tag_name} #{ref})
     system(*cmd)
   end
 
@@ -94,7 +94,7 @@ class GitlabProjects
   def import_project
     @source = ARGV.shift
     $logger.info "Importing project #{@project_name} from <#{@source}> to <#{full_path}>."
-    cmd = %W(git clone --bare #{@source} #{full_path})
+    cmd = %W(git clone --bare -- #{@source} #{full_path})
     system(*cmd) && create_hooks(full_path)
   end
 
@@ -156,7 +156,7 @@ class GitlabProjects
     end
 
     $logger.info "Forking project from <#{full_path}> to <#{full_destination_path}>."
-    cmd = %W(git clone --bare #{full_path} #{full_destination_path})
+    cmd = %W(git clone --bare -- #{full_path} #{full_destination_path})
     system(*cmd) && create_hooks(full_destination_path)
   end
 
</pre>

# Repository access privilege escalation vulnerability in GitLab
There is a repository access privilege escalation vulnerability in GitLab. This vulnerability has been assigned CVE identifier CVE-2013-4583.

Versions affected: 5.0 and newer

Not affected: 4.2 and older

Fixed versions: 5.4.2, Community Edition 6.2.4, Enterprise Edition 6.2.1 (running gitlab-shell 1.7.8)

### Impact
In affected versions a GitLab user can escalate their repository access privileges and clone a repository that they should not have access to via Git SSH access. This vulnerability can only be exploited by authenticated GitLab users.

This vulnerability has been fixed in gitlab-shell 1.7.8, which is known to work with GitLab 5.4 and newer. All users should update gitlab-shell to version 1.7.8 immediately.

### Workarounds
If you are unable to upgrade you should apply the following patch in `/home/git/gitlab-shell`.

<pre>
--- a/lib/gitlab_shell.rb
+++ b/lib/gitlab_shell.rb
@@ -43,7 +43,7 @@ class GitlabShell
   def parse_cmd
     args = Shellwords.shellwords(@origin_cmd)
     @git_cmd = args[0]
-    @repo_name = args[1]
+    @repo_name = escape_path(args[1])
   end
 
   def git_cmds
@@ -86,4 +86,12 @@ class GitlabShell
   def log_username
     @config.audit_usernames ? username : "user with key #{@key_id}"
   end
+
+  def escape_path(path)
+    if File.absolute_path(path, repos_path) == File.join(repos_path, path)
+      path
+    else
+      raise "Wrong repository path"
+    end
+  end
 end

</pre>
