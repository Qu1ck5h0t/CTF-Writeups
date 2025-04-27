# This was the first challenge I solved, which I got within 12 minutes of the CTF starting. I was the 5th guy to solve it.
![image](https://github.com/user-attachments/assets/88d33979-9a85-4fbc-815f-202698936853)
From the challenge, we are given a panorama image. It's often useless to reverse image search a panorama, so what I did was I used a [website](https://www.chiefarchitect.com/products/360-panorama-viewer/) to turn the panorama into a 360 degree scene, and took a screenshot of the bridge part.
![image](https://github.com/user-attachments/assets/5a2095a5-685c-41a8-8952-048687527931)
I then reverse image searched the above image, and found a [facebook post](https://www.facebook.com/100051181128902/posts/2267045090100363/) regarding a memorial day celebration on that bridge, where the name of the bridge was given as Putnam Bridge. I put the name in Google maps to then get the city and postal code, which was then put together to obtain the flag.

```UMDCTF{Putnam Bridge, Marietta, OH 45750}```
