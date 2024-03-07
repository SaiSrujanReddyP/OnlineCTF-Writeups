# Challenge 5: Cyber Pursuit Manhunt
Question:In response to alarming reports,our cybersecurity team is actively pursuing
a hacker known by the alias "h3ck3r_h3_bh41", who poses a serious threat by extorting
innocent individuals for monetary gain. Your mission is to track down this hacker and
provide us with the crucial information needed to apprehend them.

Retrieve the Hacker's complete full name (first name, middle name, last name), 
formatted in lowercase and replacing spaces with underscores, along with the 
associated website domain.

FLAG FORMAT: ```VishwaCTF{full_name_domain.in}```

We are given a handle of the hacker, so I used it on Twitter/X and it gives the hacker's account. 

![image](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/421f695e-b708-4db3-b20e-eb02af436526)

I got stuck here and asked the admins is if I should Twitter Binder, this is a powerful tool 
used to give a detailed Twitter posts, impressions and hashtag Analytics.

To those who are interested can check it out in the link below,
[Link](https://www.tweetbinder.com/)

But got to know that it was far more simple.The solution was actually very straightforward,
looking at the user's posts, the one that stands out the most was the first post.

```Who is Cookie the baby chick ? Very Cute indeed :)```

Upon searching for Cookie ,the baby chick. I stumbled across a instagram account called ```cookiethebabychick```.


Looking around his posts and followers, his dad's full name can be found which is ```simon_j_peter```,who is the only follower.
Additionally, his first post mentions his dad's Youtube channel.

![image](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/10fd3e86-9451-40f3-8afc-afd4a3638f1d)

[link](bit.ly/3v79BgB) 

![image](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/858927d4-0130-435a-9f90-f4cebc248592)

Analyzing his Youtube, the username can be obtained but it seems that I am in another loophole. 
I remembered Cookie mentioning his dad being a workaholic, so his dad could be on LinkedIn.

Using the username ```huskywoofwoof``` on LinkedIn, he can be found after going through several users and it shows his middle name being
```John.```

[linkedin Profile](https://www.linkedin.com/in/husky-woof-woof-3800342b8/)

![image](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/0b1c268a-a048-48b6-a0ca-6805c125c0b0)

Activity:

![image](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/34aea4c2-34f0-4833-ac05-4e79d42a0a6f)


Looking at his second post, another link could be obtained that leads to an [image](https://i.postimg.cc/dVqYpMLy/stock.jpg). Having no clue on what to do with the image, I analyzed its metadata using exiftool and found coordinates for Maharashtra, India.

![image](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/da309b32-e897-41f7-9722-84ab62672d64)


- └─$ exiftool stock.jpg 

- ExifTool Version Number         : 12.76

- File Name                       : stock.jpg

- Directory                       : .

- File Size                       : 417 kB

- File Modification Date/Time     : 2024:03:03 09:08:04-05:00

- File Access Date/Time           : 2024:03:03 09:08:11-05:00

- File Inode Change Date/Time     : 2024:03:03 09:08:04-05:00

- File Permissions                : -rwxrwxrwx

- File Type                       : JPEG

- File Type Extension             : jpg

- MIME Type                       : image/jpeg

- Exif Byte Order                 : Big-endian (Motorola, MM)

- Light Source                    : Unknown

- Orientation                     : Unknown (0)

- GPS Latitude Ref                : North

- GPS Longitude Ref               : East

- Image Width                     : 1500

- Image Height                    : 1101

- Encoding Process                : Baseline DCT, Huffman coding

- Bits Per Sample                 : 8

- Color Components                : 3

- Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)

- Image Size                      : 1500x1101

- Megapixels                      : 1.7

- GPS Latitude                    : 19 deg 57' 41.54" N

- GPS Longitude                   : 79 deg 17' 46.13" E

- GPS Position                    : 19 deg 57' 41.54" N, 79 deg 17' 46.13" E


![image](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/f6ad7a73-1e98-4517-8501-81c552890116)


Remembering there were Tigers in the picture, I linked the location and tigers to find out about a national park called Tadoba Andhari Tiger Reserve. So the national park's [website](https://www.tadobanationalpark.in/) must be the domain.

Flag: ```VishwaCTF{simon_john_peter_tadobanationalpark.in}```
