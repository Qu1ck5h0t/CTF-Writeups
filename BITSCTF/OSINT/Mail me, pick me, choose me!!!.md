## This is probably my greatest achievment in BITSCTF. I was the second person to solve this problem, which took literally two days after the demons who got first blood. Next time I'll be first though...

<img width="480" alt="image" src="https://github.com/user-attachments/assets/90cea482-7e09-4116-84c2-a05672347045" />

The challenge begins with a cryptic message written by "phineas". While there aren't any apparent clues at first, there is a mention of "my-diary" which turns out to be a website. 
Using some very basic Google dorking, I found a series of diary entries with the title "Sad". 
<img width="1012" alt="image" src="https://github.com/user-attachments/assets/07429576-548d-40ef-b2c4-1d8177c5ea0b" />

After reading through a series of very well written diary entries that were probably written by a guy who went through an emo phase in the 2000s, I found a mention of a user named kumarsinghamed.
![image](https://github.com/user-attachments/assets/41fa46ba-bba1-4a1b-9aee-fb77bc40ab17)
There was not much online about this person, and I'm pretty sure the pintrest profile was somebody else. I ended up finding a user with that username on twitter, but none of his posts (some of which were ciphers in braille, morse and base64) made sense to me.

That was when I contacted the organisers for a clarification, and it turns out that they had made a mistake with the braille as the person who made the challenge was unaware of the preceding character needed to declare numbers in braille (numbers and letters use the same characters), and thus the cipher was messed up. Furthermore, he should've declared which letters were capital due to base64 being case sensitive.
He soon posted what he meant to cipher in ASCII format, though that was still coded in base64. The error post has since been deleted, but here's a recreation of the post ciphered back from when I decoded it, as well as his correction post.
![image](https://github.com/user-attachments/assets/8af1d46b-71c2-4dcd-9cc7-7af25c607d44)

![image](https://github.com/user-attachments/assets/ebcd0cb3-2214-4874-94ca-da7a6232ab4e)

Decoding from base64, we get "pokemonkumarrai". There aren't any hints after this which is why a lot of contestants argued that it was "guessy", but since the title had the word "mail" in it and the organisers had hinted at something similar when I brought up the ticket, I tried to mail the user. It was a bit confusing since I didn't know what email they'd use, so I tried Proton Mail (which was included in one of the posts the account had retweeted) and Gmail (the most common email provider in the west). Before long, I got an automated response from the Gmail with my flag.
![image](https://github.com/user-attachments/assets/5dc95453-83a1-402d-83f4-a28c2428f1b1) 
```BITSCTF{1_4m_6047}```

Postscript: It turned out later on that I was right to get the error clarified since people started getting the flag at a rapid rate after I did. I'm still not sure how the first guy got it, but I was the first person to get the flag over 48 hours since the he did so I'm pretty proud nontheless.
