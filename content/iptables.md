---
kind: "article"
created_at: "2013-06-06 10:07:34 +04:00"
title: "iptables"
tags: [ 'iptables' ]
---
<pre><code class='bash'>netstat -anp | grep LISTEN</code></pre>
***sudo nano /etc/iptables.firewall.rules***
<pre><code class='bash'>*filter

# MongoDB
-A INPUT -m state --state NEW -p tcp --destination-port 27017 -s x.x.x.x -j ACCEPT
-A OUTPUT -d x.x.x.x -p tcp --source-port 27017 -m state --state ESTABLISHED -j ACCEPT
-A INPUT -m state --state NEW -p tcp --destination-port 28017 -s x.x.x.x -j ACCEPT
-A OUTPUT -d x.x.x.x -p tcp --source-port 28017 -m state --state ESTABLISHED -j ACCEPT

# Redis
-A INPUT -m state --state NEW -p tcp --destination-port 6379 -s x.x.x.x -j ACCEPT
-A OUTPUT -d x.x.x.x -p tcp --source-port 6379 -m state --state ESTABLISHED -j ACCEPT

# RabbitMQ
-A INPUT -m state --state NEW -p tcp --destination-port 5672 -s x.x.x.x -j ACCEPT
-A OUTPUT -d x.x.x.x -p tcp --source-port 5672 -m state --state ESTABLISHED -j ACCEPT
-A INPUT -m state --state NEW -p tcp --destination-port 5673 -s x.x.x.x -j ACCEPT
-A OUTPUT -d x.x.x.x -p tcp --source-port 5673 -m state --state ESTABLISHED -j ACCEPT
-A INPUT -m state --state NEW -p tcp --destination-port 15672 -s x.x.x.x -j ACCEPT
-A OUTPUT -d x.x.x.x -p tcp --source-port 15672 -m state --state ESTABLISHED -j ACCEPT

# MariaDB
-A INPUT -m state --state NEW -p tcp --destination-port 3306 -s x.x.x.x -j ACCEPT
-A OUTPUT -d x.x.x.x -p tcp --source-port 3306 -m state --state ESTABLISHED -j ACCEPT

#  Allow all loopback (lo0) traffic and drop all traffic to 127/8 that doesn't use lo0
-A INPUT -i lo -j ACCEPT
-A INPUT ! -i lo -d 127.0.0.0/8 -j REJECT

#  Accept all established inbound connections
-A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

#  Allow all outbound traffic - you can modify this to only allow certain traffic
-A OUTPUT -j ACCEPT

#  Allow HTTP and HTTPS connections from anywhere (the normal ports for websites and SSL).
-A INPUT -p tcp --dport 80 -j ACCEPT
-A INPUT -p tcp --dport 443 -j ACCEPT

#  Allow ports for testing
-A INPUT -p tcp --dport 8080:8090 -j ACCEPT

#  Allow ports for MOSH (mobile shell)
-A INPUT -p udp --dport 60000:61000 -j ACCEPT

#  Allow SSH connections
-A INPUT -p tcp -m state --state NEW --dport 2222 -j ACCEPT

#  Allow ping
-A INPUT -p icmp -m icmp --icmp-type 8 -j ACCEPT

#  Log iptables denied calls
-A INPUT -m limit --limit 5/min -j LOG --log-prefix "iptables denied: " --log-level 7

#  Reject all other inbound - default deny unless explicitly allowed policy
-A INPUT -j REJECT
-A FORWARD -j REJECT

COMMIT</code></pre>
***sudo iptables-restore < /etc/iptables.firewall.rules***

***sudo nano /etc/network/if-pre-up.d/firewall***
<pre><code class='bash'>#!/bin/sh
/sbin/iptables-restore < /etc/iptables.firewall.rules</code></pre>
***sudo chmod +x /etc/network/if-pre-up.d/firewall***
