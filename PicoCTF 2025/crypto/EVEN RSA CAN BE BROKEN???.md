# This challenge helped me reinforce some of my fundamentals with RSA, which is very helpful because I tend to screw up a lot with RSA challs
![image](https://github.com/user-attachments/assets/cad00a0c-392c-4630-af04-3853a3db5292)

Immediately upon connecting to the netcat instance, we can see the product of primes (n), public exponent (e) and ciphertext (c). Since the value for e is pretty standard, the most straightforward way to tackle RSA problems like this begins with finding the factors of n, which we define as p and q. Luckily for us, n is an even number which means that p and q are simply 2, and whatever n divided by 2 is. 
![image](https://github.com/user-attachments/assets/5101f779-a524-4b1d-8e2d-44117f8fd7c3)

Then, we can write a script that computes the plaintext for us.
```python
from Crypto.Util.number import long_to_bytes, inverse

N = 26182248720099819302490779307982708353128029016659872997261867782641731113593583949785049822743757267241470388041235766976005207359852316216888758091847726
e = 65537
c = 11146502590774748901638204145747813810353895561314754008831714874019207255942870875326160084132231742786246254529080554454484214921337929514473478303362855

# Factor N
q = N // 2

# Find phi
phi = q - 1

# Calculate the private exponent d
d = inverse(e, phi)

# Decrypt the ciphertext
m = pow(c, d, N)

print(long_to_bytes(m).decode('utf-8'))
```
Euler's toilent function (phi) here is simply q - 1, as normally ϕ(N)=(p-1)(q-1) but since p here is just 2, ϕ(N) becomes (1)(q-1). Then, we obtain the private exponent d by getting the modular inverse of e modulo phi. Finally, raising the ciphertext to the power of d modulo N returns the plaintext, which we then convert to bytes and utf 8 to get the flag.
![image](https://github.com/user-attachments/assets/0c3f7321-8457-40a9-a4ec-b086ced10478)

```picoCTF{tw0_1$_pr!m3}```
