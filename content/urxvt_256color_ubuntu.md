---
kind: "article"
created_at: "06/17/2012 16:10"
title: "urxvt 256color Ubuntu"
tags: [ 'ubuntu', 'urxvt', 'rxvt-unicode' ]
---
<pre><code class='bash'>mkdir urxvt
cd urxvt
apt-get source rxvt-unicode
cd rxvt-unicode-?.?/
patch -p1 < doc/urxvt-8.2-256color.patch
sudo apt-get build-dep rxvt-unicode
dpkg-buildpackage -us -uc -rfakeroot
sudo dpkg -i ../rxvt-unicode_?.?-1_i386(or amd64).deb
</code></pre>
make terminfo
<pre><code class='bash'>cd ~
infocmp -L rxvt-unicode > rxvt-unicode.terminfo
nano rxvt-unicode.terminfo
# Change from:
#    lines_of_memory#0, max_colors#88, max_pairs#256,
# to:
#    lines_of_memory#0, max_colors#256, max_pairs#32767
install -d .terminfo
tic -o .terminfo/ rxvt-unicode.terminfo
rm rxvt-unicode.terminfo
</code></pre>
Test [256colors.pl](http://notes.sovechkin.com/256colors.pl)
![256colors.pl](/images/256colors.png)

rxvt-256color unknown terminal type  
installing **ncurses-term** package
