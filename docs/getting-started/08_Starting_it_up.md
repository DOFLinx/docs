# Starting it up

DOFLinx can be run is two ways:

## Set and Forget (Recommended)

This is where DOFLinx runs all the time in the background and simple
"wakes up" when it sees a process that is configured to run with. By
default, that process is 'Pinball FX2'. DOFLinx uses SFA resources and
can comfortably "sleep" while you run VP or FP, etc.  
To use in this mode, simply add a shortcut to the program into your
Windows start up folder.

This is the mode I designed to utility to work in, and the one I
strongly recommend using.

## Launch Before

In this mode you start the DOFLinx program as a 'Launch Before'
application from your menu system (ie PinballX). You must then stop the
DOFLinx process via a 'Run After' script as well. The best way to stop
DOFLinx is to send it a message using the DOFLinxMsg utility or
something like a VBS script. Killing the process itself is always a bit
ugly.

Both modes have merit, it really comes down to how you want to run
things on your cabinet. Here are a few comparisons.

Set and Forget | Launch Before
---|---
One setup | The process is not running when you use other programs
No need to start and stop processes | 
Can use different colour sets for Pinball FX2 / 3 | 

Regardless of the mode, you may want to consider the mix of programs you
have running that are trying to control your devices. Too many things
trying to control your output board may cause you and your PC some
confusion.
