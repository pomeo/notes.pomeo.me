---
kind: "article"
created_at: "2014-04-26 28:36:17 +04:00"
title: "express(node.js) + capistrano + supervisord"
tags: [ 'nodejs', 'capistrano', 'supervisord' ]
---
<pre><code>$ sudo apt-get install supervisor git-core curl build-essential libssl-dev pkg-config libexpat1-dev libicu-dev
$ sudo apt-get install libcairo2-dev libjpeg8-dev libgif-dev libpango1.0-dev g++ # not needed
$ curl https://raw.github.com/creationix/nvm/v0.x.x/install.sh | sh
$ source ~/.nvm/nvm.sh
$ nvm install 0.x
$ nvm alias default 0.x
</code></pre>
open
<pre><code class='bash'>/etc/init.d/supervisor
</code></pre>
find PATH and add */home/ubuntu/.nvm/v0.x.x/bin*
<pre><code class='bash'>PATH=/home/ubuntu/.nvm/v0.x.x/bin:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr
</code></pre>
***/etc/sudoers***
<pre><code class='bash'>ubuntu ALL=(ALL) PASSWD: ALL
ubuntu ALL=NOPASSWD: /usr/bin/supervisorctl
</code></pre>
gem specific_install -l https://github.com/pomeo/capistrano-offroad

***./config/deploy.rb***
<pre><code class='bash'>#========================
#CONFIG
#========================
set :application, "site"
#========================
#CONFIG
#========================
require           "capistrano-offroad"
offroad_modules   "defaults", "supervisord"
set :repository,  "git@github.com:user/#{application}.git"
set :supervisord_start_group, "name"
set :supervisord_stop_group, "name"
#========================
#ROLES
#========================
set  :gateway,    "#{application}"  # main server
role :app,        "ubuntu@10.3.x.x" # lxc container
 
after "deploy:create_symlink", "deploy:npm_install", "deploy:restart"
</code></pre>
***/etc/supervisor/conf.d/site.conf***
<pre><code class='bash'>[program:site]
command=node app.js
directory=/home/ubuntu/www/current/
user=nobody
autostart=true
autorestart=true
startretries=3
stdout_logfile=/home/ubuntu/www/logs/server.log
stdout_logfile_maxbytes=1MB
stdout_logfile_backups=10
stderr_logfile=/home/ubuntu/www/logs/error.log
stderr_logfile_maxbytes=1MB
stderr_logfile_backups=10
stopsignal=TERM
environment=NODE_ENV='production'
</code></pre>
that’s all
<pre><code class='bash'>$ sudo service supervisor stop/start # not restart
</code></pre>
***cap deploy:status*** - show supervisor processes  
***cap deploy:restart*** - restart all node.js
