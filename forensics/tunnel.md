
# description:
We found this file. Recover the flag.
# solution:

First, I checked the file type  
The output indicated that the file was of "data" type, which didn't provide much useful information. Next, I performed a hex dump to inspect the file's raw content
The first few lines of the dump showed that the file began with 42 4d, which are the magic bytes for a BMP (Bitmap) file format. This led me to believe that the file might be a corrupted BMP image.

I renamed the file from tunn3l_v1s10n to tunn3l_v1s10n.bmp, hoping it might be recognized as a BMP file. When I tried to open it, I received an error stating that the format was not supported.

I suspected that the file header might be corrupted. I used a hex editor to correct the BMP header.
I researched the correct "magic bytes" for a BMP file and found the proper ones. After adjusting the header, I saved the file and tried opening it again. It was clear that the image contained information, but the flag wasn't immediately visible.

After some thinking, I recalled that the dimensions of the image might be incorrect. The flag could be hidden in a part of the image that was off-screen due to incorrect width or height values.
I researched how to modify the dimensions of a BMP file and adjusted the height and width bytes accordingly.
After adjusting the dimensions, I reopened the image. This time, the flag became visible in the image

# flag:
picoCTF{qu1t3_a_v13w_2020}
