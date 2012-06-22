---
kind: "article"
created_at: "06/22/2012 19:25"
title: "Install hubot on ubuntu"
tags: [ 'hubot', 'supervisor', 'nodejs' ]
---
[Hubot](http://hubot.github.com/)
<pre><code class='bash'>$ sudo useradd -s '/bin/bash' -d '/home/hubot' -m hubot
$ sudo apt-get install supervisor git-core curl build-essential libssl-dev pkg-config libexpat1-dev libicu-dev
$ sudo su hubot && cd ~
$ git clone git://github.com/creationix/nvm.git ~/.nvm
$ . ~/.nvm/nvm.sh
$ nvm install v0.x.x
$ nvm use v0.x.x
$ npm install -g hubot hubot-gtalk coffee-script
</code></pre>
and without '-g'
<pre><code class='bash'>$ npm install node-stringprep optparse
</code></pre>
create file
<pre><code class='bash'>/etc/supervisor/conf.d/hubot.conf
</code></pre>
with
<pre><code class='bash'>[program:hubot]
command=hubot -a gtalk
directory=/home/hubot
user=hubot
autostart=true
autorestart=true
startretries=3
stdout_logfile=/home/hubot/out.log
stdout_logfile_maxbytes=1MB
stdout_logfile_backups=10
stderr_logfile=/home/hubot/error.log
stderr_logfile_maxbytes=1MB
stderr_logfile_backups=10
stopsignal=TERM
environment=HOME='/home/hubot',USER='hubot',HUBOT_GTALK_USERNAME='user@google.com',
HUBOT_GTALK_PASSWORD='password',HUBOT_GTALK_WHITELIST_USERS='user@jabber.com'
</code></pre>
open
<pre><code class='bash'>/etc/init.d/supervisor
</code></pre>
find PATH and add **/home/hubot/.nvm/v0.x.x/bin**
<pre><code class='bash'>PATH=/home/hubot/.nvm/v0.x.x/bin:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr
</code></pre>
that’s all
<pre><code class='bash'>$ sudo service supervisor start
</code></pre>
look **/home/hubot/error.log** for errors
