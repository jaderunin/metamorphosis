# Description:
A new modular challenge!

Download the message `here`.

Take each number mod 41 and find the modular inverse for the result. Then map to the following character set: 1-26 are the alphabet, 27-36 are the decimal digits, and 37 is an underscore.

Wrap your decrypted message in the picoCTF flag format (i.e. picoCTF{decrypted_message})
# Solution: 
Read about mod inverse and how to find it then GPT’d a program for it in python 

## Cipher values and constants
cipher = [268, 413, 438, 313, 426, 337, 272, 188, 392, 338, 77, 332, 139, 113, 92, 239, 247, 120, 419, 72, 295, 190, 131]
modulus = 41

##  Initialize mod inverse array
modinv = []

# Calculate modular inverses
for value in cipher:
    for j in range(modulus):
        if (value * j) % modulus == 1:
            modinv.append(j)
            break

## Mapping for decoding
flag = []

# Decode the flag
for inv in modinv:
    if 1 <= inv <= 26:  # Letters A-Z
        flag.append(chr(inv - 1 + ord('A')))
    elif 27 <= inv <= 36:  # Digits 0-9
        flag.append(chr(inv - 27 + ord('0')))
    else:  # Underscore for other values
        flag.append('_')

## Output the decoded flag
decoded_flag = ''.join(flag)
print("Flag is:", decoded_flag)
# flag: 
picoCTF{1NV3R53LY_H4RD_DADAACAA}
