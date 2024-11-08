# Description
Let's start off simple, can you overflow the correct buffer? The program is available here. You can view source here.
Additional details will be available after launching your challenge instance.

# Hints 
How can you trigger the flag to print?
If you try to do the math by hand, maybe try and add a few more characters. Sometimes there are things you aren't expecting.
Run man gets and read the BUGS section. How many characters can the program really read?

# Procedure 
source code and program is provided but i didn't find the program useful.
I saw a variable being initialized as char buf2[16]; By typing any number with greater than 16 digits, it overflows and prints out the flag.


# Flag
> picoCTF{ov3rfl0ws_ar3nt_that_bad_ef01832d}

