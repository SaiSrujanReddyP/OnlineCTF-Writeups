# Challenge 2: Smoke Out The Rat
Question:There was a major heist at the local bank. Initial findings suggest that an intruder from within the bank,
specifically someone from the bank's database maintenance team, aided in the robbery. This traitor granted access to
an outsider, who orchestrated the generation of fake transactions and the depletion of our valuable customers' 
accounts. We have the phone number, '789-012-3456', from which the login was detected, which manipulated the bank's 
employee data. Additionally, it's noteworthy that this intruder attempted to add gibberish to the binlog and ultimately
dropped the entire database at the end of the heist.
Your task is to identify the first name of the traitor, the last name of the outsider, and the time at which the outsider 
was added to the database.

Flag format : VishwaCTF{TraitorFirstName_OutsiderLastName_HH:MM:SS}


After searching through google, I found a command that is used to extract and decode the contents of a MySQL binary log file 
into a human-readable text format and save it to a file named output.txt.

Code:
`mysqlbinlog --base64-output=DECODE-ROWS --verbose DBlog-bin.000007 > output.txt`

![WhatsApp Image 2024-03-06 at 12 53 12 AM](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/1ea0b24e-dcf3-4522-8472-99151abaa10d)

from this we can get a a.txt file that is human readable.

After we get the a.txt and put it in VS code and search of the number the culprit uses  `789-012-3456` using CTRL+F we find a man named `Matthew Miller`
who is the inside traitor, cause he is the Database Administrator who gave access to the outside attacker.

![image](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/923af411-8edc-404b-b2dc-1ef7535e26b1)

Now if we go to the end of the file we will find a man named `John Darwin` cause he is the last person who logged in before the server crash making him the 
outsider. Also the time of his entry is 15:31:29.

![image](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/5f8500ae-d1e9-4cc8-9865-da552ea20d1f)

Flag:`VishwaCTF{Matthew_Darwin_15:31:29}`

