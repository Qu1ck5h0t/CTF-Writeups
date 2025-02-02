## It actually took me longer to realise the solution than it sounds. But the troll was pretty funny though.
<img width="480" alt="image" src="https://github.com/user-attachments/assets/57517941-e19a-4695-8294-9b3aa569c341" />

When I unzipped the challenge file, my immediate thought was to run it through steghide. Well, that didn't go too well.

Then I started looking at the image, and initially I turned up the exposure to see if there was anything I couldn't see at the current exposure, similar to a problem from the last CTF I did. 

Turns out I was wrong on that as well, but that was when I noticed what seemed like braille, so I began with translating the braille code on the larger painting. 

<img width="249" alt="image" src="https://github.com/user-attachments/assets/db8fccfb-1d9b-4700-9f2a-920a3dd9dece" />

"this is jus a dummy nice try" (the guy in the DM is the creator of this challenge)

Well that was funny. Great usage of 10 minutes of my time. But what that also told me was that the dots are indeed braille, and that the other braille code is likely to be the flag. Translating from braille, I got

![image](https://github.com/user-attachments/assets/2f59b66b-49d3-4f9d-a0b6-f73267d5cf6d)

```
ectf{h1dd3n_1n_th3_d4rkn3ss}
```
