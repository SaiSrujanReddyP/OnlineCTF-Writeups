
### ==**Hack Havoc CTF 24**==

**Username : Ir0nw0lf3000** 

#Osint:
---
# CyberMaterial’s CyberSleuth Newsletter


- I went ahead and searched for Netflix leaks related articles in Cyber Material's LinkedIn Newsletter, Cyber Briefing.

- I found this [Cyber Briefing article ](https://www.linkedin.com/pulse/cyber-briefing-20240809-cybermaterial-oqrnf/?trackingId=r7DR%2FABfTL%2BMuwWJb3xCMg%3D%3D)dating back to 2024.08.09. 
- ![[Pasted image 20240909170437.png]]

- Flag: 
```
CM{4rCan3_4nD_h34rTst0pP3r}
```

---
## Meet me here !
---

- As we can see in the image given we see WAFFLE INN.

- And if we see where the CEO of CyberMaterial, Tyrone E Wilson is from we know he is from Arlington, Virginia, USA.

- So using some google dorking we can find the location.
- ![[Pasted image 20240909171424.png]]
- As we can see the place we see in MapQuest matches with our image and also it is in the flag format ==CM{6_4_2}==.

- Flag:
```
CM{Laurel_Hill_Rd}
```

---
## APT Intel Hunt
---

- When we search CyberMaterial's website, we come across Andariel Blog Post.
- ![[Pasted image 20240909173031.png]]
- In the post we can see links, URL preview of Andariel Threat Group redirects us to a Pastebin link.
![[Pasted image 20240909191933.png]]


- The [PasteBinLink](https://pastebin.com/QUwg950y) gives a paste saved by HACKERLAZARUS which had numbers in between converting them from hex to text gives the flag.
![[Pasted image 20240909192013.png]]

- Text:
```
43 4d 7b 34 70 54 5f 47 72 30 75 50 35 5f 4c 34 7a 34 52 75 35 7d
```

- Flag:
```
CM{4pT_Gr0uP5_L4z4Ru5}
```

---
## Catch me !!!
---


- I did google reverse image search and I got relevant locations in Las Vegas. And from the image name .

![[Pasted image 20240909212644.png]]

- I did some dorking and found out it was The Mob Museum in Las Vegas. The location matched the image.
![[Pasted image 20240909212850.png]]
- Flag:
```
CM{the_mob_museum}
```
---
## Oops! Where Did I Hide the Flag?
---

- After soul exhausting search for videos on CyberMaterial's Youtube Channel I found the video based on the clue they gave in the question "latest cybersecurity alerts, incidents, and news".

- I found the video at [Cyber Briefing 2024.08.30](https://www.youtube.com/@cybermaterial)


![[Pasted image 20240909193136.png]]
---
#crypto:
---
## Green Flags 🟢:
---


- ![[Flags_every_where (1).png]]
- Searching the image in google you can find out that they are maritime flags and each of them has a letter assigned to them.

- Flag:
```
CM{nato_signals}
```

---
## I can't see it
---
- ⠉⠍⠸⠣⠹⠼⠁⠼⠑_⠃⠗⠼⠙⠼⠁⠇⠇⠼⠉_⠼⠁⠎_⠼⠙⠼⠉⠁⠇⠸⠜

- The above is braille 

- Flag:
```
CM{TH15_BR41LL3_1S_43AL}
```

---
## Digital Black Hole
---
- .PNG was suspicious i tried making it .txt and i got something in binary
- converting it to text again got some something of same sort.
- Again i converted i got something same but with spaces i removed it and converted again this time i got some encoded text

- Putting the image given in [Aperi'solve](https://www.aperisolve.com/) we can see the following:

In Strings we can see:
![[Pasted image 20240909201859.png]]

After running the script:
```
def binary_to_text(binary_list):
    return ''.join([chr(int(b, 2)) for b in binary_list])
with open("1.txt", "r") as file:
    content = file.read().strip()
binary_values = content.split()
binary_values = list(filter(None, binary_values))
decoded_text = binary_to_text(binary_values)
print("Decoded Text:", decoded_text)
```

- We get 8SNZ9Rn1LCYmWnr5DVLcyhZ if we put this in dcode.fr, we get to know that it is base 62 encoded.
![[Pasted image 20240909211526.png]]
![[Pasted image 20240909211624.png]]
- Flag:
```
CM{N0t_64_Alway5}
```

---
## Dear Trithemius,
---

- The encrypted GO Code they gave you

```
 def to_my_honey(owo):
    return ord(owo) - 0x41
def from_your_lover(uwu):
    return chr(uwu % 26 + 0x41)
def encrypt(billet_doux):
    letter = ''
    for heart in range(len(billet_doux)):
        letters = billet_doux[heart]
        if not letters.isalpha():
            owo = letters
        else:
            uwu = to_my_honey(letters)
            owo = from_your_lover(uwu + heart)
        letter += owo
    return letter
m = "imissyou"
c = encrypt(m)
print(c)
```

- The decrypted Go code is 

```
def decrypt(encrypted_text):
    decrypted_text = ''
    for heart in range(len(encrypted_text)):
        letters = encrypted_text[heart]
        if not letters.isalpha():
            owo = letters
        else:
            uwu = to_my_honey(letters)
            owo = from_your_lover(uwu - heart)
        decrypted_text += owo
    return decrypted_text
def to_my_honey(owo):
    return ord(owo) - 0x41
def from_your_lover(uwu):
    return chr(uwu % 26 + 0x41)
def encrypt(billet_doux):
    letter = ''
    for heart in range(len(billet_doux)):
        letters = billet_doux[heart]
        if not letters.isalpha():
            owo = letters
        else:
            uwu = to_my_honey(letters)
            owo = from_your_lover(uwu + heart)
        letter += owo
    return letter
m = "LPXH_Z_AZRDSQZWJI" 
c = encrypt(m)  
print("Encrypted:", c)

d = decrypt(c)
print("Decrypted:", d)
```

- From the the file we get the encrypted text as LPXH_Z_AZRDSQZWJI.

- Flag:
```
CM{LOVE_U_TRITHEMIUS}
```

---
## My Secret X 'V' My Secret Y
---
- Hide Text: 6866507f43181e1874531b79741f59187448791f517256
- If we XOR 6 and C of the flag format CM we get "+", repeating the same for other digits we get to know that they all were xor'd with "+".

- So, xor'ing  the 6866507f43181e1874531b79741f59187448791f517256 with + will give us the flag.

- 
```
def decrypt_xor_with_plus(hex_string):
    hex_pairs = [hex_string[i:i+2] for i in range(0, len(hex_string), 2)]
    xor_key = ord('+')
    decrypted_message = ""
    for hex_pair in hex_pairs:
        int_value = int(hex_pair, 16)
        original_value = int_value ^ xor_key
        decrypted_message += chr(original_value)
    return decrypted_message
ciphertext = "6866507f43181e1874531b79741f59187448791f517256"
decrypted_message = decrypt_xor_with_plus(ciphertext)
print("Decrypted Message:", decrypted_message)
```

-  Flag:
```
CM{Th353_x0R_4r3_cR4zY}
```
---
#Rev:
---
## Rev is easy!
---
- I got the flag by just doing strings Lol!!

![[Pasted image 20240909215406.png]]

- Flag:

```
CM{ReV_i5_Easy}
```
---
## Go Crazy!!
---
- This one was super easy I just used [Dogbolt](https://dogbolt.org/) to decompile and i got it.
 ![[Pasted image 20240909215734.png]]

- Flag:

```
CM{5O_MuCh_7un}
```
---
## Who’s Really Dunked?
---
- This is a crypto challenge given in rev tbh.
- First I used [dcode.fr](https://www.dcode.fr/) and I found out that it's base 92 encoding.
![[Pasted image 20240909220322.png]]
- This is the decoded base 92 text is given as:
```
- 4D$j(!T_9|V6…^TJ

4@?DE 4CJAE@ l C6BF:C6WV4CJAE@VXj  
4@?DE C625=:?6 l C6BF:C6WVC625=:?6VXj  
  
^^ rC62E6 2? :?E6C7246 E@ C625 :?AFE 7C@> E96 FD6C  
4@?DE C= l C625=:?6]4C62E6x?E6C7246WL  
   :?AFEi AC@46DD]DE5:?[  
   @FEAFEi AC@46DD]DE5@FE  
NXj  
  
^^ x?:E:2= 7=28 AC67:I  
=6E 7=28!C67:I l Qr|LQj  
  
^^ uF?4E:@? E@ 4964< FD6C :?AFED 2?5 G2=:52E6 E96 7=28  
7F?4E:@? 4964<WX L  
   C=]BF6DE:@?WVt?E6C 7:CDE G2=F6i V[ WG2=F6~?6X lm L  
       C=]BF6DE:@?WVt?E6C D64@?5 G2=F6i V[ WG2=F6%H@X lm L  
           C=]BF6DE:@?WVt?E6C E9:C5 G2=F6i V[ WG2=F6%9C66X lm L  
               C=]4=@D6WXj  
  
               ^^ x?:E:2=:K6 7=28 H:E9 E96 AC67:I  
               =6E 7=28 l 7=28!C67:Ij  
  
               ^^ pAA6?5 A2CED E@ E96 7=28 32D65 @? :?AFE G2=F6D  
               :7 WG2=F6~?6 lll Q}6HDQX L  
                   7=28 Zl Q}6HD0Qj  
               N  
  
               :7 WG2=F6%H@ lll Qp=6CEDQX L  
                   7=28 Zl Qp=6CED0Qj  
               N  
  
               :7 WG2=F6%9C66 lll Qx?4:56?EQX L  
                   7=28 Zl Qx?4:56?EQj  
               N  
  
               7=28 Zl QNQj  
  
               ^^ r964< :7 E96 4@>AFE65 92D9 >2E496D E96 6IA64E65 92D9  
               4@?DE 6IA64E65w2D9 l Qg_d5eddf_dbhfeb57a_52e23f5dheefe33b52c`2_e526fefdf`g7e4a3fdd2ag5Q  
               :7 W92D9W7=28X lll 6IA64E65w2D9X L  
                   4@?D@=6]=@8WQr@?8C2EF=2E:@?DP %96 7=28 :Di Q Z 7=28Xj  
               N 6=D6 L  
                   4@?D@=6]=@8WQx?4@CC64E 7=28] %CJ 282:?]QXj  
               N  
           NXj  
       NXj  
   NXj  
N  
  
^^ uF?4E:@? E@ 4@>AFE6 $wp\ade 92D9  
7F?4E:@? 92D9W:?AFEX L  
   C6EFC? 4CJAE@]4C62E6w2D9WVD92adeVX]FA52E6W:?AFEX]5:86DEWV96IVXj  
N  
  
^^ $E2CE E96 492==6?86  
4964<WXj
```

- Putting the above thing in cipher identifier again, I got ROT-47.

![[Pasted image 20240909220559.png]]
- The decoded result is :
```
	const crypto = require('crypto');  
const readline = require('readline');  
  
// Create an interface to read input from the user  
const rl = readline.createInterface({  
  input: process.stdin,  
  output: process.stdout  
});  
  
// Initial flag prefix  
let flagPrefix = "CM{";  
  
// Function to check user inputs and validate the flag  
function check() {  
  rl.question('Enter first value: ', (valueOne) => {  
      rl.question('Enter second value: ', (valueTwo) => {  
          rl.question('Enter third value: ', (valueThree) => {  
              rl.close();  
  
              // Initialize flag with the prefix  
              let flag = flagPrefix;  
  
              // Append parts to the flag based on input values  
              if (valueOne === "News") {  
                  flag += "News_";  
              }  
  
              if (valueTwo === "Alerts") {  
                  flag += "Alerts_";  
              }  
  
              if (valueThree === "Incident") {  
                  flag += "Incident";  
              }  
  
              flag += "}";  
  
              // Check if the computed hash matches the expected hash  
              const expectedHash = "805d65570539763df20da6ab7d596676bb3da41a06dae7675718f6c2b755a28d"  
              if (hash(flag) === expectedHash) {  
                  console.log("Congratulations! The flag is: " + flag);  
              } else {  
                  console.log("Incorrect flag. Try again.");  
              }  
          });  
      });  
  });  
}  
  
// Function to compute SHA-256 hash  
function hash(input) {  
  return crypto.createHash('sha256').update(input).digest('hex');  
}  
  
// Start the challenge  
check();
```

- From this we know that the flag is 

```
CM{News_Alerts_Incident}
```

---
## The Key to Nowhere
---
- After trying so much and breaking my head for this challenge something worked. I used pyinstxtractor and it extracted files after that I used pycdc to get this code.

```
# Source Generated with Decompile++
# File: 3.pyc (Python 3.10)

def xor_encrypt(data, key):
    '''Encrypt or decrypt data using XOR with the given key.'''
    return None((lambda .0 = None: for i, c in .0:
    chr(ord(c) ^ ord(key[i % len(key)])))(enumerate(data)))

def get_hidden_key():
    '''Retrieve the hidden key.'''
    return ''.join((lambda .0: for c in .0:
    chr(c))((83, 84, 65, 84, 73, 67, 75, 69, 72)))

def get_hidden_flag():
    '''Retrieve the hidden flag.'''
    return ''.join((lambda .0: for c in .0:
    chr(c))((82, 51, 86, 95, 68, 52, 84, 52, 95, 72, 51, 114, 79)))

def main():
    key = get_hidden_key()
    flag = get_hidden_flag()
    encrypted_flag = xor_encrypt(flag, key)
    print('Welcome to CyberMaterial, where only the brave dare to crack the code!')
    response = input('Do you think you can outsmart the system? (yes/no): ').strip().lower()

    if response == 'yes':
        user_input = input('Alright, savvy one! Enter the secret key: ')
        if user_input == key:
            decrypted_flag = xor_encrypt(encrypted_flag, key)
            print(f'''Congratulations! Here's your flag: CM{{{{decrypted_flag}}}}''')
        else:
            print('Oops! Incorrect key. Try again.')
            return None
    else:
        print('I see you’re a true codebreaker! No key needed. The flag is hidden, but you’re smart enough to find it. Good luck!')

if __name__ == '__main__':
    main()
return none
```

- After this using ChatGPT we will get the correct code and we will get the flag:

```
CM{R3V_D4T4_H3rO}
```

---
## Awwwwwwwwwwwwwww!!
---
- This challenge is the same challenge as in [VSCTF Writeup](https://hackmd.io/@Raviyelna/r1bWNHiHA)

- Flag:
```
CM{awawawawaawa_0oooosHii11i_J3lly!}
```
---
#web:
---
## We're rolling
---
- I solved a similar challenge before ,there are contents below, which can be realized after seeing the scrollbar in robots.txt.
- Flag:
```
 CM{RoOL_&_ROoL}
```
---
## Drunken website
---
- We are given with [Challenge Link](http://challenge.ctf.cybermaterial.com/dissssissssimpul/) .
- If we go to source code we can find [THIS](http://challenge.ctf.cybermaterial.com/dissssissssimpul/homepage.html#).
- In that source code we get 

   [Final Link OOF!!](http://challenge.ctf.cybermaterial.com/dissssissssimpul/0.html)
   
- Flag:

```
CM{W3bs1t3_15_5hi7}
```
---
## A Shakespearian Tragedy
---
- Using gobuster, found these sites:


![[Pasted image 20240910133543.png]]

- I found this in /users, 
![[Pasted image 20240910133338.png]]

- Keep the text in cipher Identifier we get to know it is Base 58 Encoding.

![[Pasted image 20240910133851.png]]

- Decoding that we get the flag scrambled as C3Mr{3id_}c4me_i_s4w_i_c0nqu.

![[Pasted image 20240910133916.png]]

- Flag:
```
CM{i_c4me_i_s4w_i_c0nqu3rd}
```
---
## Bidden Funhouse
---
- We can observe one thing whenever a name is given "/b/" is being removed. There is a URL switch.

  - Example: 
```
  http://challenge.ctf.cybermaterial.com/?name=hello.
```
  
- When it is supposed to be 
```
http://challenge.ctf.cybermaterial.com/b/?name=hello.
```
  
  which welcomes you with a "==こんにちは hello==".
![[Pasted image 20240909233805.png]]

- If we try SSTI Payload here on
```
http://challenge.ctf.cybermaterial.com/b/?name={{7*7}}
```
   
   we can observe that we get "==こんにちは 49==" which makes it clear that its being evaluated. This means this a Jinja Injection.
   ![[Pasted image 20240909233845.png]]

- So we use {{ config }} payload - In these object you can find all the configured env variables.

![[Pasted image 20240909233605.png]]

- Flag:
```
CM{Y0u_4r3_a_r3A1Ly_go0D_nINj4}
```
---
## The Shell Shocker
---
- If we open burpsuite and see the request that is made we can see that
-![[Pasted image 20240909234657.png]]

- script.js: If we go to **/a/static/script**.js we can see the js file:

```
const commandForm = document.querySelector('#command-form');
const commandInput = document.querySelector('#command-input');
const outputDiv = document.querySelector('#output');

commandForm.addEventListener('submit', async (event) => {
  event.preventDefault();
  
  const command = commandInput.value;
  
  const validCommand = /^((uname|echo|pwd|whoami)\s*([-\w\s]*))?$/i.test(command);
  
  if (!validCommand) {
    outputDiv.textContent = 'Error: Invalid command. Please enter a valid command (uname, echo, pwd, or whoami) with optional arguments and options separated by spaces and hyphens.';
    return;
  }
  
  try {
    const response = await fetch('/exec', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({ command }) 
    });
    const result = await response.text();
    outputDiv.textContent = result;
  } catch (error) {
    console.error(error);
    outputDiv.textContent = `Error: ${error.message}`;
  }
});
```

- From the file we understand that we can only run "uname|echo|pwd|whoami".
- So we go back to where we were before, as we on intercept and forward all the requests, we come across
```
GET /a/%7B%7B%20url_for('static',%20filename='script.js')%20%7D%7D HTTP/1.1
```

```
GET /a/%7B%7B%20url_for('static',%20filename='style.css')%20%7D%7D HTTP/1.1
```
- We need to change them to the below as they are sending request to wrong endpoint.

```
GET /a/static/script.js HTTP/1.1
```

```
GET /a/static/styles.css HTTP/1.1
```


-  After pushing those requests we need to go to the website and type "PWD" or any accceptable command. From that we can see a POST request but it is odd.

![[Pasted image 20240910001520.png]]

- The request is supposed to go to
```
POST /a/exec HTTP/1.1
```

- We change that and also now we need to change the "pwd" to "cat flag.txt" to get the flag.

- And we get the flag.

![[Pasted image 20240910000923.png]]

- Flag:
```
CM{c0mMAnd_INjEc7iON_f7w}
```
---
#Welcome:
---
## Welcome To CyberMaterial
---
- We can get the flag in discord CTF-Support channel
- Flag:

```
CM{Subscribe_TO_CyberMaterial}
```
---
## FeedBack challenge
---
>Submit the feedback and get the flag.
```
CM{HApPy_EnDiNg}
```



