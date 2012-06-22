---
kind: "article"
created_at: "06/21/2012 22:40"
title: "Linux fastest console screenshot"
tags: [ 'screenshot', 'linux' ]
---
<pre><code class='bash'>xwd -root -screen -out screenshot.xwd
gm convert screenshot.xwd screenshot.png
</code></pre>
