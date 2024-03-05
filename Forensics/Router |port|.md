#Challenge 1; Router |port|
Question: There's some unusual traffic on the daytime port, but it isn't related to date or time requests. Analyze the packet capture to retrieve the flag.

We are given a pcap file that has several packets with different protocols. The description mentioned something about daytime port, so I checked online on what port is it to filter my search. Doing some Googling, the port for daytime protocol is `Port 13 (tcp/udp)`. Looking at the packets, there seems to be encoded text that holds valuable information. This is pretty guessy but I tried Vigenère decode with this [site](https://www.guballa.de/vigenere-solver) and it shows that it was decoded using keyword `nnn`.

![image](https://github.com/warlocksmurf/onlinectf-writeups/assets/121353711/67c09a9a-6f6f-4c64-9ad6-499abc3937be)

The decoded text:
```
Hey, mate!
Yo, long time no see! You sure this mode of communication is still safe?
Yeah, unless someone else is capturing network packets on the same network we're using. Anyhow, our text is encrypted, and it would be difficult to interpret. So let's hope no one else is capturing. What's so confidential that you're about to share? It's about cracking the password of a person with the username 'Anonymous.'
Oh wait! Don't you know I'm not so good at password cracking?
Yeah, I know, but it's not about cracking. It's about the analysis of packets. I've completed most of the job, even figured out a way to get the session key to decrypt and decompress the packets. Holy cow! How in the world did you manage to get this key from his device? Firstly, I hacked the router of our institute and closely monitored the traffic, waiting for 'Anonymous' to download some software that requires admin privilege to install. Once he started the download, I, with complete control of the router, replaced the incoming packets with the ones I created containing malicious scripts, and thus gained a backdoor access to his device. The further job was a piece of cake.
Whoa! It's so surprising to see how much you know about networking or hacking, to be specific.
Yeah, I did a lot of research on that. Now, should we focus on the purpose of this meet? Yes, of course. So, what should I do for you?
Have you started the packet capture as I told you earlier?
Yes, I did. Great! I will be sending his SSL key, so find the password of 'Anonymous.' Yes, I would, but I need some details like where to start. The only details I have are he uses the same password for every website, and he just went on to register for a CTF event.
Okay, I will search for it. Wait a second, I won't be sending the SSL key on this Daytime Protocol port; we need to keep this untraceable. I will be sending it through FTP. Since the file is too large, I will be sending it in two parts. Please remember to merge them before using it. Additionally, some changes may be made to it during transfer due to the method I'm using. Ensure that you handle these issues.
Okay! ...
```

Reading the decoded text, it seems that the flag is the password of the user `Anonymous` and the hacker managed to steal a SSL key to encrypt packets. It also mentions that the SSL key is sent to another hacker via FTP. So I filtered the pcap to find ftp-data and found 2 packets, so the key is probably broken up into 2 parts.

![image](https://github.com/warlocksmurf/onlinectf-writeups/assets/121353711/f684a1a6-e4f0-4a77-95b4-6ca3c1b6c351)

Again, I randomly guessed Vigenère with the same site and succesfully extracted both PSK log files and placed them into Wireshark. This can be done by navigating to `Preferences > Protocols > TLS > (Pre)-Master-Secret log files` and add in the key file.

![image](https://github.com/warlocksmurf/onlinectf-writeups/assets/121353711/6f597263-e4e2-4582-8645-e25d13baa080)

![image](https://github.com/warlocksmurf/onlinectf-writeups/assets/121353711/2720f354-161c-4a82-8c7f-98320c98e845)

After decoding it, several HTTP2 and HTTP3 packets can be found. Filtering down for passwords, I managed to find it which is basically the flag.

![image](https://github.com/warlocksmurf/onlinectf-writeups/assets/121353711/e9703380-4f54-4208-8bf4-cd1dfeadcc34)

![image](https://github.com/warlocksmurf/onlinectf-writeups/assets/121353711/0f686fef-22d2-4769-94b4-cebe8f9a43a4)

## Task 4: Wired Secrets
Question: You are an intern at the Cyber Security Department of India and you have been assigned your first case. The Department has finally caught a notorious Hacker who communicates online in a Secretive manner. It is suspected that this file might contain clues to unlock critical information. Your task is to analyse the file and decipher any hidden messages or patterns to progress further in the investigation, PS: Zero is Hero, and dont forget to treat brackets neatly. Note: Flag has upper case letter and numbers only

Flag: `VishwaCTF{KUD0SD3T3CTIVE}`

This question gave us a pcap file that seems to record USB data. I've done this in another CTF but it was for USB keyboard data only. Unfortunately, I could not finish this challenge before the CTF ended, so I attempted it again with help from @red on Discord. He mentioned that the reason my tool did not work is because the question gave us USB mouse data, not keyboard. After parsing HID data from the USB packets to a csv file, I can proceed to analyze them.

![image](https://github.com/warlocksmurf/onlinectf-writeups/assets/121353711/20686e3e-70c7-4a27-8d6a-837da801de04)

```
cat hiddata.csv | cut -d "," -f 7 | cut -d "\"" -f 2 | grep -vE "HID Data" > hexoutput.txt

000b0000
00080300
00030100
00050000
00060200
00060100
00030000
00060200
00030100
00080300
00050300
00090600
000b0800
000c0900
000d0900
...
```

@red mentioned a [writeup](https://github.com/sourcekris/ctf-solutions/blob/master/forensics/google16-for2/README.md) that talks about extracting USB mouse data. With their script, the flag can be obtained.

```
```
Flag: `VishwaCTF{K3Y5_CAN_0P3N_10CK5}`
