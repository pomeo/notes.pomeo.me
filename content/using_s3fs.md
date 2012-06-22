---
kind: "article"
created_at: "06/21/2012 22:27"
title: "Using S3fs"
tags: [ 's3fs' ]
---
<pre><code class='bash'>$ sudo echo "AccessKeyID:SecretKey" > /etc/passwd-s3fs
</code></pre>
you can find AccessKeyID and SecretKey out under AWS Menu -> Your Account -> Security Credentials
<pre><code class='bash'>$ sudo chmod 640 /etc/passwd-s3fs
$ sudo s3fs bucketname /mountpoint
</code></pre>
**Setting up automatic mounts**  
add into /etc/fstab:
<pre><code class='bash'>s3fs#mybucket /mountpoint fuse url=https://s3.amazonaws.com 0 0
</code></pre>
Now you should be able to mount the filesystem with a regular mount command:

<pre><code class='bash'>$ sudo mount /mountpoint
</code></pre>
**More mount options**  
By default, Fuse will lock the access to a file down to whoever ran the Fuse command. So, if you mount a filesystem as user foo, only foo will be able to access the filesystem- even root can’t get to it! If you want to put an S3 filesystem in /etc/fstab and have root mount it at boot but have a regular user or group own the filesystem, you can set uid and/or gid in /etc/fstab:
<pre><code class='bash'>s3fs#mybucket /mountpoint fuse uid=500,gid=500,url=https://s3.amazonaws.com 0 0
</code></pre>
