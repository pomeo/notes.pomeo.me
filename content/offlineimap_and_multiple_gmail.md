---
kind: "article"
created_at: "2012-06-17 16:24:17 +04:00"
title: "offlineimap and multiple gmail"
tags: [ 'offlineimap', 'gmail' ]
---
~/.offlineimaprc
<pre><code class='bash'>[general]
accounts = account1@gmail.com, account2@gmail.com, account3@gmail.com
maxsyncaccounts = 3
socktimeout = 60
ui = TTY.TTYUI

[Account account1@gmail.com]
localrepository = account1@gmail.com-local
remoterepository = account1@gmail.com-remote

[Repository account1@gmail.com-local]
type = Maildir
localfolders = ~/Mail/account1@gmail.com

[Repository account1@gmail.com-remote]
type = IMAP
remotehost = imap.gmail.com
remoteuser = account1@gmail.com
remotepass = password
ssl = yes
realdelete = no

[Account account2@gmail.com]
localrepository = account2@gmail.com-local
remoterepository = account2@gmail.com-remote

[Repository account2@gmail.com-local]
type = Maildir
localfolders = ~/Mail/account2@gmail.com

[Repository account2@gmail.com-remote]
type = IMAP
remotehost = imap.gmail.com
remoteuser = account2@gmail.com
remotepass = password
ssl = yes
realdelete = no

[Account account3@gmail.com]
localrepository = account3@gmail.com-local
remoterepository = account3@gmail.com-remote

[Repository account3@gmail.com-local]
type = Maildir
localfolders = ~/Mail/account3@gmail.com

[Repository account3@gmail.com-remote]
type = IMAP
remotehost = imap.gmail.com
remoteuser = account3@gmail.com
remotepass = password
ssl = yes
realdelete = no
</code></pre>

**crontab -e**

<pre><code class='bash'>*/10 * * * * offlineimap -o -q -u Noninteractive.Basic
* */1 * * * offlineimap -o -u Noninteractive.Basic
</code></pre>
