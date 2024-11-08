# Description:
This vault uses for-loops and byte arrays. The source code for this vault is here: VaultDoor3.java
# Hint:
Make a table that contains each value of the loop variables and the corresponding buffer index that it writes to.
# Procedure
'buffer' is the string that was produced by the VaultDoor3 Java program after all transformations. This string is known, and we are trying to find the input that produces this output.
'password' is an array of 33 characters (32 characters for the password plus a null terminator) that will store the reconstructed original password, of value 0 to prevent garbage values. 
In the original Java code, the first loop directly copies the first 8 characters of the input string to buffer[0] through buffer[7]. 
To reverse this, I  set password[0] to password[7] = buffer[0] to buffer[7].
Then I noticed buffer[8] through buffer[15] was filled with characters from password using password.charAt(23 - i), so i reveresed it by using buffer[8] to buffer[15] = password[15] to password[8].
The code filled buffer[16] through buffer[31] at even indices using password.charAt(46 - i)  while reversing, I assigned password[30] down to password[16] using buffer[16] through buffer[30] at every even index.
The last loop in the Java code fills odd indices from buffer[31] down to buffer[17] using characters directly from the input so I directly assigned password[31] down to password[17] using buffer[31] to buffer[17].
Finally, I printed it in the format picoCTF{<password>} as expected by the original prompt.
## code
#include <stdio.h>
#include <string.h>

int main() {

    char buffer[] = "jU5t_a_sna_3lpm18g947_u_4_m9r54f";
    char password[33]; 

    
    memset(password, 0, sizeof(password));

    
    for (int i = 0; i < 8; i++) {
        password[i] = buffer[i];
    }


    for (int i = 8; i < 16; i++) {
        password[23 - i] = buffer[i];
    }

   
    for (int i = 16; i < 32; i += 2) {
        password[46 - i] = buffer[i];
    }

    
    for (int i = 31; i >= 17; i -= 2) {
        password[i] = buffer[i];
    }

   
    printf("The correct password is: picoCTF{%s}\n", password);

    return 0;
}

# Flag
> picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_79958f}
