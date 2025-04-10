# Run DOFLinx with Sufficient Access

DOFLinx needs to run with access to the /dev/input/ path.
Some versions of Linux, such as that on the Raspberry Pi have this access by default, others do not.
The reason for this is that DOFLinx needs to monitor the raw keyboard inputs of all keyboard devices such as an iPac, Pinscape, etc.
This is so that DOFlinx can determine when a button is pressed while Mame (and other things) are the in focus / foreground applications.
The raw keyboard input files /dev/input/by-path/*-kbd are owned and controlled by root as part of the Linux system.

If DOFLinx does not have access to input devices then button input cannot be monitored.
The use of input buttons in DOFLinx will be logged and disabled for that session.
Without being able to check on pressed keys then DOFLinx cannot determine when Coin, Pause, P1, P2, Exit, and all other Mame input keys are pressed.
DOFLinx needs this monitoring for proper operation and triggering. 
