# This was the only chall I solved on my own for this CTF since most of it was web that I'm relatively bad at, but I did help with a couple more. Overall a pretty neat challenge with a pretty neat solution
![image](https://github.com/user-attachments/assets/8b1591ec-7623-479f-a654-549e56ce5464)
![image](https://github.com/user-attachments/assets/c4354fc6-e1c9-48cc-bf76-f65506d6e833)

Reading the rules, I quickly realised that since I can know whether or not a specific character is correct in a specific position, brute force becomes surprisingly feasible as it would require at most 36 attempts at each character place (assuming all lowercase alphanumeric), which adds up to 1152 attempts total given an algorithm that can remember correct guesses for each place. Since it uses web requests, I did have to decode bytecodes to emojis but luckily python is able to handle unicode for strings, so I was able to write the script below.

```
import requests
import json

def findflag():
  input = "deadbeefdeadbeefdeadbeefdeadbeef"
  url = 'http://challenge.nahamcon.com:31942/guess'
  headers = {'Content-Type': 'application/json'}
  response = list("00000000000000000000000000000000")
  realflag = list("00000000000000000000000000000000")
  for x in range(len(realflag)):
    letter = 48
    while response[x] != "🟩":
      if letter == 58:
        letter = 97
      input = list(input)
      input[x] = chr(letter)
      input = ''.join(input)
      response = list(requests.post(url, data=json.dumps({'guess': f'flag{{{input}}}'}), headers=headers).json()["result"])
      print(input[:x+1])
      print(''.join(response))
      if response[x] == "🟩":
        realflag[x] = input[x]
      letter = letter + 1

findflag()
```
The final printed output would've been the flag, which in my case was bec42475a614b9c9ba80d0eb7ed258c5. Hence, the flag is ```flag{bec42475a614b9c9ba80d0eb7ed258c5}```.

Postscript: I probably could've solved it quicker had I used chatgpt, but what I really like about this is that it's mostly algorithmic rather than niche knowledge and I enjoyed it quite a bit as a brain exercise.
