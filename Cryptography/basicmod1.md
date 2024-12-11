# Description:
We found this weird message being passed around on the servers, we think we have a working decryption scheme.
Download the message here.

Take each number mod 37 and map it to the following character set: 0-25 is the alphabet (uppercase), 26-35 are the decimal digits, and 36 is an underscore.
Wrap your decrypted message in the picoCTF flag format (i.e. picoCTF{decrypted_message})
# Solution:
GPT’d a c pgm for it

```
#include <stdio.h>

int main() {
    // Define the cipher array containing the encoded numbers
    int cipher[] = {128, 322, 353, 235, 336, 73, 198, 332, 202, 285, 57, 87, 262, 221, 218, 405, 335, 101, 256, 227, 112, 140};

    int i, j;
    // Define an array with digits '0' to '9' for decoding
    char dec[] = {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9'};

    // Array to store the remainder values when each cipher number is divided by 37
    int rem[22];

    // Loop over each cipher number to compute the remainder when divided by 37
    for (i = 0; i < 22; i++) {
        rem[i] = cipher[i] % 37;  // Modulo operation to get remainder
    }

    // Array to store the decoded flag characters
    char flag[22];

    // Loop over the remainders and map them to characters
    for (i = 0; i < 22; i++) {
        // If remainder is between 0 and 25, map it to 'A' to 'Z'
        if (rem[i] >= 0 && rem[i] <= 25) {
            flag[i] = (char)(rem[i] + 'A');  // Convert to 'A' to 'Z'
        }
        // If remainder is between 26 and 35, map it to '0' to '9'
        else if (rem[i] >= 26 && rem[i] <= 35) {
            flag[i] = dec[rem[i] - 26];  // Convert to '0' to '9'
        }
        // If remainder is 36, map it to '_'
        else {
            flag[i] = '_';  // Underscore is used for remainder 36
        }
    }

    // Print the decoded flag
    printf("Flag is: ");
    for (i = 0; i < 22; i++) {
        printf("%c", flag[i]);  // Print each character of the decoded flag
    }

    return 0;
}


Output: `Flag is: R0UND_N_R0UND_79C18FB3`
```
# Flag:
picoCTF{R0UND_N_R0UND_79C18FB3}
