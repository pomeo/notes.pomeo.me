---
kind: "article"
created_at: "2012-06-22 18:44:17 +04:00"
title: "node.js + socket.io = send message to one client"
tags: [ 'nodejs', 'socket.io' ]
---
<pre><code class='javascript'>//client
<script type="text/javascript">
  var socket = new io.Socket();
  socket.connect();
  socket.on('connect', function(){
    socket.send({key: socket.transport.sessionid});
  });
  socket.on('message', function(data){
    alert(data);
  });
  socket.on('disconnect', function(){
    
  });
</script>

//server
var socket = io.listen(app);
socket.on('connection', function(client) {
    client.on('message', function(message) {
        if(message.key) {
          socket.clients[message.key].send('Hello world');
        }
      });
  });
</code></pre>
