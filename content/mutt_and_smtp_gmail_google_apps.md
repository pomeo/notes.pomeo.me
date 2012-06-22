---
kind: "article"
created_at: "2012-06-21 20:44:17 +04:00"
title: "Mutt and SMTP Gmail/Google Apps"
tags: [ 'mutt', 'gmail', 'googleapps' ]
---
<pre><code class='bash'>set postponed = "+[Gmail].Drafts" #offlineimap
set record = "+[Gmail].Sent\ Mail" #offlineimap
set smtp_pass = Password
set smtp_url = "smtp://user@domain.com@smtp.gmail.com:587/"
set from = "user@domain.com"
set realname = "Name"
</code></pre>
