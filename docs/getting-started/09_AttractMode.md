# Attract Mode

DOFLinx can be setup to “play” a series of display items in a variety of sequences to create an attract mode display.  In addition, Attract Mode can display marquees on your Pixelcade or DMD device.  This guide will help explain how to setup and use that function.

There are two parts to attract mode, the setup, then the starting and stopping of “playing” the display.  You can load a single attract mode sequence and use it multiple times.  You can load a new attract mode sequence at any time.

Loading the attract mode sequence is via the ATTRACT\_SETUP= parameter.  This parameter has a single number as the first item that defines the time unit of measure in mS that each display item will use via its multiplier.  The rest of the parameter is a repeating sequence of five items being the display item number, the device/port, the colour (or on/off for mono devices), multiplier of the time unit, then finally the next item number to “play”.

If you have RGB outputs on output device #1 using port #1 and port #4 they would be defined as 1001 and 1004.  To make an attract mode that plays red – blue repeating at 1 second intervals you would set the delay to 1000mS = 1 second, then two display item groups being display item group 1 on device/port 1001 for Red followed by display item group 2 on device/port 1004 for Blue.  In a simple table it looks like;

|  | Display Item #1 | Display Item #2 |
| --- | --- | --- |
| ID Number | 1 | 2 |
| Device | 1001 | 1004 |
| Colour | Red | Blue |
| Time Multiplier | 1 | 1 |
| Next ID Number | 2 | 1 |

The parameter would then be

ATTRACT\_SETUP=1000,1,1001,Red,1,2,2,1004,Blue,1,1

If you wanted the above RGB outputs to go off in between, so flip-flop between red and blue you need a sequence of Red – Off – Blue – Off repeating with the off items running in parallel to the on items.  This would look like;

|  | Display Item #1 | Display Item #2 | Display Item #3 | Display Item #4 |
| --- | --- | --- | --- | --- |
| ID Number | 1 | 1 | 2 | 2 |
| Device | 1001 | 1004 | 1004 | 1001 |
| Colour | Red | Black | Blue | Black |
| Time Multiplier | 1 | 0 | 1 | 0 |
| Next ID Number | 2 | 0 | 1 | 0 |

The parameter would then be

ATTRACT\_SETUP=1000,1,1001,Red,1,2,1,1004,Black,0,0,2,1004,Blue,1,1,2,1001,Black,0,0

Once loaded the attract mode sequence is started or stopped by using ATTRACT\_MODE=1 or ATTRACT\_MODE=0 respectively.

Attract mode sequences are very flexible.  There are a number of basic sequence types that can be setup.  They can be combined to form more complex sequences.

**_Sequential_**

To play at increasing increments and cycle

A-> B -> C ->D -> E -> A

|  | A | B | C | D | E |
| --- | --- | --- | --- | --- | --- |
| ID Number | 1 | 2 | 3 | 4 | 5 |
| Device | 1001 | 1004 | 1007 | 1010 | 1013 |
| Colour | Orange | Pink | Green | Yellow | Blue |
| Unit | 1 | 2 | 4 | 8 | 16 |
| Next ID Item | 2 | 3 | 4 | 5 | 1 |

Note that the last item in the sequence has the ID Number of the first item to play next, hence a loop.

**_Parallel_**

To play at equal increments and cycle

A -> B -> C -> A

D -> E -> F -> D

|  | A | B | C | D | E | F |
| --- | --- | --- | --- | --- | --- | --- |
| ID Number | 1 | 2 | 3 | 1 | 2 | 3 |
| Device | 1001 | 1004 | 1007 | 1010 | 1013 | 1016 |
| Colour | Blue | Orange | Red | Blue | Orange | Red |
| Unit | 1 | 1 | 1 | 1 | 1 | 1 |
| Next ID Item | 2 | 3 | 1 | 0 | 0 | 0 |

Note the second parallel set does not have Next Id Item’s set as the first set will drive the changes.

**_Sequential and Parallel_**

To play at equal intervals and cycle

                C -> D

A -> B ->               -> A

                E -> F

|  | A | B | C | D | E | F |
| --- | --- | --- | --- | --- | --- | --- |
| ID Number | 1 | 2 | 3 | 4 | 3 | 4 |
| Device | 1001 | 1004 | 1007 | 1010 | 1013 | 1016 |
| Colour | Random | Random | Red | Blue | Red | Blue |
| Unit | 1 | 1 | 1 | 1 | 1 | 1 |
| Next ID Item | 2 | 3 | 4 | 1 | 0 | 0 |

To make it easier to read the INI file you can split the ATTRACT\_SETUP= line using a semicolon to indicate that there is more to come on the next line.  For example:

ATTRACT\_SETUP=1000,;

1,1001,Red,1,2,;

1,1004,Black,0,0,;

2,1004,Blue,1,1,;

2,1001,Black,0,0

In addition, the ATTACT\_SETUP= line can be made even more legible by using device names instead of device / output (DOOO) identification.  For example:

ATTRACT\_SETUP=1000,;

1,BUT\_B1,Red,1,2,;

1,BUT\_B2,Black,0,0,;

2,BUT\_B2,Blue,1,1,;

2,BUT\_B1,Black,0,0

Attract Mode can be started in one of two ways:

1.       Set the ATRACT\_START\_DELAY=X where X is the number of milliseconds of inactivity, ie ATTRACT\_START\_DELAY=60000 to auto start after 1 minute

2.       Send the ATTRACT\_MODE=1 message via any method you like, ie via DOFLinxMsg.exe

Attract Mode will stop when either:

1\. A Game is started, a menu navigation message is received, you are in debug mode and use the right-click menu.

2\. The ATTRACT\_MODE=0 message is sent to DOFLinx
