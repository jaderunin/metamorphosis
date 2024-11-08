# Description
Decode this message from the moon.

# Hints:
How did pictures from the moon landing get sent back to Earth?
What is the CMU mascot?, that might help select a RX option.

# Procedure:
I found that pictures from the moon were received back on earth by QSSTV which is a utility for dealing with slow scan television signals (SSTV) which transmits and receives still images over radio frequenices.
so I installed qsstv
> apurva@Deepas-MacBook-Air ~ %  sudo apt-get install pavucontrol
> apurva@Deepas-MacBook-Air ~ %  pavucontrol
> apurva@Deepas-MacBook-Air ~ %  pactl load-module module-null-sink sink_name=virtual-cable
> apurva@Deepas-MacBook-Air ~ % qsstv &
> apurva@Deepas-MacBook-Air ~ %  pavucontrol &
> apurva@Deepas-MacBook-Air ~ %  paplay -d virtual-cable /Users/apurva/Downloads/messages.wav

# FLAG
> picoCTF{beep_boop_im_in_space}
