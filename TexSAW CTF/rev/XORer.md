# I usually suck at rev so this was a nice boost to my confidence, as well as a warmup to the slightly more difficult challs
![image](https://github.com/user-attachments/assets/36c547b7-eb6c-4e69-91c4-cf74826ab6c7)

The challenge gives a binary file that asks for a password. When run through ghidra, the following code is decompiled:
``` C
void check_password(char *input)

{
  uchar key [12];
  int len;
  int i;
  
  key[0] = 0xcb;
  key[1] = 0x95;
  key[2] = 0xd1;
  key[3] = 0xfa;
  key[4] = 0xd1;
  key[5] = 0xcd;
  key[6] = 0x96;
  key[7] = 0xfa;
  key[8] = 0xc3;
  key[9] = 0xc9;
  key[10] = 0x91;
  key[0xb] = 0xc2;
  strlen(input);
  i = 0;
  while( true ) {
    if (7 < i) {
      printf("Correct! Here\'s your flag: texsaw{%s}\n",input);
      return;
    }
    if (((int)input[i] ^ 0xa5U) != (uint)key[i]) break;
    i = i + 1;
  }
  puts("Wrong password!");
  return;
}
```
What this code does is that it checks the first 7 bytes of user input against each key byte that is XORed with ```a5```, and prints out the user input in the flag format if correct. To solve for the flag, simply XOR each byte in the key against the ```a5``` byte to get the flag. This can be done in cyberchef as below:
![image](https://github.com/user-attachments/assets/f308e592-7b72-4ff0-a66f-757948deb63d)

```texsaw{n0t_th3_fl4g}```
