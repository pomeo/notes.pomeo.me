---
kind: "article"
created_at: "06/21/2012 20:44"
title: "Mutt and SMTP Gmail/Google Apps"
tags: [ 'mutt', 'gmail', 'google apps' ]
---
<pre><code class='bash'>set postponed = "+[Gmail].Drafts" #offlineimap
set record = "+[Gmail].Sent\ Mail" #offlineimap
set smtp_pass = Password
set smtp_url = "smtp://user@domain.com@smtp.gmail.com:587/"
set from = "user@domain.com"
set realname = "Name"
</code></pre>
