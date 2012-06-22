---
kind: "article"
created_at: "2012-06-21 22:40:17 +04:00"
title: "Linux fastest console screenshot"
tags: [ 'screenshot', 'linux' ]
---
<pre><code class='bash'>xwd -root -screen -out screenshot.xwd
gm convert screenshot.xwd screenshot.png
</code></pre>
