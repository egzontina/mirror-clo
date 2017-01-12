--- 
title: Migrating to mysql
wordpress_id: 260
wordpress_url: http://blog.gitlabhq.com/?p=260
date: 2012-03-12 07:28:15 +00:00
community: true
---
Now mysql is officially supported by gitlabhq. 
Follow next steps to migrate to mysql

1. Get latest code
2. Install mysql
3. Save data - `bundle exec rake db:data:dump RAILS_ENV=production`
4. Change config to mysql using `database.yml.example`
5. Setup db - `bundle exec rake db:setup RAILS_ENV=production`
6. Restore old data - `bundle exec rake db:data:load RAILS_ENV=production`
