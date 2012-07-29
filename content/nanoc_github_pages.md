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
  # initialize the local repository
  $ git init
  $ git add .
  # commits your files
  $ git commit -am "init"
  # rename our master branch
  $ git branch -m master gh-pages
  # add your github repository as origin
  $ git remote add origin git@github.com:[user]/[name].git
  # push to the remote repository
  $ git push origin gh-pages
</code></pre>
