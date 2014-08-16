---
kind: "article"
created_at: "2012-06-22 19:33:17 +04:00"
title: "Install LXC (Linux Containers)"
tags: [ 'lxc', 'linux' ]
---
<pre><code class='bash'>$ sudo apt-get install lxc dnsmasq
$ sudo lxc-create -n name -t ubuntu
</code></pre>
create /etc/network/if-up.d/lxc
<pre><code class='bash'>#!/bin/bash
# script to setup a natted network for lxc guests
CMD_BRCTL=/sbin/brctl
CMD_IFCONFIG=/sbin/ifconfig
CMD_IPTABLES=/sbin/iptables
CMD_ROUTE=/sbin/route
NETWORK_BRIDGE_DEVICE_NAT=lxc-bridge-nat
HOST_NETDEVICE=eth0
PRIVATE_GW_NAT=10.3.0.1
PRIVATE_NETMASK=255.255.0.0

${CMD_BRCTL} addbr ${NETWORK_BRIDGE_DEVICE_NAT}
${CMD_BRCTL} setfd ${NETWORK_BRIDGE_DEVICE_NAT} 0
${CMD_IFCONFIG} ${NETWORK_BRIDGE_DEVICE_NAT} ${PRIVATE_GW_NAT} netmask ${PRIVATE_NETMASK} promisc up
${CMD_IPTABLES} -t nat -A POSTROUTING -o ${HOST_NETDEVICE} -j MASQUERADE
echo 1 > /proc/sys/net/ipv4/ip_forward
</code></pre>
insert in */var/lib/lxc/name/config*
<pre><code class='bash'>lxc.network.type = veth
lxc.network.flags = up
lxc.network.link = lxc-bridge-nat
lxc.network.name = eth0
lxc.network.hwaddr = ac:de:48:00:0x:xx
lxc.network.ipv4 = 10.0.2.xxx/24
</code></pre>
<pre><code class='bash'>echo "nameserver 8.8.8.8" > /var/lib/lxc/name/rootfs/etc/resolvconf/resolv.conf.d/base
</code></pre>
edit */var/lib/lxc/name/rootfs/etc/network/interfaces*
<pre><code class='bash'>auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
  address   10.0.2.xxx
  netmask   255.255.255.0
  gateway   10.0.2.1
</code></pre>
run
<pre><code class='bash'>$ sudo lxc-start --name name_container
</code></pre>
login *root* / password *root*

for boot on startup  
LXC < 0.7.5
<pre><code class='bash'>$ sudo ln -s /var/lib/lxc/name/config /etc/lxc/name.conf
</code></pre>
edit */etc/default/lxc* add
<pre><code class='bash'>CONTAINERS="name"
</code></pre>
LXC >=0.7.5
<pre><code class='bash'>$ sudo ln -s /var/lib/lxc/name/config /etc/lxc/auto/name.conf
</code></pre>
