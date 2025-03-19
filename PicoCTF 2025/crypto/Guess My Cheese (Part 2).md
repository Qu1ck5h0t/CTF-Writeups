# Disclaimer: The following solution is 100% NOT the intended solution to this challenge. It is incredibly slower, but also 10 times funnier (and we ran out of ideas before attempting this). Solving this chall using my solution is one of the biggest achievements of my life, and the fallout that followed the flag capture was beautiful.
![image](https://github.com/user-attachments/assets/242707c0-3dec-4a67-a6e5-42bfa77cf859)

When connecting to the netcat we are given a hash. According to the hints, the hash is SHA256 with "2 nibbles of hexadecimal character salt". Also the hints mentioned rainbow tables but we didn't try that after we saw some guys fail to find the flag when their rainbow table exceeded 30GB. Since we're given a wordlist, my initial idea was to simply crack the hash by making a script that appends salt. 
![image](https://github.com/user-attachments/assets/2c944d21-75fd-4ef2-8395-b1b43c527524)

Question is: how? Well, I know that a nibble is half a byte, the salt is two nibbles and each hex character holds 1 nibble of data. Thus, the salt has to be two hexadecimal characters. I began with appending every possible 2 hex character combination before each word, then after each word, then one hex char before the word and one after. Then I tried the hex chars in uppercase. Then I tried treating the nibble data literally, rather as UTF-8 characters. Then I tried a script that puts every possible nibble in every possible position in each word in the wordlist. None of those attempts matched the hash I was given, and our entire team was furious.
![image](https://github.com/user-attachments/assets/d9c0f847-12f8-4041-82eb-62a21ac8747f)

Then all of a sudden, I had a bright idea. The problem would ask for the cheese and salt at the same time, and rejects the answer if one or both of them is wrong. However, it doesn't ask for the POSITION of the salt. Furthermore, connection and inputs can be made programmically. And to make things better, the instance's address and port remains constant. Therefore, it is hypotehtically possible to make a brute force script that tries the same cheese and salt combination every single time. 

There are 600 cheeses in the wordlist and 256 possible salts, so after crunching the numbers there are only 153600 possible combinations. Given that the CTF is over a week long, brute forcing one single cheese within the time limits is actually feasible. I quickly went on to make a script that does the brute forcing:
```python
import socket
import sys

HOST = "verbal-sleep.picoctf.net"
PORT = 54640

def wait_for_prompt(file_obj, prompt):
    output = ""
    while True:
        line = file_obj.readline()
        if not line:  # connection closed
            break
        decoded_line = line.decode("utf-8", errors="ignore")
        
        output += decoded_line
        if prompt in decoded_line:
            break
    return output

while True:
    try:
        # Connect to the remote host and port
        with socket.create_connection((HOST, PORT)) as sock:
            # Use makefile for easier reading/writing (binary mode)
            with sock.makefile('rwb') as f:
                # Wait until the prompt "What would you like to do?" appears
                wait_for_prompt(f, "What would you like to do?")
                # Send "g" followed by newline
                f.write(b"g\n")
                f.flush()

                wait_for_prompt(f, "So...what's my cheese?")
                # Send "Blue" followed by newline
                f.write(b"Blue\n")
                f.flush()

                wait_for_prompt(f, "Annnnd...what's my salt?")
                # Send "00" followed by newline
                f.write(b"00\n")
                f.flush()

                # After sending the final input, read all remaining output until the connection is closed
                final_output = f.read()  # This will read until EOF
                decoded_final_output = final_output.decode("utf-8", errors="ignore")
                print(decoded_final_output)

                # If "pico" is found anywhere in the output, terminate the script
                if "pico" in decoded_final_output:
                    print("Flag found!")
                    sys.exit(0)
    except Exception as e:
        print(f"An error occurred: {e}")
```
I made a variation of the script that tests the amount of tries my computer could do in a second, and after doing some maths I calculated that it should theoretically take me around 8 hours to find the flag. Then I learnt about exponential distribution... As a result I asked my teammates to run the same script.

After around 4 hours of the team brute forcing, Cloud got the flag

![image](https://github.com/user-attachments/assets/cc545df7-4334-4a41-8788-e8dae70b291d)
```
picoCTF{cHeEsY6ce3864c}
```



Though, I'm sure this isn't exactly the most "satisfying" solution. So here's what my friend Flum who solved the flag had to say about it after our team had solved the flag:

![image](https://github.com/user-attachments/assets/41dd9897-8c28-4ea0-8e61-990228e269d6)

Lowercase letters and no whitespaces. All I had to do was that, all along.

Postscript: Looking back, what we did is somewhat similar to a bitcoin mining pool which is pretty funny. I'm glad we got to capitalise on that with some very fitting humour in the Discord server chat.
