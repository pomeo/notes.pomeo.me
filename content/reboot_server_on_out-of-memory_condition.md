---
kind: "article"
created_at: "2013-06-06 11:01:42 +04:00"
title: "reboot server on out-of-memory condition"
tags: [ 'server' ]
---
***/etc/sysctl.conf***
<pre><code class='bash'>vm.panic_on_oom=1
kernel.panic=10
</code></pre>
The vm.panic_on_oom=1 line enables panic on OOM, the kernel.panic=10 line tells the kernel to reboot ten seconds after panicking.
