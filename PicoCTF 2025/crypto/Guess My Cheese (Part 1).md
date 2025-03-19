# This was pretty fun because it had me learning about a brand new cipher type. On with the problem!
![image](https://github.com/user-attachments/assets/3c171448-733d-4a91-84a8-431c36b5d7e5)

When I connected to the instance, I saw an encryption unlike anything I'd seen before. It somewhat resembles caesar, but after testing with a caesar cracker I concluded that it was definitely not caesar.
![image](https://github.com/user-attachments/assets/99bd63a0-cce5-43da-9ed4-6db5282852ac)
Then, I had a look at the hint to see if it could give me anything useful.
![image](https://github.com/user-attachments/assets/72d829d0-3108-4f23-a16a-3f59848d7e69)

This told me that the cipher had something to do with linear equations. After some digging, I found out about affine ciphers. I had learnt a bit about affine transformations when I was researching AES for my extended essay (long story), so I figured it would basically be the same thing. I input "swiss" to the encrypter to see what it would output, and I got FPTFF. So definitely, I was on the right track. I then tried solving for the paramters of the affine cipher for which F(x)=(ax+b) mod 26. I began with mapping out the letters for "swiss" to their corresponding alphabet positions (18, 22, 8, 18, 18). Then, I mapped out the corresponding alphabet positions for the output letters (5, 15, 19, 5, 5). Lastly, I constructed a system of linear equations using the first two letters to solve for a and b.
![image](https://github.com/user-attachments/assets/c62b54f6-3ecc-479e-8437-55d87ec63f2b)
Using a and b, I then wrote a script that deciphers the given ciphertext IWHMAQZJIG.

```python
ciphertext = "IWHMAQZJIG"
a = 9
b = 25
a_inv = 3
plaintext = ""

for char in ciphertext:
        x = ord(char) - ord('A')
        plain_index = (a_inv * (x - b)) % 26
        plaintext += chr(plain_index + ord('A'))


print("Cheese:", plaintext)
```

![image](https://github.com/user-attachments/assets/94e59a57-09e7-4651-a057-937efbd1ce86)

Putting in the cheese from the script, we get the flag
![image](https://github.com/user-attachments/assets/93d87281-168b-4eca-bffc-a5b1046c0566)

```picoCTF{ChEeSy6320b114}```
