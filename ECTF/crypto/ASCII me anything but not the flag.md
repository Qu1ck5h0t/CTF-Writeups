## This is the first challenge I tackled for the CTF. I found it quite easy, but the triple encryption made it quite fun.

<img width="502" alt="image" src="https://github.com/user-attachments/assets/7b46de5e-52ff-4e18-9dbd-605cabb37d6e" />


Converting from denary to ASCII, we get this

```
ldom{Uc1z_j5_Oo3_X4t_0m_3oXyZkaj0i}

Ebob fp vlro hbv, dlla irzh : HBVHBV

Well done, but now do you know about the guy who got stabbed 23 times ?
```

I think the guy who got stabbed was ceasar. I also think there's a cipher named after him, so I tried that.

After shifting 23 places, I got

```
"ogrp{Xf1c_m5_Rr3_A4w_0p_3rAbCndm0l}
```

Here is your key, good luck : KEYKEY"

The format resembled Vigenère, so I tried a Vigenère decipher with the key 'KEYKEY'

ectf{Th1s_i5_Th3_W4y_0f_3nCrYpti0n}
