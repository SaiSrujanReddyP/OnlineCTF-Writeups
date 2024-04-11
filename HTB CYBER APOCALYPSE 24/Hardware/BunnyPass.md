## Task 2: BunnyPass
Question: As you discovered in the PDF, the production factory of the game is revealed. This factory manufactures all the hardware devices and custom silicon chips (of common components) that The Fray uses to create sensors, drones, and various other items for the games. Upon arriving at the factory, you scan the networks and come across a RabbitMQ instance. It appears that default credentials will work.

Flag: `HTB{th3_hunt3d_b3c0m3s_th3_hunt3r}`

We are given a `RabbitMQ` instance to investigate. On the login page, we use the default credentials of `admin` username and `admin` password. Inside the website portal, the flag is probably hidden somewhere. 

![image](https://github.com/warlocksmurf/onlinectf-writeups/assets/121353711/6241c200-afc4-43f7-8e4f-597d3a677d1c)

![image](https://github.com/warlocksmurf/onlinectf-writeups/assets/121353711/b1ad4d54-651d-4558-815b-ec445f68e445)

After 2 hours, I came across the `Queues` page where it seems that there are several messages in certain queues. Analyzing the `factory_idle` queue, I noticed the `Get Message` function.
