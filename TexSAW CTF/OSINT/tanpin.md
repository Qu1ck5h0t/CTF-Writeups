# This was by far the most difficult chall I solved all weekend, as well as the chall I spent the most time on. I would have no shot at placing where I did if not for this solution, enjoy.
![image](https://github.com/user-attachments/assets/8f6a61db-3c53-4942-ba13-d8792ac7631d)

Given image:
![image](https://github.com/user-attachments/assets/b6233e42-71a1-4e06-b807-6b7a3761977c)


The first step to the solution was pretty obvious - I just have to find the video. Given that there does not exist a youtube search filter that specifies the month the video is released, I used the following search term to narrow it down to 2024:

```合作 before:2025 after:2023```

After doing some maths I figured that my target video would've been posted 6 months ago, and I found just one video that followed the criteria (clicky):

[![image](https://img.youtube.com/vi/-c6fmouqPUI/0.jpg)](https://www.youtube.com/watch?v=-c6fmouqPUI)

Title: このメドレーのこの部分が好きなのでここだけ作りました！合作＋ BASIC

The thing was a 1h20m long compilation of japanese brainrot anime meme culture. After looking through all the "most viewed" parts, I did not find the target. However, I did identify that "doctor" from the screenshot was present in live chat, so I thought that had to be it. I called my friend on Discord, screenshared and we watched the whole video together. Well I did, he left halfway through. Unfortunately, I did not find that moment anywhere in the video, but at least the music and editing was good.

Then, in the description I found a link to another video:

[![image](https://img.youtube.com/vi/pxyONEf8ZGE/0.jpg)](https://www.youtube.com/watch?v=pxyONEf8ZGE)

Title: このメドレーのこの部分が好きなのでここだけ作りました！合作＋ ADVANCED

Again, our friend doctor was present in live chat so I knew that this was likely it. However, I was not about to waste almost 2 hours of my life on brainrot, so instead I wasted those two hours downloading the videos, then coding and running a script that tries to find the images from the video. Long story short, the script worked on other videos but somehow not those ones. However, I then realised that what doctor said in live chat is distinct from what everyone else was spamming (神, which means god/deity in both Japanese and Chinese, so like saying "godly"). 

I used a [Japanese OCR tool](https://www.i2ocr.com/free-online-japanese-ocr) online to extract the text contents of his comment, and downloaded the live chat logs using a [chrome extension](https://chromewebstore.google.com/detail/ycs-youtube-comment-searc/pmfhcilikeembgbiadjiojgfgcfbcoaa). I found the specific comment (文字出し神過ぎる, don't ask me what that means) in the second video at ```2024-09-15T14:59:25```. Since the given timestamp is not relative to the video, I had to find a comment posted at the first second of the video and find the difference. I found a comment at ```2024-09-15T14:03:05``` so I could conclude that the timestamp relative to the video is around 56:20. While the actual timestamp turned out to be 56:35 for some reason, I did find the timestamp.

From there, things were much easier - or so I thought. Finding the girl wasn't hard, even though her face isn't in that frame one could still identify her pigtails, so all I had to do was go back a few seconds, find the girl with the pigtails and reverse image search frames with her in it to reveal her to be ```Aya Komichi```. The second part was a lot harder, I do not understand Japanese so thankfully there were lyrics on the screen. 

However I could not identify those lyrics, and neither could my OCR website. What I ended up doing was going to a Japanese discord server where somebody identified the text of the following frame:
![image](https://github.com/user-attachments/assets/de242e29-4528-47b4-b793-f3e76dd500ef)

To be  ```離さないルールとして```. 

I didn't think I wanted to know anything about baseball despite what my search engine returned me when looking it up, so I looked up the phrase on youtube instead and found the music video for "Ice Drop", featuring Hatsune Miku. I assumed that that was the correct song for the following step, given that it is the first search result and has an English name.

My next and final step was to find the author of that specific part of the video. Luckily for me, the video's description has a [spreadsheet](https://docs.google.com/spreadsheets/d/1p58XfZqNvvuzFX9XelQlE3fcvYq9dwLglwJz9MKwxq8/edit?gid=253941028#gid=253941028) of all the songs featured and the respective editors that used the music. There were no results for "Ice Drop", but by using its Japanese name listed in the MV's description, I found that it was made by ```ねそ```. 
![image](https://github.com/user-attachments/assets/633880bf-a338-4496-bdfb-7bf783340e60)

Looking up their username on youtube, I found a user with the same handle to be ```@ねそ-l9b```. So now that I had all the information I need, I could assemble the flag.


```texsaw{pxyONEf8ZGE,ice drop,aya komichi,ねそ-l9b}```
