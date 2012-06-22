---
kind: "article"
created_at: "2012-06-21 21:33:17 +04:00"
title: "express(node.js) + capistrano + supervisord"
tags: [ 'nodejs', 'capistrano', 'supervisord' ]
---
***/etc/sudoers***
<pre><code class='bash'>user ALL=(ALL) PASSWD: ALL
user ALL=NOPASSWD: /usr/bin/supervisorctl
</code></pre>
gem install capistrano-offroad

***./config/deploy.rb***
<pre><code class='bash'> #========================
 #CONFIG
 #========================
 set :application, "site"

 require "capistrano-offroad"
 offroad_modules "defaults", "supervisord"
 set :supervisord_conf, "/etc/supervisor/supervisord.conf"
 set :supervisord_pidfile, "/var/run/supervisord.pid"

 set :appweb, "#{application}.com"
 set :repository,  "gitosis@git.yourgitserver.com:#{application}"
 set :user, "user"
 set :use_sudo, false
 set :deploy_via, :copy
 set :scm, :git
 #========================
 #ROLES
 #========================
 role :web, "#{appweb}"
 set :deploy_to, "/var/www/#{appweb}/www"
</code></pre>
***/etc/supervisor/conf.d/site.conf***
<pre><code class='bash'>[program:site]
 command=/usr/local/bin/node app.js
 directory=/var/www/site.com/www/current/
 user=nobody
 autostart=true
 autorestart=true
 startretries=3
 stdout_logfile=/var/www/site.com/www/shared/log/server.log
 stdout_logfile_maxbytes=1MB
 stdout_logfile_backups=10
 stderr_logfile=/var/www/site.com/www/shared/log/error.log
 stderr_logfile_maxbytes=1MB
 stderr_logfile_backups=10
 stopsignal=TERM
 environment=NODE_ENV=production
</code></pre>
***cap deploy:status*** - show supervisor processes  
***cap deploy:restart*** - restart all node.js
