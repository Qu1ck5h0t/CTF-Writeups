## I'm a bit late on the writeup due to having to do a lot of things when I was going to write it, so here I am. This was fun because I got to do a lot of hash cracking, which was the first thing I've ever done in cryptography CTF rooms.
![image](https://github.com/user-attachments/assets/6c1bf125-db08-4b72-b5d1-b0ca095214d3)
When I unzipped the file, there were three files, being an excel spreadsheet, a password protected zip file and a wordlist. I noticed that the spreadsheet, parts.xlsx was password protected.

After some searches, I figured out that the whole file is encrypted unlike the more common method for "password protecting" an excel spreadsheet for which protection can be removed by simply changing the file extension to .zip and then removing a string involving "sheetProtection" line from the xml file. 
I found out that the encryption is a hash, so after running the file through an online hash extractor after failing to get office2john.py to work, I got this:

```$office$*2013*100000*256*16*d6a9c9e885c7598e216ef9f757788a5c*76091527bca96e559a934f13e19057c9*5a947c513545093c3198fb6213ecf202a01aff188537f01a58cf1aec03558a79```

From there, I used johntheripper to crack the hash of the excel password with the following command:

```john --rules --wordlist=wordlist.txt hash.txt```

As a result, I got "dolphin" as the password. From there, I opened the file with the password and saw three "parts". 

The first part was "036074c2585230c1ad9e6b654a1671ac13ee856eb505f44346593e1748a6a52a", which appears to be an SHA256 hash at first. 

I couldn't get it to work with any SHA algo on hashcat or johntheripper, so it definitely wasn't SHA256 given that the resultant password exists in the wordlist I used, so if it were SHA256 it would've been cracked. An [online tool](https://hashes.com/en/decrypt/hash) was able to crack it, however (without giving me the algorithm though, which was pretty annoying). After cracking the hash, I got "spooky".

![image](https://github.com/user-attachments/assets/9febff0c-d94e-452f-8aff-8862cd3a461f)

The second part, "2H8ZcpmQyRisn" was base58, and after running it through cyberchef I got "digestive".

The third part, "cHJlc2NyaXB0aW9u" was base64, and after running it through cyberchef I got "prescription".

Given that the zip file's name is "Format_excelPassword_Part1_Part2_Part3", I put together the password following the format "dolphin_spooky_digestive_prescription".
![image](https://github.com/user-attachments/assets/405ea749-2a4d-45b8-b194-731f1f08b87f)
```ECTF{J0nH_tH3_Cr4ck3R_95234826}```
