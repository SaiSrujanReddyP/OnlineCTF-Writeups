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




