# Challenge 2: Recipe Archival Workshop
Question:New interns in the Recipe Archival Workshop have a simple task- 
upload images of yummy delicacies and dream about tasting them some day.

This is what the challenge looks like ,

![image](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/89d6485a-8c3e-47ee-8e5e-f93b205c57c2)

Looking at the challenge we can tell it is a file upload vulnerability.So, for this we can use Upload Scanner, a burp extension.

[Burp Extension](https://portswigger.net/bappstore/b2244cbb6953442cb3c82fa0a0d908fa)

after downloading the extension, click on right click on "upload" and select the extension "Upload Scanner", in burp suite go to upload scanner extension and enable the Create log see 'Done upload" tab.

![webrecipe](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/5060f265-9178-4fb7-bf08-116017045204)

Then go to "Done upload" tab . As we can see the flag is

![web recipe2 answer](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/7f53bf7d-7eaf-4474-b395-92be59d25386)

Flag:`VishwaCTF{today_i_wanted_to_eat_a_croissant_QUASO}`
