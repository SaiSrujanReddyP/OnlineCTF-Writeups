# Challenge 2: ifconfig_inet
Question:In the labyrinth of binary shadows, Elliot finds himself standing at the crossroads of justice and chaos.
Mr. Robot, the enigmatic leader of the clandestine hacktivist group, has just unleashed a digital storm upon Evil 
Corp's fortress. The chaos is palpable, but this is just the beginning.As the digital tempest rages, Elliot receives 
a cryptic message from Mr. Robot. "To bring down Evil Corp, we must cast the shadows of guilt upon Terry Colby," the 
message echoes in the encrypted channels. However, in the haze of hacktivism, Elliot loses the crucial IP address 
and the elusive name of the DAT file, leaving him in a digital conundrum.

To navigate this cybernetic maze, Elliot must embark on a quest through the binary underbelly of Evil Corp's servers.
The servers, guarded by firewalls and encrypted gatekeepers, conceal the secrets needed to ensure Terry Colby's fall.

Guide Elliot to the his destiny.

Flag Format : VishwaCTF{name of DAT file with extension_IP address of Terry Colby}

E.g : ``` VishwaCTF{file.dat_0.0.0.0} ```

So if we search for mr robot dat file and colby's IP address, we can find a reddit post on the same.
[link](https://www.reddit.com/r/MrRobot/comments/km2xo0/ip_address_goof_up/)

From the post if we go down we can see a user named Kaptnik gives us the 
name of the dat file: ``` fsociety00.dat ```
IP Address: ``` 218.108.149.373 ```

![image](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/f8a68c74-95c3-4076-ba2e-b7f010484260)

Flag: ``` VishwaCTF{fsociety00.dat_218.108.149.373} ```

