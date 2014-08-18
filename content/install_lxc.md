---
kind: "article"
created_at: "2012-06-22 19:33:17 +04:00"
title: "Install LXC (Linux Containers)"
tags: [ 'lxc', 'linux' ]
---
<pre><code class='bash'>apt-get install lxc dnsmasq</code></pre>
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
*/etc/default/dnsmasq*
<pre><code class='bash'>ENABLED=1</code></pre>
*/etc/dnsmasq.conf*
<pre><code class='bash'>interface=lxc-bridge-nat
except-interface=eth0</code></pre>
*/etc/default/lxc*
<pre><code class='bash'>LXC_AUTO="true"</code></pre>
*/etc/default/lxc-net*
<pre><code class='bash'>USE_LXC_BRIDGE="false"
LXC_BRIDGE="lxcbr0"
LXC_ADDR="10.3.0.1"
LXC_NETMASK="255.255.0.0"
LXC_NETWORK="10.3.0.0/24"
LXC_DHCP_RANGE="10.3.0.2,10.3.0.254"
LXC_DHCP_MAX="253"
</code></pre>
*/etc/lxc/default.conf*
<pre><code class='bash'>lxc.network.type = veth
lxc.network.link = lxc-bridge-nat
lxc.network.flags = up
lxc.network.hwaddr = 00:16:3e:xx:xx:xx
lxc.start.auto = 1
lxc.start.delay = 5
lxc.start.order = 50
#lxc.network.ipv4.gateway = auto
</code></pre>
run
<pre><code class='bash'>lxc-create -n name -t ubuntu</code></pre>
*/etc/dnsmasq.d/lxc*
<pre><code class='bash'>#bind-interfaces
#except-interface=lxcbr0

dhcp-range=10.3.0.2,10.3.0.253,255.255.0.0
dhcp-host=00:16:3e:xx:xx:xx,10.3.x.x
dhcp-host=00:16:3e:xx:xx:xx,10.3.x.x
</code></pre>
restart all
<pre><code class='bash'>service lxc stop
service dnsmasq restart
service lxc start
lxc-ls --fancy
</code></pre>
