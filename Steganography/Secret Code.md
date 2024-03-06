# Challenge 3: Secret Code
Question: Akshay has a letter for you and need your help.


We are provided with  a black jpg file and a txt file containing a message from Akshay.

```
To,
VishwaCTF'24 Participant

I am Akshay, an ex employee at a Tech firm. Over all the years, I have been trading Cypto currencies and made a lot of money doing that. Now I want to withdraw my money, but I'll be charged a huge tax for the transaction in my country.

I got to know that you are a nice person and also your country doesn't charge any tax so I need your help. 

I want you to withdraw the money and hand over to me. But I feel some hackers are spying on my internet activity, so I am sharing this file with you. Get the password and withdraw it before the hackers have the access to my account.

Your friend,
Akshay
```

binwalk the jpg file to extract hidden data embedded within it.

```
└─$ binwalk -e confidential.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
116247        0x1C617         Zip archive data, at least v2.0 to extract, compressed size: 72486, uncompressed size: 72530, name: 5ecr3t_c0de.zip
188778        0x2E16A         Zip archive data, at least v2.0 to extract, compressed size: 170, uncompressed size: 263, name: helper.txt
189177        0x2E2F9         End of Zip archive, footer length: 22
```

The zip file contains a password-protected zip file and a txt file containing a hint.

```
Hey buddy, I'm really sorry if this takes long for you to get the password. But it's a matter of $10,000,000 so I can't risk it out.

"I really can't remember the password for zip. All I can remember is it was a 6 digit number. Hope you can figure it out easily"
```

Now, we need to crack the zip password. so I used `John the Ripper` instead. I also created a script to generated a wordlist of 6 digit numbers .

```
$ zip2john 5ecr3t_c0de.zip > secret.hash
$ john --wordlist=sixdigits.txt secret.hash
$ john --show secret.hash

5ecr3t_c0de.zip/5ecr3t_c0de.txt:945621:5ecr3t_c0de.txt:5ecr3t_c0de.zip:5ecr3t_c0de.zip
5ecr3t_c0de.zip/info.txt:945621:info.txt:5ecr3t_c0de.zip:5ecr3t_c0de.zip

2 password hashes cracked, 0 left
```

Unlock the Zip file to get two txt files. One of them was random numbers while the other had another hint.

```
What are these random numbers? Is it related to the given image? Maybe you should find it out by yourself
```

 The random numbers represent (x,y) pixels.

```
(443, 1096)
(444, 1096)
(445, 1096)
(3220, 1096)
(3221, 1096)
(38, 1097)
(39, 1097)
(43, 1097)
(80, 1097)
(81, 1097)
(83, 1097)
(93, 1097)
(95, 1097)
...
```

 I used ChatGPT to create a script that will color a white pixel on a blank jpg  file which could uncover the flag,as this challenge has image in it.
```
from PIL import Image

def read_coordinates(file_path):
    with open(file_path, 'r') as f:
        lines = f.readlines()
    coordinates = []
    for line in lines:
        x, y = line.replace('(', '').replace(')', '').split(',')
        coordinates.append((int(x), int(y)))
    return coordinates

def draw_white_pixels(image_path, coordinates, output_path):
    img = Image.open(image_path)
    for coord in coordinates:
        img.putpixel(coord, (255, 255, 255))  # RGB value for white
    img.save(output_path)

image_path = '/confidential.jpg'
file_path = '/5ecr3t_c0de.txt'
output_path = 'output_image.png'

coordinates = read_coordinates(file_path)
draw_white_pixels(image_path, coordinates, output_path)

print(f"Image with white pixels at the given coordinates has been saved as {output_path}.")
```
Run the script, we get the the flag in the output jpg file.

![output_image](https://github.com/warlocksmurf/onlinectf-writeups/assets/121353711/b9e33a42-f20f-4553-b7fc-137099bf6b1a)

Flag: `VishwaCTF{th15_15_4_5up3r_53cr3t_c0d3_u53_1t_w153ly_4nd_d0nt_5h4re_1t_w1th_4ny0ne}`
