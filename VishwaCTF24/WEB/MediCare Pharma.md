# Challenge 3: MediCare Pharma
Question: Greetings form MediCare Pharma!!!!
We have started a very new pharmacy where we have various surgical equipments (more to be added soon).
But recently some hackers took control of our server and changed a hell lot of things (probably wiped 
out everything). Luckily we have few of the accounts and we need more consumers on board. For security 
reasons, we have disabled SignUp, only authorised persons are allowed to login.Have a look at our 
pharmacy and hope we grow again soon.

![admin](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/70f9bdf9-615e-433b-be88-49700ab57aca)

I attempted to inject some humor into the login page by using 'admin' for both username and password, but it seems 
this page has a stronger immunity to SQL injections than americans to Covid-vaccines!

![sqlinjection](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/d94b809b-c3e0-4a16-85d1-a17038e3e8b8)


As a result we got the sql query, 
 ![sql query](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/f21519db-ce66-4aff-a7d4-fc304acb3ca2)

Seeing that, I took username=tst&password=tst' or 'a'='a'#, This can leak accounts, and you can login.

![user](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/0d868ce4-aea2-450c-b18a-fa6744389a85)

From these user names,
`
Username : medicare ,Password : 5trongp455!
`
`
Username : janice ,Password : 5trongp455@
`
`
Username : rootuser ,Password : 5trongp455%
`
`
Username : pharmaowner ,Password : 5trongp455$
`

![user](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/ed2f63e3-9c5b-4b44-baf7-8c735ee9fe42)


If we try to login using the first one we go to the medicare site where we can order medical equipments.

So curious ,I tried buying all items to see what happens, and clicked on ```BUY ALL```,then I was greeted 
by a notification saying 

![alert](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/87dd682d-adce-4e6d-8341-54a8c710921c)

and source code got downloaded.

![source code](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/6c3368de-2cca-4faa-8768-86d2c9ec714e)

 Below is the source code,
![sourcecode2](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/5ec96f83-7c3f-4e4a-b5de-cf7e4e413a87)

Source Code:

```
<?php
header('Content-Type: application/json');

if ($_SERVER["REQUEST_METHOD"] == "POST") 
{
    $enteredInput = $_POST['search_param'];
    
    if (strlen($enteredInput) == 0)
    {
        echo json_encode(['result' => "Search bar cannot be empty"]);
    }

    else
    {
        $result = shell_exec($enteredInput);

        if ($result == null)
        {
            echo json_encode(['result' => ($enteredInput . " not found in store")]);
        }

        else
        {
            echo json_encode(['result' => $result]);
        }
    }

} 

else 
{
    http_response_code(404);
    echo json_encode(['error' => 'Access Forbidden']);
}
?>
```

After seeing the souce code,it appears that this code allows for command execution from the search bar. The key line is:

`$result = shell_exec($enteredInput);
`
This line takes the input from the search bar ($_POST['search_param']), and directly executes it using shell_exec, without 
any validation or sanitization. This means that any command entered into the search bar will be executed on the server.
. So, I tried cat ~/flag.txt and voila, we got the flag.

![flag](https://github.com/PSrujanReddy/OnlineCTF-Writeups/assets/118731259/27c2de5a-2e27-41c7-b119-fbfae852edc1)


Flag:`VishwaCTF{d1g1t4l_p41n_di5p4tch3d_th4nk5_f0r_sh0pp1ng_with_M3diC4re_Ph4rm4}`






