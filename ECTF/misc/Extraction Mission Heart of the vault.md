## This is probably the most difficult challenge I've solved in this CTF, but also the most fun and definitely my favourite by far.

I was given a password protected zip file. I've never dealt with zip file cracking before, but my instincts told me that it shouldn't be very difficult. After a quick search on DuckDuckGo (because Google won't tell me how to... nevermind), I found a very neat tool on GitHub called [ZipRipper](https://github.com/illsk1lls/ZipRipper/tree/main.)

I ran the zip file through it and the password I got for the zip was 'panget'.

It gave me another zip, named dwarf_vault_199.zip

I realised that there's probably 200 of these zips, and if I was going to use ZipRipper every time, I would likely have grandkids before I get the flag. Or, at least I would lose a lot of valuable time that could've been spent on solving more flags. 

For automation, I looked for command line options for cracking zip file passwords, and found a really useful utility on my Kali WSL that I didn't even know I had called fcrackzip. It was FAST. I quickly got to writing a script to automate the commands, and after a couple minutes of tinkering, it worked like a charm.



``` python
import os
vault = 199
while vault > 0:
  password = os.popen(f"fcrackzip -u -D -p '/usr/share/wordlists/rockyou.txt' dwarf_vault_{vault}.zip").read()[28:].strip()
  print(password)
  print(os.getcwd())
  os.system(f"unzip -P {password} dwarf_vault_{vault}.zip")
  vault = vault - 1
```

![image](https://github.com/user-attachments/assets/23618175-3ad2-409a-b3c8-7dd3da357832)

What I got from the last zip are two files: one called mining_report.txt and the other called drop_pod.py. 
![image](https://github.com/user-attachments/assets/fd504fac-652e-48e2-badb-2004b9060e1e)

After analysing the two files for a couple minutes, I figured out the structure. In the script, each letter of the flag was outputted by an array of pairs [x,y] for which x is a string in a list of the passwords used to decrypt the zip files, and y is the index of string x. At first I tried taking the first and last 29 consecutive passwords in forward and backward order, which didn't work. Then I realised I hadn't been zero indexing the second index, so I did that for the last 29 passwords in backward order and got the flag.

![image](https://github.com/user-attachments/assets/a2f02fe5-8664-4f29-8f6f-786d1f741b9f)
##### My (mostly un)successful attempt(s)

```
ectf{d1ggy_d1ggy_h0l3}
```

Postscript: I probably should've scripted the last part.
