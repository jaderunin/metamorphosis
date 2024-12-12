# description:
We found this file. Recover the flag.
# solution:
The task was to figure out how the flag was hidden, using network traffic and steganography techniques.
The challenge provided a .pcapng file, which is a network packet capture file. These files are typically used to store data captured from network traffic.I used Wireshark, a popular network protocol analyzer, to open the .pcapng file. The first clue came from the challenge name "Trivial Flag Transfer Protocol," which pointed to TFTP (Trivial File Transfer Protocol) being used in the captured traffic.
Inside Wireshark, I used the display filter tftp to narrow down the packets to those related to TFTP. Upon further filtering with tftp.type, I discovered that TFTP was actively transferring data. This led me to use Wireshark's "Export Objects" feature (File > Export Objects > TFTP > Save All) to extract the files being transferred. One of these files was an instructions.txt file, which contained the following text:    GSGCQBRFAGRAPELCGBHEGENSSVPFBJRZHFGQVFTHVFRBHESYNTGENAFSRE.SVTHERBHGNJNLGBUVQRGURSYNTNAQVJVYYPURPXONPXSBEGURCYNA

Upon inspection, the string appeared to be encoded. After experimenting with different cipher methods, I used ROT13 (a substitution cipher) to decode the message:   TFTPDOESNTENCRYPTOURTRAFFICSOWEMUSTDISGUISEOURFLAGTRANSFER.FIGUREOUTAWAYTOHIDETHEFLAGANDIWILLCHECKBACKFORTHEPL

After formatting the message, it read:   TFTP DOESNT ENCRYPT OUR TRAFFIC SO WE MUST DISGUISE OUR FLAG TRANSFER. FIGURE OUT A WAY TO HIDE THE FLAG AND I WILL CHECK BACK FOR THE PLAN
  
This hinted at the need to hide the flag in some way.

There was another file named plan, and it contained the following text:    VHFRQGURCEBTENZNAQUVQVGJVGU-QHRQVYVTRAPR.PURPXBHGGURCUBGBF
  I applied ROT13 to this text:    IUSEDTHEPROGRAMANDHIDITWITH-DUEDILIGENCE.CHECKOUTTHEPHOTOS
  
This decoded message read:   I USED THE PROGRAM AND HID IT WITH-DUE DILIGENCE. CHECKOUT THE PHOTOS
  
The message suggested checking out photos, which pointed to image files in the TFTP traffic.


    * The file named program appeared to be related to the use of a program for hiding something. It turned out that it was a .deb package, which led me to investigate a tool called Steghide.
    * Steghide is a steganography tool that can hide data in image files (such as BMP, JPEG, etc.).

    * After installing Steghide (sudo apt install steghide), I used it to extract hidden data from the image files. The images were in BMP format, which is supported by Steghide for hiding information.
    * The passphrase for extraction was hinted at in the decoded message: "DUE DILIGENCE."
    * The correct passphrase, without spaces, was used to extract hidden data from picture3.bmp. The flag was successfully revealed: Copy code   picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919} 
this one genuinely screwed me over lol.
# Flag:
picoCTF{qu1t3_a_v13w_2020}
