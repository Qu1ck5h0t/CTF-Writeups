## This was one of the two problems I solved in BroncoCTF, and for once the crypto guy did something cool in a crypto chall!
![image](https://github.com/user-attachments/assets/27287223-4f12-429f-8fa9-d1b7ecdc29f2)

Downloading and opening intel.txt gives the following:
```
Psst... Luigi here. I have some intel on this mysterious yoshie user. He:

1. Really likes being called a homie. Specifically, yoshiethehomie.
2. Likes to talk in "partial leetspeak."
3. Is a fan of "one, only one!" special character replacement.
4. Appends his 4-digit PIN to all his secure logins.
5. Loves BroncoCTF so much that he includes the flag format in his credentials.

This info wasn't easy to get! But, he owes me money too, so you better catch this fool and gimme some of the dough I also deserve!
```
From the information, we get clues that can be used as parameters for brute forcing possible passwords. Following that, all we would need is hash every candidate and compare it to the given SHA256 hash. 

Firstly, the password is probably some variation of "yoshiethehomie". 

Secondly, "partial leetspeak" implies that one or more of the "1337able" characters will be present in their 1337speak equivalent. 

Thirdly, "one, only one!" special character replament implies that one of the characters will be replaced by a special character in the password. It is important to note that if every special character in every position is treated as a candidate, the brute force will likely take longer than the CTF will remain active for, and possibly the heat death of the universe. Therefore, I defined some rules based on human behaviour patterns for the special characters:
```
s -> $, a -> @, i -> !
```

Fourth(-ly?), for every candidate we will also have to append a 4 digit number to the end, multiplying the number of possibilities by 10000. 

Lastly, we need to format the password as bronco{candidate} before hashing, which also happens to be the flag.

Following that, I made a script in python that brute forces the password. Note that it would not be possible to brute force the hash using a dictionary or ruleset due to the length and complexity of the password. [Here's an xkcd](https://xkcd.com/936/) that sort of shares the same idea, but not quite. Still amusing regardless though.

Script:
```python
import itertools
import hashlib

leet_dict = {
    'a': '4', 'b': '8', 'c': '<', 'e': '3', 'g': '6', 'h': '#', 'i': '1',
    'l': '1', 'o': '0', 's': '5', 't': '7', 'z': '2'
}

target_hash = 'ea23f261fff0ebc5b0a5d74621218e413a694ed0815a90615cf6edd7b49e6d0d'

original_str = list("yoshiethehomie")

# Define the replaceable positions as (index, original_char, substitution)
replaceable = [
    (1, 'o', leet_dict['o']),
    (2, 's', leet_dict['s']),
    (3, 'h', leet_dict['h']),
    (4, 'i', leet_dict['i']),
    (5, 'e', leet_dict['e']),
    (6, 't', leet_dict['t']),
    (7, 'h', leet_dict['h']),
    (8, 'e', leet_dict['e']),
    (9, 'h', leet_dict['h']),
    (10, 'o', leet_dict['o']),
    (12, 'i', leet_dict['i']),
    (13, 'e', leet_dict['e']),
]

found = False

for bits in itertools.product([0, 1], repeat=len(replaceable)):
    temp = original_str.copy()
    for i, bit in enumerate(bits):
        if bit:
            idx, orig, sub = replaceable[i]
            temp[idx] = sub
    leet_str = ''.join(temp)
    
    special_positions = []
    for idx, c in enumerate(leet_str):
        if c == 's':
            special_positions.append((idx, '$'))
        elif c == 'i':
            special_positions.append((idx, '!'))
    
    if not special_positions:
        continue  
    
    for pos, replacement in special_positions:
        special_str = leet_str[:pos] + replacement + leet_str[pos+1:]
        
        for num in range(10000):
            candidate = f"{special_str}{num:04}"
            flag = f"bronco{{{candidate}}}"
            hash_obj = hashlib.sha256(flag.encode()).hexdigest()
            if hash_obj == target_hash:
                print(f"Found flag: {flag}")
                found = True
                exit()
    
if not found:
    print("All possibilities exhausted.")
```
Executing the script, my computer finds the flag within.... Actually I never timed it, let me run it again and time it this time. 
![image](https://github.com/user-attachments/assets/9dab7189-8154-4f6b-82e9-83c67ca8f332)

21 seconds! Much more appealing than until the heat death of the universe I must say.
```
bronco{y0sh1eth3hom!e8778}
```
