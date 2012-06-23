---
kind: "article"
created_at: "2012-06-23 16:13:17 +04:00"
title: "deploy nanoc on github pages"
tags: [ 'nanoc', 'github' ]
---
nanoc workspace:
<pre><code class='bash'>root [ -> "master" ]
  |- content (nanoc templates)
  |- layouts (nanoc layouts)
  |- lib (ruby files extending nanoc)
  |- output [ -> "gh-pages" ]
</code></pre>
create the gh-pages branch
<pre><code class='bash'>  $ cd output
  # create the isolated branch
  $ git symbolic-ref HEAD refs/heads/master
  $ rm .git/index
  $ git clean -fdx
</code></pre>
in nanoc root
<pre><code class='bash'>  $ nanoc compile
</code></pre>
in **nanoc_root/output**
<pre><code class='bash'>  $ git checkout gh-pages
  $ git add .
  $ git commit -a -m "First pages commit"
  $ git push origin gh-pages
</code></pre>
