# Challenge 2: BIBBA Part 3 

Question: There's no osint without geoguesser... this one is pretty simple, find out the location co-ordinates of the AREA where the battle took place. I wish googlemaps could've worked that time :(((

![image](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/be92cd23-883e-499a-8064-57a9ef5f5575)

Note: you only need to be precise upto 2 decimals, i.e: 99.32 N, 29.06 E This has been done because there's no exact location where battles are fought so just a generic nearby approx location would do. Flag Format: 0CTF{XX.XX,YY.YY}

FLAG FORMAT: ```0CTF{XX.XX,YY.YY}```

Reverse search the image we got in BIBBA [PART-2], in Google 

![ggg](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/b56fced0-e4dd-4a10-8de1-b23cd908306d)

I opened the first article,
[Article Link](https://www.bssnews.net/news/99954)

The image matches ours,
![image](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/46a9f61f-c326-446a-a5b2-5a30ef8225ce)

We get a map of where the event happened on the website,
![image](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/9f2c8399-18a1-4218-93d1-05101a4afbb2)


if we search for the location in google maps, we get the location of the place as somewhere in 23.23 N and 89.04 S,

Flag: ```0CTF{23.23, 89.04}```
