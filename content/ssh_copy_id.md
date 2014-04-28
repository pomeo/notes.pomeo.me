---
kind: "article"
created_at: "2014-04-20 28:36:17 +04:00"
title: "copy pubkey without ssh-copy-id"
tags: [ 'key', 'ssh' ]
---
<pre><code>cat ~/id_dsa.pub | ssh user@host \
"(cat > tmp.pubkey ; mkdir -p .ssh ; touch .ssh/authorized_keys ; \
sed -i.bak -e '/$(awk '{print $NF}' ~/id_dsa.pub)/d' .ssh/authorized_keys; \
cat tmp.pubkey >> .ssh/authorized_keys; rm tmp.pubkey)"
</code></pre>

