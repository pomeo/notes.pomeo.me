---
kind: "article"
created_at: "06/22/2012 19:01"
title: "node.js move file"
tags: [ 'nodejs' ]
---
<pre><code class='bash'>var is = fs.createReadStream(file1);
var os = fs.createWriteStream(file2);
      
util.pump(is, os, function() {
  fs.unlinkSync(file1);
});
</code></pre>
