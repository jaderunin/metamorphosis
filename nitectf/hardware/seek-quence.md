I started by going through the schematic, which had AND, OR, and NOT gates, D-flip-flops, an 8-bit shift register, and comparators. The comparators caught my attention because some bits were pulled high and some low, representing the byte patterns `00000101` and `00010101`. These patterns were inverted at the output and fed into an OR gate. To unlock the system, the OR gate's output had to be 0, meaning the comparators needed to get those exact byte patterns as input.

The two shift registers were connected in a way that extended them into a 16-bit register, with the last bit of the first register feeding into the second. So, the full sequence I needed to send into the registers was `0001010100000101`. The challenge was figuring out how to input this pattern step by step.

My teammate  noticed that an AND gate controlled the input to the first shift register, and it would only output 1 if two D-flip-flops were set to 1 and the input to the AND gate was 0. The D-flip-flops were triggered on the rising edge of the clock, so we needed a specific input sequence to get them both to 1. I simulated this in Logisim-evolution and found that the sequence `1010` did the trick.

Once we had the AND gate working, my friend moved on to loading the shift registers with the required pattern. By adding `10` to the input sequence after the initial `1010`, I got the first register to output `00000101`. Repeating the same process loaded `00010101` into the second register. Some extra padding was needed to shift the bits into the right positions, and this is around where we got stuck lol

