# Challenge 1: H34D3RS
Question:Name of the challenge says something.

![lorbrowser](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/f26e1346-b196-4e2b-b3d3-7caee5732f20)

So, after seeing that it wants me to come from lorbrowser.I opened burpsuite and pasted the instance URL, went to interceptor ,
turn on intercept, made changes in the user agent of HTTP Request to lorbrowser 

Here, are the screenshots :

![Burpsuite](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/ab98ee75-f877-4b37-b80a-291f7aa5b358)

and went to actions and Selected Send to repeater,

![Step2](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/8a0fea19-2be5-4202-87fc-86d5eb37b145)

Sending it to repeater makes thing easy ,we dont have to always rewrite the entire request again and refresh to lose everything.
We can get all the responses and make changes to requests and all we need to do is simply press "send", isn't that convenient?.

![4](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/4cf9c1fa-2809-4d27-a547-15062c9a5e99)

So we can see that it is now asking for us to come from vishwactf site . So, we need to add `Referer: https://vishwactf.com/` 
to the request.

![5](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/70092e89-7d26-4d78-b887-96168f7cb27d)

So again it is saying that we have to be 20 years in the future .So we need to add `Date:2044` to the request.

![6](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/7450a5ed-1ca1-46c1-bf9f-f009b545d186)

Now as we can see it is telling us to put a client preference of 10 for authenticated and encrypted response.
For that we need to change the `Upgrade-Insecure-Requests to 10`.

![7](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/64a78fee-d1ac-4035-9bd1-60a2b9dc9b7d)

Now as we can see they are taking about a nine times (9) header field approximate bandwith of clients connection to server.
The header it is taking about is Downlink.

![Downlink](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/61475bed-7ec1-4041-b0fb-68a9a0a556f4)

So after we add `Downlink:999999999` we get the flag.

![headerflag](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/7ba579a7-8f9b-47f7-bc63-88bbd28144b2)

Flag:`VishwaCTF{s3cret_sit3_http_head3rs_r_c0o1}`


