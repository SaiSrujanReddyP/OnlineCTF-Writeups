# We Are Valorant
Question: One day, while playing Valorant, I received a mail from Riot Games that read,
“In a world full of light, sometimes the shadows help you win.” “Your Signature move also helps you a lot ; develop one and ace it now.”
It also had an image and a video/gif attached to it. I am not able to understand what they want to say. Help me find what the message wants to express.

We are given a corrupted jpg file and a mp4 video of Astra (which seems to be a gif). 
Fixing the jpg file, it shows the agents in Valorant but there were no important information in it.

For fixing ,we need to do hex edit and change the header of the file.

![WhatsApp Image 2024-03-05 at 1 45 08 PM](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/364fb388-8d0a-477f-84dc-bb46e147af28)
As we can see the header is FF D8 , we need to change that to FF F8.

After the hex edit the image is repaired,
![WhatsApp Image 2024-03-05 at 1 45 09 PM](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/51f5c2be-6688-4548-93a2-117ef5c46b9d)

and the image we get is image of all valorant characters.

![we_are_valorant (1)](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/d7e2cc90-2ce7-4019-a6b9-1f47bfe5c508)

I went ahead to analyze the jpg file via [Aperi'Solve](https://www.aperisolve.com/) and found out the common password which is Tenz

![image](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/c31f199b-6b1d-4316-879a-d3b3f43a8ac9)

Now after Typing in the password in aperisolve , we will get a  hidden file in steghide .

![image](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/fc491055-d0a8-4cd2-bfe6-1818e1d1e55e)

Not_a_Secret.txt

![image](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/1940f11a-4578-4ab3-b5ff-98264dd2cfbe)

The content of the text file is 
```
Hello!!
hope you are enjoying the CTF
here's your flag

VishwaCTF{you_are_invited_to_the_biggest_valorant_event}
```

Flag:`VishwaCTF{you_are_invited_to_the_biggest_valorant_event}`





 
