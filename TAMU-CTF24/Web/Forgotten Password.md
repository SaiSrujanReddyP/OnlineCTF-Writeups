# Forgotten Password
We discovered that this blog owner's email is `b8500763@gmail.com` through reconnaissance. We do not have access to the password of the account, how could we login regardless?

## Solution
Even though we can do the below,
The exploit is that you can force mailing API fields to cc additional emails despite only designating one recipient using commas or semicolons.
and bypass the front-end email verification by using Burp Suite where we send an HTTPS request without being verified by the actual text box, then simply add another email after the email.
Afterwards, you will receive the email with the flag.

## My solution
What I did was made an account I just put some characters in front of the email and registered a google account matching The mail we got from th challenge, like  myemail\x00b8500763@gmail.com 

I felt like doing this after seeing the below 

`authenticity_token=hSPThoNNXpExLZL1PX2dEKqtxh9hDjtItt6t-DhZfU-isiZASAigkqSHVoSVyeF4kmhFsz8Cx2fRbeQL8siZ9g&email[]=b8500763%40gmail.com&email[]=hydiqauhbsosightqj@cazlp.com&commit=Submit`

Then got the below flag to the mail,

Flag: `gigem{sptfy.com/Qhnv}`
