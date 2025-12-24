# Real Time Parameters and Commands

A number of commands and many parameters can be changed while DOFLinx is
running. This is made possible by sending commands via Windows
inter-process communication. A small utility DOFLinxMsg.exe is included
as one way to do this. Another way is a simple VBS script, again an
example is included.

## Real-Time Commands

These commands allow you to control DOFLinx or perform some action
outside of those setup per game to occur. Commands are sent from the
messaging utility like:

```ascii
DOFLinxMsg QUIT
```

Multiple commands can be placed on one line. They need to be separated
by a #. So for some colour and a shaker:

```ascii
DOFLinxMsg
OUTPUT_NOW_TIMER=115,1500#OUTPUT_COLOUR_NOW=109,5000,Yellow
```

The commands are:

### ATTRACT_MODE=0/1

Turn attract mode on / off.

### GAME_FLAG_FILE=PPPP\FFFF

`PPPP` is the path and FFFF is the file.  
When an emulator process is in the PROCESSES list and a GAME_FLAG_FILE
is provided, DOFLinx will only wake up if the file name provided, with
the extension ".DOFLINX" exists.  
This allows for emulators that have some tables correctly DOF'ed to be
added to the PROCESSES list. Then in the 'Launch Before' section you run
something like:

```ascii
DOFLinxMsg GAME_NAME_FILE=[TABLEPATH]\[TABLENAME]
```

If you then create a file in your tables folder with the same name as
the table you want DOFLinx to wake up for with the extension of
".DOFLINX" then it will provide rudimentary DOF with no additional
effort. Of course I do encourage people to continue to add DOF to VP and
FP tables, that's proper DOF. It is quite handy for custom tables, just
to give them a little more 'feeling'.  
This is designed for use when DOFLinx is running in Set and Forget mode.

### HOLD_ACTIVATION=0/1

Places DOFLinx on hold from activating when a configured emulator is seen running.  This was added specifically so that HOLD_ACTIVATION=1 could be sent in real-time to stop DOFLinx activating for Future Pinball when other DOF mechanisms were being used.
Place HOLD_ACTIVATION=1 in the "run before script" and HOLD_ACTIVATION=0 in the "run after script" of your front end for FP tables without DOFLinx code.  Some people have recommended stopping and restarting DOFLinx at these points, but this is much cleaner and will avoid the creation of secondary issues.

### INFO=Messgae

Places the "Message" into the DOFLinx LOG file.  Used to enable marking of the LOG file during testing and by third part applications.

### LIGHT_BUTTONS_NOW

Used to immediately turn on all of the buttons that have been defined by
BUTTONS_LIT= . This is handy when you define some RGB buttons that you
want to turn on when your front end is running but DOFLinx is not fully
active because no emulator is running. Just issue the command via
DOFLinxMsg or similar.

### KILL=XXXXX

This sends a Windows kill message to all instances of the process name
provided. It does not wait for the process to exit, it just sends the
message and continues.

```ascii
DOFLinxMsg "KILL=Pinball FX2"
```

The double quotes are used on the above since the process has a space in
its name. This sample command will send a kill message to all instances
of Pinball FX2 running at the time. You would use this as Launch After
command when exiting Pinball FX2 back to the menu if you want to ensure
that all instances are closed. I use it for those occasions when
PinballX doesn't manage to close things on exit.

### OUTPUT_NOW_TIMER=DOOO,MMMM,DOOO,MMMM, etc  

DOOO is the device / port combination, and MMMM is how long that
output will be left on in milliseconds. So, "DOFLinxMsg
OUTPUT_NOW_TIMER=1015,2000" will turn on device 1, output 15 for 2
seconds. This will occur regardless of DOFLinx being awake for a game
or not, so you can have a DOF device triggered by anything you can think
of and create a batch file for.

### OUTPUT_NOW_COLOUR=DOOO,MMMM,CCCC,DOOO,MMMM,CCCC, etc

DOOO is the Red device / port combination for the RGB device, MMMM is
how long the RGB displays colour CCCC. This will occur regardless of
DOFLinx being awake for a game or not.

### OUTPUTS_OFF

Turn off all outputs now. Handy if you have LED buttons that you turn on
at different points and want them all off when you do something like
exit your front end. This command can easily be issues vis DOFLinxMsg.

### QUIT

Shutdown DOFLinx immediately. This is much nicer than killing the
process from the operating system. It allows DOFLinx to neatly close
devices, pipes and return other resources to the operating system.

### START_DOF2DMD

Starts up DOF2DMD.  You may want this if you didn't start it when DOFLinx started, often because you've got a mixture of pinball and Mame.

### STOP_DOF2DMD

Sends the shutdown command to DOF2DMD. This is far preferable to trying
to kill the process. Likely used if you have a mixed arcade and pinball
cabinet and want to stop DOF2DMD after you've played a MAME game.

### SUP_INI=

This is the same as the command line argument, but parsed in real-time.
It allows a SUP_INI file to be processed without the need to stop and
restart DOFLinx. The parameters processed in real-time must abide by the
same rules as messages, ie BUTTONS_ON can only be changed while DOFLinx
is asleep. If DOFLinx is awake when parsed this parameter, it will be
ignored.

### SHOW_IN_TASKBAR=[0|1]

DOFLinx starts up with this set to 0 (Off)

Setting this parameter to 1 (On) will display DOFLinx in the Windows
Taskbar rather than hide it completely. Very handy when you are playing
around to get things working, etc.

### SHOW_VARIABLES

Displays all the key variables in the log file to assist with debugging.
This command takes a moment to process, so may cause a slight pause in
operation.

## Parameters That Can Be Changed Only When DOFLinx is Sleeping

Setting these parameters via the messenger will replace the setting from
the INI until you change it again or restart DOFLinx.

```ascii
BUTTONS_ON
FORCE_ACTIVE
KEY_TO_COLOUR
KEY_TO_COLOUR_TIMER
KEY_TO_COLOUR_TOGGLE
KEY_TO_OUTPUT
KEY_TO_OUTPUT_TIMER
L_FLIPPER_KEY
L_FLIPPER_OUT
MAX_FLIPPER_ON
OUTPUT_GAME_NAME
R_FLIPPER_KEY
R_FLIPPER_OUT
RGB_MIN_TIME
RGB_OUTPUT
RGB_STYLE
RGB_TRIGGER
QUIT_AFTER_PROCESS
```

## These parameters can only occur in the `DOFLinx.INI` file

```ascii
DIRECTOUTPUTCONFIG
GAME_COLOUR
PROCESSES
```

## Sending Commands To DOFLinx

Commands are sent to DOFLinx via a named pipe "DOFLINX". This means you
can use the utility provided (DOFLinxMsg), or anything else that will
write to the named pipe. A file Sample.vbs is included that shows how to
use VB Script to write directly to the named pipe. This allows a lot of
flexibility in how you send commands to DOFLinx.
