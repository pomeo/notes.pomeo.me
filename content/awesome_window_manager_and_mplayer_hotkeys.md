---
kind: "article"
created_at: "06/21/2012 19:25"
title: "awesome window manager and mplayer hotkeys"
tags: [ 'mplayer', 'awesome' ]
---
mplayer
<pre><code class='bash'>mkfifo ~/.mplayer/mplayer.pipe
mplayer -slave -input file=~/.mplayer/mplayer.pipe
</code></pre>
test
<pre><code class='bash'>echo "pause" > ~/.mplayer/mplayer.pipe
</code></pre>
xev
<pre><code class='bash'>KeyPress event, serial 28, synthetic NO, window 0x3400001,
    root 0x15a, subw 0x0, time 20967870, (191,146), root:(832,554),
    state 0x0, keycode >>>>>146<<<<< (keysym 0xff6a, XF86Pause), same_screen YES,
    XLookupString gives 0 bytes: 
    XmbLookupString gives 0 bytes: 
    XFilterEvent returns: False
</code></pre>
/etc/xdg/awesome/rc.lua
<pre><code class='bash'>awful.key({}, "#146", function () os.execute("echo pause > ~/.mplayer/mplayer.pipe") end),
</code></pre>
