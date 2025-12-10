# The Parameters

## Device / Port

A device / port setting is used by many of the parameters. It is always
in the form `DOOO`, where `D=` the device number as assigned by DOFLinx (if
in doubt run in debug and read what it is). They start at 1 and go up
from there. So if you've only got one SainSmart, LedWiz, etc then it is
almost certainly 1. The `OOO=` is the output port number. This can be from
1 up to the maximum supported by your device, ie LedWiz its 32.

So `DOOO` as

- 1009 is device 1, output port 9,
- 2027 is device number 2, port 27,
- 1120 is device 1, output port 120.

Prior to V7.23 the format was `DOO` as opposed to the current `DOOO`. This
change was made to accommodate output ports >=100. Both `DOO` and `DOOO` formats are currently supported, but use `DOOO` as its the long term direction.

!!! note

    A LedWiz or KL25Z device can have an ID number that is
    different to the device number assigned by DOFLinx. For example, ID #8
    may initialise as device #2. So the second device that comes with a
    KL25Z has the ID of 8 and will be normally be addressed as 2001 to 2032. 
    (note this may vary based on how many devices you have and how they are
    setup). If in doubt look at the `DOFLinx.LOG` file, the device ID's and
    numbers are always in there from start-up regardless of the `DEBUG=` flag.

## Key numbers

Key numbers, represented by in the commands below, can be either
keyboard codes or Xbox keys.

### Keyboard

This is the key scan code to monitor, shown as KK. Codes can be found
[here](https://msdn.microsoft.com/en-us/library/windows/desktop/dd375731(v=vs.85).aspx).

So, for the left shift key KK is A0 (A zero), and right control key KK is
A3.

### Xbox Controller

The code to indicate an Xbox key has three parts;

1. "X" to indicate Xbox
2. `#` is the controller number from 1 to 4
3. CC the 1 or 2 digit code for the button

So "X1A" (no quotes in the INI file) is Xbox controller #1 "A" button.
Valid button codes are;

```ascii
DU -- Dpad Up
DD -- Dpad Down
DL -- Dpad Left
DR -- Dpad Right
ST -- Start
BK -- Back
LT -- Left Thumb
RT -- Right Thumb
LS -- Left Shoulder
RS -- Right Shoulder
A -- A button
B -- B button
X -- X button
Y -- Y button
```

### Joy Stick Controller

The code to indicate a joystick has three parts;

1. "J" to indicate a joystick
2. `##` is the joystick number from 1 to 16
3. CC is the DPAD button or button number

So "J01DD" (no quotes in INI file) is joystick #1 DPAD Down button, and
"J0204" is joystick #2, button number #4.

```ascii
DU -- Dpad Up
DD -- Dpad Down
DL -- Dpad Left
DR -- Dpad Right
XX -- is the joystick button number from 1 to 32 with leading zeros up to and including 9, ie 01,02, etc.
```

## `ATTRACT_MARQUEE_TIME=X`

Sets the time in milliseconds that marquees will display when Attract
Mode is running. To not display marquees when in Attract Mode set this
parameter to 0 or just leave it out of your INI file. Do not set this
parameter to less than 1000 (1 second) as you will flood the device
trying to display the marquee.

## `ATTRACT_MODE=[0/1]`

Manually turn attract mode on or off. On is 1 and off is 0, so turning attract
mode on is ATTRACT_MODE=1

## `ATTRACT_SETUP=DDD,N,DOOO,CCCC,U,X[,N,DOOO,CCCC,U,X]`

Load up an attract mode sequence, `DDD` is the unit of delay in
milliseconds between 100 and 10000 inclusive, so 1000 sets a unit of
delay of 1 second.

The next section of five items is repeated as many times as you want.

N is the item number of the current display item. You must have at least
one display item numbered 1.

DOOO is the device / output to act on.

CCCC is the colour to display. RANDOM is valid for a RGB device, ON /
OFF is used for mono devices.

U is the number of units to delay. So if U = 3, and DDD=500, then this
item will be displayed for 1500mS or 1.5 seconds. Set this to 0 if the
action is to happen immediately, ie turning off the last displayed
colour to create a chain effect.

X is the next item to display. For a loop make the last display item 1
to start from the beginning again.

## `ATTRACT_START_DELAY=X`

Set this to a value above zero to be the number of milliseconds of
inactivity until DOFLinx starts your Attract Mode activities. If you are
not using Attract Mode simply leave this parameter out of your INI file.  For most something like ATTRACT_START_DELAY=30000 is a good setting, this means after 30 seconds attract mode actions start.  If you have attract mode in your front end menu as well, then make these timeout values align.

Inactivity is defined as, not having an emulator that DOFLinx monitors,
time since the last menu system navigation message was received, time
since the right-click menu was activated.

## `AUTO_MX=[0|1}`

Default is 0, can be left out of INI file. 0=off, 1=on.

Setting this parameter on (1) will make DOFLinx use some basic default
MX displays for Pinball FX2, Pinball FX3 and Future Pinball DOFLinx
tables that are not explicitly coded to trigger MX commands. It will use
default MX displays for the five flashers, flippers, slingshots,
bumpers, strobe and beacon.

If a Pinball FX2, Pinball FX3 or Future Pinball table has been coded
with MX commands then this parameter will have no effect for that table
and the coded commands will be used.

## `BUTTON_COLOUR_CHANGE=NNNNN,CCCC[,NNNNN,CCCC]`

An option list of button name and colour pairs to change the colour of a
button set via LINK_xx buttons. This is used to change the set colour of
a button after its been defined using LINK_xx.

So if in `DOFLinx.INI` you setup the Start button to be green using
LINK_ST=101,Green then find that in a particular game you want the Start
button to be blue use BUTTON_CHANGE_COLOUR=BUT_ST,Blue

While logically not required in DOFLinx.INI, if set in the DOFLinx.INI
file buttons must be defined before they can be used. So, you must set LINK_P1= and LINK_CN= higher in your DOFLinx.INI file before using a command like above.

## `BUTTON_LIGHT_ACTION=BBB,AAA,O,N,T,C[,BBB,AAA,O,N,T,C]`

This parameter is most likely used in a game file, ie FX3 file. It links
a table trigger to a button LED action. The Button LED can be RGB or
MONO.

BBB is the button identifier, ie BUT_LF for left flipper.

AAA is the action from the table, common actions for FX3 are
LeftFlipper, RightFlipper, Slingshot_Left, Bumper_01,NudgeLeft, etc.

O defines if this action links to the ON or OFF of the action, so
LeftFlipper,ON will trigger when the left flipper activates.

N is the action to take, valid codes for button LEDs are 1,2,3,6,7,
where:

- 1 = on
- 2 = off
- 3 = on for X milliseconds
- 6 = off for X milliseconds
- 7 = show alternate colour for X milliseconds

T = time in milliseconds for the action

C = alternate colour if action #7 is used. For other actions just
ensure there is a valid colour there, ie Black

So
`BUTTON_LIGHT_ACTION=BUT_LF,LeftFlipper,ON,2,0,Black,BUT_LF,LeftFlipper,OFF,1,0,Black`
means that the left flipper button LED is turned off when the flipper
turns on, then the second action turns on the left flipper button LED
when the left flipper turns off. The effect is that the button is
normally lit, then turns off as you hold in the flipper button, then
turns back on when you release the button.

## `BUTTONS_LIT=NNNNN[,NNNNN]`

## `BUTTON_LIT_ADDED=NNNNN[,NNNNN]`

An optional list of buttons to light when DOFLinx activates due to a
PROCESS being detected. NNNNN is in the form of BUT_P1 for player 1,
etc. So lighting Player 1 and the coin button will require
BUTTONS_LIT=BUT_CN, BUT_P1

BUTTONS_LIT clears the list of buttons to light then adds the buttons
provided whereas BTTONS_LIT_ADDED adds buttons to the existing list.
Beware of your logic when adding buttons to ensure you don't keep adding
the same buttons over and over as games start / stop.

If set in the `DOFLinx.INI` file buttons must be defined before they can
be used. So you must set LINK_P1= and LINK_CN= before using the above
sample command.

## `CLOSE_DEVICES_BETWEN_ACTIVE=[0|1]`

Default is 0, can be left out of INI file, 0=off, 1=on

Don't set this to "1" (on) unless advised to do so. It will force the
closing of devices between periods of activity. A very similar mode of
operation occurs when a SainSmart device is detected since FTDI drivers
only allow for one program to control the device at any point in time,
hence DOFLinx releases the device when at all possible.

## `COLOUR_PALETTE=CCCCC,CCCCC,CCCCC, etc`

Not required, default is to use the full colour palette in the
DIRECTOUTPUTCONFIG file.

This parameter allows you to set the current colour palette used by the
RGB devices (RGB_OUTPUT). For example, if you want to restrict to greens
and yellows then

> `"COLOUR_PALETTE=Lime,Green,Yellow,Gold,Lawn_Green,Chart_Reuse,Green_Yellow,Forect_Green,Dark_Green,Yellow_Green,Light_Green"`

would do it.

This is intended for use in the STARTUP section of \*.MAME and \*.FX files to set
the colour palette to a restricted set of colours for the MAME game
being run. It is possible to use the GAME_COLOUR= command and add all
MAME games to your `DOFLinx.INI` file and have them selected by game name.
The problem with that is the list will become super long and you have to
maintain two configuration areas.

## `CLOSE_ROMS=0/1`

Not required in the INI file, default is 1

The default is for DOFLinx to close DOF ROMs between uses. This ensures
that other software can use DOF unhindered. This was the default action
until v7.16 when this option was introduced. For pinball cabinets
leaving this as default makes sense as most front ends are setup on
pinball cabinets now to use DOF for menu effects and each table uses a
different ROM.

For an arcade machine the setup can be quite different. At the time of
writing, all MAME files (300+) use the doflinx ROM for MX effects. By
not closing the ROM each time the transition between games can be sped
up by 5-10 seconds each time (the amount of time it takes DOF to load a
larger ROM). It also allows for the ROM to remain open (you can
explicitly do this in other ways) outside of when the emulator is
running. Having the ROM active allows many other effects and button
setups to continue unhindered.

If the parameter is set to leave the ROM open it will still close when
DOFLinx exits, is explicitly told to close the ROM by using the
FF_ROM="" command, or when a new ROM is requested that doesn't match the
one currently loaded.

## `DEBUG= [ 0|1|2]`

Default is 0, can be left out of INI file. 0=off, 1=on showing DOFLinx
window, 2=on not showing DOFLinx window.

Setting DEBUG on optionally makes the DOFLinx window visible and always
creates the DOFLinx.LOG file. It makes all messages visible in the
window for =1. The same messages are written to the DOFLinx.LOG file for
=1 and =2.

Other than logging and the window being visible, nothing is different
between having debug on or off. Of course, you wouldn't want debug on
during normal use as it will leave the window visible, create a very big
log file and log file writes are a slow thing to do so may cause delay /
stuttering.

DOFLinx logs the first few start-up actions every time regardless of
this parameter. The reason, well it hasn't read the flag yet, so key
start-up info is sent to the log just in case.

The DOFLinx.LOG file can be safely deleted at any time.

## `DEBUG_TCP_PORT=pppp`

No default, not required

When the DEBUG parameter is set to anything other than 0 messages are
added to DOFLinx.LOG. If the DEBUG_TCP_PORT= is set to a valid TCP port,
for example DEBUG_TCP_PORT=8001 then the messages sent to DOFLinx.LOG
are mirrored as an output on this TCP port. So once DEBUG_TCP_PORT is set, messages can be
monitored using a TCP port reading utility such as NC. A utility that
handles DOFLinx messages, TCPReader, is included with the DOFLinx
distribution.

DEBUG_TCP_PORT= can be both a `DOFLinx.INI` parameter or a command line
parameter in your shortcut to run DOFLinx. Setting this parameter via
the command line will ensure all messages from the very beginning are
logged.

With DEBUG=2 and DEBUG_TCP_PORT=8001 DOFLinx will log all messages to
both the DOFLinx.LOG file and mirrored as output on TCP port 8001. With
this configuration DOFLinx will not be displayed on your cabinet screen
and logging can be monitored in real time.

## `DELAY_BETWEEN_KEY_PRESS=`

Default is 500, can be left out of ini file.

This is the delay in milliseconds between key presses for KEY_TO_COLOUR,
KEY_TO_OUTPUT_TIMER, KEY_TO_COLOUR_TIMER commands being triggered. So at
its default, 500mS, if a key is detected as pressed again within 500mS
the trigger action will not be reinitiated.

This delay is required given that DOFLinx is not the program in focus
and hence is monitoring the keyboard as opposed to receiving keystrokes.
As such, a single quick key press can be detected multiple times without
this delay.

## `DIRECTOUTPUTCONFIG=DRV:\PATH\FFFF.INI or`

## `COLOUR_FILE= DRV:\PATH\FFFF.INI`

No default, required parameter.

This is the full file name, including path, to you
directoutputconfig.ini file, ie
"C:\directoutput\config\DirectOutputConfig.ini" , or “c:\DOFLinx\config\colours.ini” without the quotes.
The only reason a pointer to this file exits is to get the DOF colours,
so technically it could be any file so long as it has the section from
your directoutputconfig.ini file that looks like:

```ini
[Colors DOF]
White=#FFFFFFFF
Red=#FF0000FF
Lime=#00FF00FF
...
```

If you do make up a separate colour file and point to that, then you can
also add your own custom colours. Just keep them in the same format and
use any name you like less than 21 characters. You can then use those
custom colours with the likes of GAME_COLOUR or KEY_TO_RGB.

If you have multiple DOF devices, then you will have multiple
directoutputconfig files. Just find the one with a section that looks
like the above and use that (yes I know they spell colour in some
strange way, American I think?).

***IMPORTANT NOTE: This parameter must come before any colours are
assigned. To avoid any issues, the easiest thing is to make sure this is
the first parameter in the `DOFLinx.INI` file.***

## `DIRECTOUTPUTGLOBAL=DRV:\PATH\FFFF.INI`

No default, optional parameter.

Required if you intend to use addressable LEDs.

This is the full file name, including path, to your DOF R3
GlobalConfig.xml file, ie
"C:\directoutput\config\GlobalConfig_b2sServer.xml" without the
quotes.

You may not have a global config XML file for DOF, if not, do not panic,
and do not include this parameter. I ran for years without one. This
file got created on my cabinet when I added a Teensy addressable LED
controller.

## `DOF2DMD_GAME_START_HIGHSCORE=[0|1]`

Default is 0, not required in INI.

Set this to 1 (enabled) to have MAME high scores scroll up on the DMD when you start a MAME game.

## `DOF2DMD_MENU_HIGHSCORE=[0|1]`

Default is 0, not required in INI.

Set this to 1 (anabled) to have MAME high scores scroll up on the DMD as you navigate your front end.  This on is a personal prefernece, as reading the scores is not possible if you are flipping through games quickly.  So if you only want the marquee, leave this one disabled.  Always worth a play around to see what  you like.

## `DOF2DMDSHOW_NO_SCORE=[0|1]`

Default is 0, not required in INI file.

Setting this to 1 will stop the MAME score displaying on the DMD via DOF2DMD and only display animations and high scores if enabled.  THis is very useful when you have both an active DMD and the DOFLinx score screen showing as you probably don't want scores on both.  It makes enjoying the animations easier.

## `FF_DOF=CCCC,DDD[,CCCC,DDD]`

An optional parameter, most likely used in a supplementary INI file

One or a series of DOF commands to trigger events setup in ROMs vis the
DOF.

You need to have selected a DOF ROM via FF_ROM= before this command can
be used.

CCCC is a command to trigger in the DOF directoutputconfigxx.ini file
(normally a MX effects command), ie E99

`DDD` is the duration. If the duration is set in the DOF
directoutputconfigxxx.ini file then this value will be -1 to use the
predefined duration. If the event has no duration, ie an effect for MX
LEDs when a flipper is down, then the duration is a time in milliseconds
for the effect to stay on.

A duration (DDD) of 0 (zero) will turn off an effect previously turned
on, ie setting a flipper effect on for 10000mS (10 seconds) on flipper
down, but wanting the effect to stop on flipper up.

## `FF_PC A,O,DDDDD`

Mainly used in \*.MAME and possibly \*.FX files.

For initiating an action on a Pixelcade device. "A" is the action, "O"
is the output device, "DDDD" is the detail.

Valid actions:

T = Text, D`DDD` = The text to display. Remember this is in the format
used in a URL, to a space is %20

U = User command. A native Pixelcade V1 or V2 command as a URL without
the host name and no leading / . ie the native command
<http://pixelcade.local:8080/console/stream/nes> becomes
FF_PC,U,E,console/stream/nes

Valid devices

C = LCD

E = LED

## `FF_PUP_EVENT=EEE,VV[,EEE,V]`

An optional parameter, most likely used in a supplementary INI file

One or a series of PUP events to be triggered. EEE is the event name and
V the value passed with that event identifier.

## `FF_ROM=RRRRR`

An optional parameter, most likely used in a supplementary INI file

RRR is the ROM name setup within the DOF Config tool.

This is used to set the ROM for KEY_TO_ROM= commands. If the ROM name
was "doflinx" this command would look like FF_ROM=doflinx

## `FIXED_OUTPUTS= DOOO[,DOOO,DOOO]`

Replaces the old BUTTONS_ON=DOO[,DOO,DOO]

Default is no outputs activated. This can be left out of the INI file.

A comma separated list of outputs to turn on when DOFLinx "wakes up".
This is designed to turn on the LEDs within buttons that can be used
within the game being started. It can of course be used to turn on an
output for any purpose. The output remains on until DOFLinx goes back to
"sleep"

This command can use DOOO for output device and output port.

BUTTONS_ON=1016

## `FIXED_OUTPUTS_COLOUR= DOOO,CCCC[,DOOO,CCCC,DOOO,CCCC]`

Replaces the old BUTTONS_ON_COLOUR=DOO,CCCC[,DOO,CCCC,DOO,CCCC] 

Default is no outputs activated. This can be left out of the INI file.

A comma separated list of outputs and colours to turn on when DOFLinx
"wakes up". This is designed to turn on the RGB LEDs within buttons that
can be used within the game being started. It can of course be used to
turn on other RGB outputs for any purpose. The output remains on until
DOFLinx goes back to "sleep"

This command can use DOOO for output device and output port.

FIXED_OUTPUTS_COLOUR=2018,Blue

## `FP_ATTEMPT_LINK=[0|1]`

Default is 0, this parameter can be left out of the INI file. 0=off,
1=on

If one of your PROCESSES= is "Future Pinball" then with this parameter
set DOFLinx will try and establish a link with FP for tables that have
been appropriately DOF'ed. There is a section below that details how to
install the required FP script and DOF a FP table. What can I say, get
DOF'ing!

If the FP link is activated you will need to setup LINK_xx parameters,
see below.

## `FP_LINK_WAIT_TIME=`

Default is 40000, this parameter can be left out of the INI.

This sets the amount of time that DOFLinx will look for a Future Pinball
table running DOFLinx code. DOFLinx code can only be recognised once
Future Pinball has completely loaded the table and its ready to play,
that is the progress bar has finished.

Setting this value too high will cause DOFLinx to stop responding (don't
worry its still working) and potentially still be waiting once you start
playing a non-DOFLinx'ed FP table. It should only be extended if you
have a slower PC. To get an idea of what to set this to, time your
cabinet from table selection from your front end until ready to play the
slowest DOFLinx'ed table you have. Once you know how long that is, add
10 seconds just in case, times the result by 1000 and you have your
value.

So if your cabinet takes 36 seconds to load a particular DOFLinx'ed
table, then add 10 to get 46, times by 1000 to get 46000 and use
FP_LINK_WAIT_TIME=46000

If you know that your cabinet always loads FP tables within 15 seconds
to ready to play, then you could drop this value to 25000. This will
allow DOFLinx to stop looking for a table link and move onto checking
other methods of operation such as flag files for FP sooner. Probably
not worth it, but you could.

## `FORCE_ACTIVE=[0|1]`

Default is 0, this parameter can be left out of the INI file. 0=off,
1=on.

When set to 1, DOFLinx is awake the entire time its running. It negates
the need to check for a PROCESSES process.

This is a brute force way to use the utility but can provide ease of use
in Launch Before mode for emulators other than Pinball FX2. Use this
option with caution, ie get everything else going first, then think
about why you want to do this. A better way, rather than using this, is
to add the other emulators you want DOFLinx to be active for to your
PROCESSES= list and leave this parameter out of your INI or set to 0.

## `FX_LEFT_NUDGE_POINT=`

## `FX_FORWARD_NUDGE_POINT=`

## `FX_RIGHT_NUDGE_POINT=`

Not required, this parameter can be left out of the INI file, only used
with FX3 nudge.

The point at which movement of the joystick from the Pinscape
accelerometer register as a nudge in the respective direction. Note the
nudge point for LEFT will be -ve.

Nudge trigger points can be discovered and tested using the "Test Joy
Stick" function on the right click menu when in DEBUG mode.

## `FX2_FOCUS=`

Not required, defaults to 1

Enabled is 1, disabled is 0. When enabled DOFLinx shifts focus to FX2
every 0.5 seconds for 60 seconds after FX2 starts up. This is to assist
with focus sometimes doing odd things as FX starts and then we start an
active back glass or other things.

## `FX2_WINDOW_WAIT_TIME=`

Not required, defaults to 10000

This value in milliseconds can be used to manipulate the length of time
that DOFLinx scans for a valid game window after FX2 starts. The default
is a timeout of 10 seconds if a valid game window is not found. If you
are using the grid rather than a front end like PinballX then you may
wish to set the maximum higher, thus giving yourself time to select a
game from the grid.

## `FX3_FOCUS=`

Not required, defaults to 1

Enabled is 1, disabled is 0. When enabled DOFLinx shifts focus to FX3
every 0.5 seconds for 60 seconds after FX3 starts up. This is to assist
with focus sometimes doing odd things as FX starts and then we start an
active backglass or other things.

## `FX3_TRIGGER_RELEASE_DELAY`

Not required defaults to 0

This value in milliseconds determines how long a trigger from FX3 must
have changed state (ie turned on or off) until DOFLinx believes it. This
was added to allow the control of false off triggering, particularly
when holding the flipper on. A value of 50mS should be enough for most
situations without causing any noticeable delay.

## `GAME_COLOUR=NNNN,CCCCC,CCCCC,CCCCC`

Not required, default is to use the full colour palette in the
DIRECTOUTPUTCONFIG file.

This parameter allows you to limit the colour palette used by the RGB
devices (RGB_OUTPUT) for a specific game. For example, if you want to
restrict to greens and yellows for 'Plants Vs Zombies' a line like

`GAME_COLOUR=Plants VS. Zombies,Lime,Green,Yellow,Gold,Lawn_Green,Chart_Reuse,Green_Yellow,Forest_Green,Dark_Green,Yellow_Green,Light_Green`

would do it.

The Game Name is automatically detected for Pinball FX2 and Pinball FX3
when launched with the [TABLEFILE] as a parameter, ie the default mode
from PinballX. If you wish to use a separate palette via GAME_COLOUR for
other emulators you will need to force the GAME_NAME via message just
before you launch that emulator, ie "DOFLinxMsg GAME_NAME=SomeTable".

Even with a limited palette via this option, KEY_TO_RGB can still use
any colour in the full range.

## `JOY_PORT=`

Not required, this parameter can be left out of the INI file, only used
with FX3 nudge. Default = 1.

The port number of the joystick port, between 1 and 16, that the
Pinscape accelerometer maps to.

## `JOY_X_OFFSET`

## `JOY_Y_OFFSET=`

Not required, these parameters can be left out of the INI file, only
used with FX3 nudge. Default = 0.

These values are the offset from zero of the resting position of the
joystick. They can be found using the "Test Joy Stick" function from the
right-click test menu when DOFLinx is in DEBUG.

## `KEY_TO_COLOUR=KK,DOOO,CCC,KK,DOOO,CCC,KK,DOOO,CCC`

Default is no KEY_TO_COLOUR activity, this parameter can be left out of
the INI file.

A comma separated list in sets of three parameters key(KK), output
(DOOO), colour to set(CCC).

This is used to configure an RGB device to a set colour when a key is
pressed. For example, set you under cabinet RGB to display Red when a
nudge key is pressed.

## `KEY_TO_COLOUR_TIMER=KK,DOOO,CCC,MMMM[,KK,DOOO,CCC,MMMM]`

Default is no KEY_TO_COLOUR_TIMER activity, this parameter can be left
out of the INI file.

A comma separated list in sets of four parameters key (KK),
output(DOOO), colour to set (CCC) and the time in milliseconds to
display that colour (MMM).

This is used to set an RGB to a defined colour for a set time from when
a key is pressed. The RGB will revert back to colour that it was prior,
or would have been in the RGB sequence when the timer expirers. While
active any RGB_OUTPUT activity on that RGB port is suspended.

## `KEY_TO_COLOUR_TOGGLE=KK,DOOO,CCC[,KK,DOOO,CCC,KK,DOOO,CCC]`

Default is no KEY_TO_COLOUR_TOGGLE activity, this parameter can be left
out of the INI file.

A comma separated list in sets of three parameters key(KK), output
(DOOO), colour to set(CCC).

This is used to set an RGB to the defined colour while the key is
pressed and then revert back to the colour that was there prior, or
would have been in the RGB sequence, when the key is released. While
pressed any RGB_OUTPUT activity on that RGB port will be suspended.

## `KEY_TO_COMMAND=NNN,CCCC[,NNN,CCCC]`

Default is no KEY_TO_COMMAND activity, this parameter can be left out of
the INI file.

A comma separated list of button names (BUT-ST, BUT_B1, etc) and Actions
as defined in the [COMMAND] section of a FX3 or MAME file.

To make button #1 (fire) trigger a "shoot" command you would have
KEY_TO_COMMAND=BUT_B1,shoot

Then define the "shoot" action, such as;

```ini
[COMMAND]
shoot|ON|FF_DOR E216,-1
```

## `KEY_TO_OUTPUT=KK,DOOO[,KK,DOOO,KK,DOOO]`

Default is no key KEY_TO_OUTPUT activity, this parameter can be left out
of the INI file.

A comma separated list in sets of keys (KK) and the corresponding output
(DOOO) to turn on when its pressed. The output remains on while the key
is pressed.

This can be used to turn on a button LED when the button is pressed,
making the cabinet seem more interactive. It can be used to turn on a
relay when a button is pressed activating a toy or relay for other
purposes.

Keys can be defined more than once meaning that one key can be set to
turn on multiple outputs while pressed, ie light its own LED and run a
relay or toy.

## `KEY_TO_OUTPUT_TIMER=KK,DOOO,MMMM[,KK,DOOO,MMMM]`

Default is no key KEY_TO_OUTPUT_TIMER activity, this parameter can be
left out of the INI file.

A comma separated list in sets of keys (KK) and the corresponding output
(DOOO) to turn on for (MMMM) when its pressed. The output remains on
until MMMM milliseconds have expired.

This can be used to turn run a shaker, turn on a beacon for s short
period as a key is pressed.

Keys can be defined more than once meaning that one key can be set to
turn on multiple outputs for different time periods.

## `KEY_TO_ROM=KK,CCC,DDD[,KK,CCC,DDD]`

Default is no KEY_TO_ROM activity, this parameter can be left out of the
INI file.

To use this command you must have previously set a ROM with FF_ROM=

This command is designed to allow the use of addressable LEDs with
emulators other than FP, FX or VP such as MAME.

A comma separated list in sets of keys (KK) with the corresponding ROM
command (CCC) and duration (DDD) for that command.

ROM commands must be set in the respective DirectOutputConfigXX.ini
file. For MX ROM commands this is likely to be DIrectOutputConfig30.ini.
The command will look something like E120 or E410. The duration is set
in milliseconds for the command to be active. There are two special
durations, 0 to turn the command off, and -1 for the command to run
using its default time contained in the DirectOutputConfigXX.ini file.

The command is use looks like KEY_TO_ROM=A0,E130,-1,A1,110,500

## `KEY_TO_XBOX_RUMBLE= KK,C,M,SS,DDD[,KK,C,M,SS,DDD]`

No default, only required if using this functionality.

This functionality allows Xbox rumble controls to be driven from pressed
keys. By setting this parameter you can drive the selected Xbox motor on
the selected controller at any valid speed for a settable number of
milliseconds.

Load a series of keys and rumble motors, intensity and durations.

KK is the key identifier to trigger this rumble.

C is the Xbox controller from 1 to 4. You can use the GamePad test
screen in DOFLinx (available when in DEBUG and visible) to determine the
controller number.

M is the motor, so L, R or B for both.

SS is the motor speed. Valid values for an XBox motor speed are 0 to
65535 (100%)

`DDD` is the duration in milliseconds.

KEY_TO_XBOX_RUMBLE=21,1,L,50000,1000,J0103,1,R,30000,1500 will turn on
either the left rumble motor to a speed of 50000 (about 75%) for 1
second when the Page Up key is pressed, and turn on the right rumble
motor to a speed of 30000 (about 50%) for 1.5 seconds when the 3^rd^
button on joystick #1 is pressed.

## `LED_COLOUR_ORDER`

Default is all buttons, ie BUT_xx, are RGB order of LEDs.

If any of your RGB LED buttons are in a differnt order to RGB, ie ports 49 to 96 on an Ulimate I/O board, then you will need this parameter.

Simply specify the buttons that ARE NOT in RGB order and their order.

For example if you had 4 buttons being LINK_BUT_B1, LINK_BUT_B2, LINK_BUT_B3 and LINK_BUT_B4 with buttons 3 and 4 in the >port 48 range on an Ultimate I/O board, then you would add this line to your INI file.

LED_COLOUR_ORDER=BUT_B3,BGR,BUT_B4,BGR

## `L_FLIPPER_KEY=KK`

No default, required parameter.

This is the key code for the left flipper key.

## `L_FLIPPER_OUTPUT=DOOO`

No default, required parameter.

This is port to trigger for the solenoid / contactor when the left
flipper key is pressed

## `LINK_xx=DOOO,FFFFF,MMMM,III[, DOOO,FFFFF,MMMM,III,DOOO,FFFF,MMMM,III]`

No default, required for the FP and FX links.

A comma separated list of sets of output (DOOO), Default on time for the
device (FFFF), maximum on time for the device (MMMM) at intensity (III).
You can have multiple sets of these three just in case you need multiple
outputs for the one logical device.

The default on time is used when an FP or FX author triggers the device
with a default on time, quite normal for solenoid based devices. Using
the default on time allows you to set the best time for your device. The
maximum on time allows you to stop a FP author from turning on your
solenoid, etc for a super long time and not turning it off. Turning on a
solenoid / contactor for too long may cause it to overheat. It is normal
for a FP and FX author to turn on your flipper solenoid on key down and
off at key up, as such, don't set the maximum on-time for flippers to
anything too short, I'd suggest at least 10000 for 10 seconds.

Intensity can be in the range of 0 to 255 where 0 is off (ie the device
will never turn on despite being triggered), through to 255, being fully
on. In most circumstances this will be 255. Situations where it might be
a different value are for something like a shaker motor that needs to
run at 50% power, in that case set it to 128. This value will only work
properly for output devices (and boosters if applicable) that use
proportional outputs, for example LedWiz, PacLED.

For xx being as per below. ie LINK_MC=1030,75,1000,255 sets the mid
field centre solenoid / contactor to device #1, port 30 with a default
time of 75ms, a maximum on time of 1 second, with the intensity set to
255 being fully on.

```ascii
LF = Left flipper
RF = Right flipper
LS = Left slingshot
RS= Right slingshot
ML = Mid field left solenoid
MC = Mid field centre solenoid
MR = Mid field right solenoid
BL = Back left solenoid
BC = Back centre solenoid
BR = Back right solenoid
SH = Shaker motor
GR = Gear motor
KN = Knocker
FN = Fan
BE = Bell
C1 = Chime 1 (high note)
C2 = Chime 2 (mid note)
C3 = Chime 3 (low note)
```

## `LINK_xx=DOOO,MODE,TTTT,III[,DOOO,MODE,TTTT,III]`

No default, required for the FP and FX link.

A comma separated list of sets of output (DOOO), MODE being ON or FLASH,
this allows for DOFLinx to pulse the output or just turn it on. Some
physical devices will flash themselves, whereas others need the output
to be pulsed. TTTT is only relevant for MODE FLASH, it is the time for
each on then off pulse. So a TTTT of 100Ms will turn the output on for
100Ms then off for 100Ms.

Intensity can be in the range of 0 to 255 where 0 is off (ie the device
will never turn on despite being triggered), through to 255, being fully
on. In most circumstances this will be 255. Situations where it might be
a different value are for something like a beacon that needs to run at
50% power, in that case set it to 128. This value will only work
properly for output devices (and boosters if applicable) that use
proportional outputs, for example LedWiz, PacLED.

```ascii
SR = Strobe
BK = Beacon
```

LINK_SR=1005,ON,0,255 -- This will set device #1, port #5 to be turned
on when the strobe is activated

LINK_SR=1005,FLASH,150,255 -- This will turn device #1, port #5 to be
on for 150Ms then off for 150Ms over and over for the time the device is
turned on from the FP table.

## `LINK_BUT_xx=DOOO,CCCC,KK[,DOOO,CCCC,KK]`

No default, required for the FP, FX and MAME link.

A comma separated list of devices to activate when the associated button
LED illumination message is sent as an action. Multiple devices are
possible, ie you have more than one coin button and want to turn them
all on.

The button can be either a single LED or RGB colour based button. For a
single LED illuminated button set CCCC as the colour to MONO
LINK_BUT_EB=1002,MONO,4A . Otherwise the colour you want the button to
be illuminated as, LINK_BUT_EB=1002,YELLOW,4A. Where the input key is
"J" (4A)

The third parameter is the key code (KK) that this button produces when
pressed. So if the key is a number 1 then its 31, if it's a number 5
then its 35. These are the same key codes used elsewhere in DOFLinx.
Having the keycode is important if you wish to use key alias elsewhere
in DOFLinx. For example, if you wish to use the KEY_TO_COLOUR_TIMER= and
not specifiy a key code, you can specify a button name, ie BUT_P1. This
means that in all of your SUP.INI, MAME, FX3 files you can use a key
alias and not have to define the key code everyone. Much simpler for
transportable configuration files that we can all share.

For xx being as per below. ie LINK_BUT_ST=1003,Cyan,31 sets the Start
button illumination LED to device #1, port 3, makes the colour of the
RGB button LEDs cyan, and defines the Start Button input key code(ie the
key stroke when you press the start button) as "1". If the button is a
colour button then the device and port is the red LED of the RGB LED
within the illuminated button.

```ascii
BUT_ST = Start button
BUT_EB = Extra Ball button
BUT_EX = Exit button
BUT_CN = Coin button
BUT_LB = Launch Ball button
BUT_FR = Fire Button
BUT_P1 -- BUT_P4 = Player 1 to 4
BUT_PS = Pause
BUT_RE = Reset
BUT_LF = Flipper Left
BUT_RF = Flipper Right
BUT_ML = Magna Save Left
BUT_MR = Magna Save Right
BUT_B1 -- BUT_B16 = Arcade buttons
BUT_CH = Cheat
BUT_MN = Menu
BUT_J1 -- BUT_J2 = Joysticks
BUT_TB1 -- BUT_TB2 = Trackballs
BUT_L1 -- BUT_L8 = LEDs 1 to 8
```

## `LINK_xx=DOOO,CCCC,[,DOOO,CCCC]` the old way of doing it, retained for compatibility from V7.10`

No default, required for the FP, FX and MAME link.

A comma separated list of devices to activate when the associated button
LED illumination message is sent as an action. Multiple devices are
possible, ie you have more than one coin button and want to turn them
all on.

The button can be either a single LED or RGB colour based button. For a
single LED illuminated button set CCCC as the colour to MONO or just
leave it blank, LINK_EB=1002,MONO or LINK_EB=1002, . Otherwise the
colour you want the button to be illuminated as, LINK_EB=1002,YELLOW.

For xx being as per below. ie LINK_ST=1003 sets the Start button
illumination LED to device #1, port 3. If the button is a colour button
then the device and port is the red LED of the RGB LED within the
illuminated button.

```ascii
ST = Start button
EB = Extra Ball button
EX = Exit button
CN = Coin button
LB = Launch Ball button
FR = Fire Button
```

## `LINK_xxxx=DOOO[,DOOO]`

No default, required for the FP, FX and MAME link.

A comma separated list of devices to activate when the associated
flasher message is sent. Multiple devices are possible, ie you have more
than one centre flasher and want to turn them all on.

For xxxx being as per below. ie LINK_FLCN=1003 sets the red LED of the
flasher to device #1, port 3.

```ascii
FLOL = Flasher outer left
FLIL = Flasher Inner Left
FLCN = Flasher Centre
FLOR = Flasher Outer Right
FLIR = Flasher Inner Right
```

## `LOAD_SOUND=NNN,V,SPEAKER(S),File1[,FileX]`

Used in the [STARTUP] section of a game file to load SSF sounds.
Unless you are customising this will not be relevant to you.

NNN is the label used to identify this sound when using FF_SSF in a
table.FX file.

V is volume from 1 to 100%, mostly this will be 100 unless you need the
sound to be quieter relative to other SSF sounds.

Speaker(s) specifies where to output the sound. Available options are:

| Option      | 7.1 | 5.1                 | 2 speakers         |
|-------------|-----|---------------------|---------------------|
| FRONT       | Yes |                     |                     |
| SIDE        | Yes | Becomes FRONT       | Becomes FRONT       |
| REAR        | Yes |                     | Becomes FRONT       |
| CENTRE      | Yes |                     | Becomes FRONT       |
| LEFT_FRONT  | Yes |                     |                     |
| RIGHT_FRONT | Yes |                     |                     |
| LEFT_SIDE   | Yes | Becomes FRONT_LEFT  | Becomes FRONT_LEFT  |
| RIGHT_SIDE  | Yes | Becomes FRONT_RIGHT | Becomes FRONT_RIGHT |
| LEFT_REAR   | Yes |                     | Becomes FRONT_LEFT  |
| RIGHT_REAR  | Yes |                     | Becomes FRONT_RIGHT |


File1 to FileX are the WAV files to load for this sound. You at a
minimum one file. When there is more than one sound file loaded, they
will play sequentially each time this sound is called.

## `MAME_FOLDER=`

This is the path to where your Mame executable (MAME.EXE) is located, ie C:\MAME\

It is required for the checking of Mame setup and the loading of Mame game names.  If you see, "Now Playing Unknown" instead of something like "Now Playing Pacman" then an issue here is likely the problem.

A typical setup would be MAME_FOLDER=C:\MAME\

## `MAME_FOCUS=`

Not required, defaults to 1

Enabled is 1, disabled is 0. When enabled DOFLinx shifts focus to MAME
every 0.5 seconds for 60 seconds after MAME starts up. This is to assist
with focus sometimes doing odd things as MAME starts and then we start
an active back glass or other things.

## `MAME_HISCORE_FOLDER=`

This is the folder where you can find the MAME high score files. Usually
this parameter is not required unless you use a non-standard folder for
high scores. DOFLinx use in order;

1. The folder given in this parameter, if not blank
2. MAME_PATH + \hiscore\ - the default from about MAME 0.175
3. MAME_PATH +\hi\ - the original default folder

## `MAME_LINK_WAIT_TIME=`

Default=5000, can be left out of INI

This sets the maximum number of milliseconds to wait for MAME to allow a
network connection after the process starts. A couple of seconds should
really be enough.

## `MAME_PLUGIN_LOOPS=`

Windows default is 2, Linux default is 4

In the DOFLinx Mame LUA plugin the main processing loop is set to the Mame LUA 'periodic' function.  This parameter sets how many loops of the periocid function go by before DOFLinx processing takes place.  So a value of 2 means that DOFLinx plugin processing happens every second loop, a value of 5 means processing happens every 5th loop.  The value allows you to tune for slower machines running Mame, for example for a Pi4 running Batocera a value of 2 gives a balance between Mame performace and prompt score updates.  The lower the value the 'snappier' the score updates and hence animations.  The higher the value the more processing time for Mame to avoid game stuttering.

On a Pi 5 with Debian and every Windows machine I am running a value of 1 works well.  You shouldn't need to tune this variable but can.  The Pixelcade installation of DOFLinx for Pi 4 Batocera sets a value of 2 given the Pi 4's limited processing power for Mame.

## `MAME_PROCESS=`

No default, can be left out of INI.

This is the process name of the MAME emulator you are using. It must
also appear in the PROCESSES= as an activating process. The MAME process
needs to be specifically named as there are so many variants of the MAME
executable. For most people on a Windows 10 platform using the core MAME
emulator this will be MAME_PROCESS=MAME

## `MAME_SCORE_CHECK_PERIOD=`

Default is 250mS, can be left out of INI

This is the maximum delay between score checks for a MAME game.

## `MAME_TRIGGER_OUTPUT_PATH=`

No default, can be left out of INI.

If this path is set, when a MAME game runs a text-based output file will
be created. If the MAME game has outputs, then they will be in a file
with the same name as the MAME game. If there are no outputs sent, then
a blank file, again with the same name as the game, will be created in a
subdirectory of this path called "NoTriggers".

The trigger names can then be used to build XX.MAME files to trigger
actions through DOFLinx.

The trigger "pause" is suppressed from this output as it can be manually
generated in every game by pressing the MAME Pause key. It's a general
MAME output, not a specific game trigger. The Pause trigger is still
valid, just not potentially placed in every trigger file generated via
DOFLinx.

## `MAX_FLIPPER_ON=SSSS`

Default 5000, can be left out of INI file.

This is the maximum time, in milliseconds, that a flipper output can
remain on without the flipper key being repressed. This is to provide
protection for those worried about burning out solenoids / contacts if
you hold in the flipper key too long.

## `NIGHT_MODE=[1|0]`

Default is 0, can be left out of INI file.

This setting is designed to be used in real-time, ideally via a message
sent to DOFLinx. Setting this on (1) will disable noise making devices
(flippers, solenoids, knocker) and let you play without disturbing the
rest of the household.

When a FP table with a link is active it will disable the device
mechanical feedback and re-enable the table sounds. Night Mode can be
turned on / off at any time and will notify FP in real-time.

## `NUDGE_CHECK_BASIC_KEYBOARD=`

Not required, this parameter can be left out of the INI, the default is
0 or disabled.

Setting this to 1, on, will enable checking of the Pinscape nudge
checking when DOFLinx is operating in its most basic mode checking
keyboard keys for a process that triggers it in the PROCESSES=
parameter. This allows other emulators to use the joystick nudge
checking.

## `NUDGE_LEFT_KEY=`

## `NUDGE_FORWARD_KEY=`

## `NUDGE_RIGHT_KEY=`

Not required, this parameter can be left out of the INI file, only used
with FX3 nudge.

These are the keys setup within FX3 to trigger keyboard nudge. The
default keys are L-Ctrl, R-Ctrl and Space. Sadly, the L-Ctrl and R-Ctrl
keys do not work, as such, the keys will need to be changed in FX3 to
something else. I suggest "L" and "R". While in the form KK, these are
only keyboard keys, they cannot be Xbox buttons.

## `NUDGE_LEFT_INPUT=`

## `NUDGE_FORWARD_INPUT=`

## `NUDGE_RIGHT_INPUT=`

Not required, this parameter can be left out of the INI file, only used
with FX3 nudge.

If like me, you change the keys in FX3 to trigger nudge (as per
NUDGE_???_KEY= above) but don't want to reprogram your nudge buttons
away from L-Ctrl and R-Ctrl because you use them for other inputs, ie
VPX or PinballX, then setup these parameters and DOFLinx will parse the
Ctrl key presses to the new FX3 nudge keys. These are in the format of
KK, so can e keyboard keys or Xbox buttons.

## `NUDGE_WAIT=`

Not required, this parameter can be left out of the INI file, default is
1500

This is the minimum delay between nudge events from the Pinscape. It
allows you to stop getting multiple nudge events from the single nudge.
The minimum this can be set to is 1500Ms (1.5 seconds)

Normally you should not need to play with this, but hey why not give it
a try.

## `OUTPUT_GAME_NAME=[0|1]`

Default is 0, can be left out of INI file. 0=off, 1=on.

When turned on it will force the Game Name to be written to the debug
log regardless of the DEBUG setting. This is handy when you are setting
up GAME_COLOUR palettes and want the game name without a full
DOFLinx.LOG being created.

## `PATH_B2S_SERVER=`

The path where your B2SServerEXE.exe is located. The default is C:\VP  

This value can be set via real-time command or in an INI file.

This parameter is required if you plan to use B2S back glass files with
Pinball FX2 or Pinball FX3. A common place to find this file would be
C:\VP\Tables\ if you have a nice neat VP setup.

## `PATH_DOF2DMD=`

The path to where DOF2DMD has been installed. Ie PATH_DOF2DMD=C:\DMD\

If you don't have DOF2DMD then don't add this parameter to your INI file.

If the path is set and dof2dmd is not running, then DOFLinx will attempt to run dof2dmd in the background for you.

## `PATH_FX2=`

The path to locate FX2 files in. This value can be set via a real-time
command or in an INI file.

The path can be absolute, ie C:\DOFLinx\FX2\ or relative from the
location where the program executes from, ie if the program is in
C:\DirectOutput and you have a DOFLinx_FX2 folder below that the value
can be DOFLinx_FX2  

Not setting a value or setting it to nothing means the FX2 files are to
be located in the same folder as DOFLinx.exe

## `PATH_FX3=`

Same as above but for FX3 files.

Usually C:\DOFLinx\FX3\

## `PATH_FX=`

Same as above but for FX files (Pinball FX).

Usually C:\DOFLinx\FX\

## `PATH_FX2_B2S=`

The path to the directb2s files for FX2 games. This value can be set via
real-time command or in the INI file.

The path can be absolute, ie C:\DOFLinx\FX2_B2S\ or relative from the
location where the program executes from, ie if the program is in
C:\DirectOutput and you have a DOFLinx_FX2_B2S folder below that the
value can be DOFLinx_FX2_B2S  

The value must end with a backslash   

Not setting a value or setting it to nothing means the B2S files are to
be located in the same folder as DOFLinx.exe

## `PATH_FX3_B2S=`

Same as above but for FX3 B2S files. If you already have PATH_FX2_B2S=
setup, you can point this to the same folder. About 90% of B2S files are
the same between FX2 and FX3 and it saves having two copies.

## `PATH_FX_B2S=`

Same as above but for FX B2S files (Pinball FX).

## `PATH_HI2TXT=`

The path to where Hi2Txt has been installed. Hi2Txt is used to get high
scores from MAME.

## `PATH_INI=`

The path to locate INI files in. This value can be set as a command line
argument, via a real-time command or in an INI file. Obviously if you
wish to locate your `DOFLinx.INI` in this path then you must use the
command line to set this value.

The path can be absolute, ie C:\DOFLinx\INI\ or relative from the
location where the program executes from, ie if the program is in
C:\DirectOutput and you have a DOFLinx_INI folder below that the value
can be DOFLinx_INI  

Not setting a value or setting it to nothing means the INI files are to
be located in the same folder as DOFLinx.exe

## `PATH_LINX=`

As above, the path for LINX files used for the more generic emulator link. Currently used for Pinball M and Infected Mushroom Pinball

## `PATH_LINX_B2S=`

As above, path for LINX based B2S files.  Place your Pinball M active back glasses here.

## `PATH_MAME=`

The path to locate MAME files in. This value can be set via a real-time
command or in an INI file.

The path can be absolute, ie C:\DOFLinx\MAME\ or relative from the
location where the program executes from, ie if the program is in
C:\DOFLinx and you have a DOFLinx_MAME folder below that the value
can be DOFLinx_MAME\ . Absolute path names such as
C:\DOFLinx\MAME\ are best.

The value must end with a backslash   

Not setting a value or setting it to nothing means the MAME files are to
be located in the same folder as DOFLinx.exe

## `PATH_PIXELCADE=`

The path to where Pixelcade has been installed. Ie
PATH_PIXELCADE=C:\Pixelacde  

If you don't have Pixelcade then don't add this parameter to your INI
file.

If the path is set and pixelweb is not running, then DOFLinx will
attempt to run pixelweb in the background for you.

## `PINCONTROL2_UNIVERSE=`

***DEPRECIATED -- Now able to pick this up from your cabinet.xml from
V6.50***

No default, can be left out on INI

If you have a PinControl2 board you will need to set this parameter and
PINCONTROL_BROADCST. The normal setting required will be
PINCONTROL2_UNIVERSE=0, if you need anything else you will have been
given that parameter value with your board.

## `PINCONTROL2_BROADCAST=`

***DEPRECIATED -- Now able to pick this up from your cabinet.xml from
V6.50***

No default, can be left out on INI

If you have a PinControl2 board you will need to set this parameter and
PINCONTROL_UNIVERSE. The normal setting required will be
PINCONTROL2_BROADCAST=192.168.178.50

, if you need anything else you will have been given that parameter
value with your board.

## `PIXELCADE_GAME_START_HIGHSCORE=1/0`

Default 0, can be left out of the INI

Set this to 1 DOFLinx will display MAME high scores when a game starts.

## PIXELCADE_LCD_USENETWORK_ADDRESS=[1/0]

Default is 1 (true)

set this to true to force use of the Pixelcade LCD IP network address as opposed to the USB IP address.

## `PIXELCADE_MENU_HIGHSCORE=1/0`

Default 1, can be left out of INI

When set to 1 then DOFLinx will display MAME game high scores on the
Pixelcade device as you move through your selections on your front end
menu. Currently front end menu systems supported are -- Pinup Popper.  
When 0 / false then only the appropriate marquee will be displayed with
no high scores.

## `PIXELCADE_REPLACE_LED_MARQUEE_AFTER_ANIMATION=1/0`

Default 0, can be left out of INI

Possibly the longest parameter \... although I'm sure I can beat it
later!

1 = yes / true, 0 = false / no

Determines if DOFLinx will redisplay the MAME game marquee after an
animation command in the game.MAME file is executed. So if an explosion
is shown when you hit a ship, do you want the marquee for the game to be
displayed on the LED screen after its finished.  
Having this on makes sense when you only have an LED screen. If you have
an LCD and LED then the marquee will already be on the LCD, so it makes
sense to keep the LED for animations only and not duplicate the marquee.
But then, here we go, its your choice!

## `PIXELCADE_SCORE_DISPLAYS=DEFAULT,LCD,LCD_MATRIX,LCD_7SEG,LED,LED_7SEG,LED_LEDSTRIP,LED_MATRIX`

Default is DEFAULT and this can be left out of your INI.

The default will enable LCD and LED meaning that if you have a score display on either or both of these Pixelcade devices then the score will be displayed using the default Pixelcade order of device precedence. So using DEFAULT or LCD,LED is the same as leaving this parameter out alltogether or having a blank parameter, ie PIXELCADE_SCORE_DISPLAYS=

Adding any or all of the other options will force a score display to those devicess.  Doing this allows you to customise precisely where scores are displayed.

If you want to see the score on the Dot Matrix connected to your Pixelcade LCD screen and on the Seven Segement display connected to your LED panel then you would set PIXELCADE_SCORE_DISPLAYS=LCD_MATRIX,LED_7SEG

## `PROCESSES=PPPP,PPPP,PPPP`

Default Pinball FX2, can be left out of INI file.

This is the name(s) of the process(es) that will "wake up" DOFLinx. By
default, it is 'Pinball FX2' only. When the process goes away again
DOFLinx goes back into its idle state.

The process names are as they can be seen in Task Manager. For example

> PROCESSES=Pinball FX2,Pinball FX3,Future Pinball,PinballFX-Win64-Shipping

## `PROCESS_ADD=`

No default, can be left out of INI file.

A comma separated list of process names to add to the PROCESS= set while
DOFLinx is running.

## `PROCESS_DEL=`

No default, can be left out of INI file.

A comma separated list of process names to remove from the PROCESS= set
while DOFLinx is running.

## `PROCESSES_LINX=`

A comma separated list of processes to activte the LINX based emulators such as Pinball M and Infected Mushroom Pinball.  These process names do not need to be duplicated in the PROCESSES= line.
If you are editing your DOFLinx.INI file manually make sure this line is in your INI after the PROCESSES= line.

## `PLUNGER_AXIS=A`

No default, can be left out of INI file.

"A" is the axis to read the plunger position from. At present the only
valid option is "Z" (no quotes) indicating the Z-axis for a plunger.
This is used to allow a plunger to trigger ball launch in FX3.

## `PLUNGER_JOYSTICK_NUMBER=XX`

No default, can be left out of INI file.

Valid values are 1 to 16 being the joystick ID # that the plunger
device is connected to.

## `PLUNGER_KEY=KK`

No default, can be left out of INI file.

The key number to send to FX3 when the plunger passes the
PLUNGER_PULL_POINT and then returns back past the PLUNGER_RELEASE_POINT.

To send the default launch key of FX3 being <ENTER> this line should
read PLUNGER_KEY=0D

## `PLUNGER_PULL_POINT=NNNNN`

No default, can be left out of INI file.

If PLUNGER_AXIS and PLUNGER_JOYSTICK_PORT are set, this is to point at
which the plunger being pulled is registered. Values can be determined
from the Pinscape setup tool or DOFLinx in DEBUG mode using the Test
Joystick function.

If your plunger has a Z-Axis range of 0 at rest through to 65000 at full
pull, then PLUNGER PULL_POINT could be 40000 and
PLUNGER_RELEASE_POINT=20000. You will need to test to determine the best
values. There should be a reasonable gap between PLUNGER_PULL_POINT and
PLUNGER_RELEASE_POINT to avoid accidental triggering.

## `PLUNGER_RELEASE_POINT=NNNNN`

No default, can be left out of INI file.

See PLUNGER_PULL_POINT

## `PROCESS_TO_ACTIVE_TIME=MMMM`

Default is 2000ms, can be left out of INI file.

This allows you to customise the time between the detection of a process
to wake up DOFLInx as defined in PROCESSES= , and when DOFLinx 'wakes
up'. The reason to tweak this is to allow for odd start-up processes
whereby the PROCESSES process is detected quickly but configuration
messages are taking a while to be sent through by something like the
DOFLinxMsg utility as a 'Launch Before' process. If in doubt, leave it
alone.

## `QUIT_AFTER_PROCESS=[0|1]`

Default is 0, can be left out of INI file. 0=off, 1=on.

When turned on, DOFLinx will shutdown after the monitored process that
woke it disappears. This can be used in Launch Before mode to stop
DOFLinx without needing to be killed by batch file, etc.

So if you are monitoring the default process of 'Pinball FX2' and start
up DOFLinx via a Launch Before option, with the parameter set to 1,
DOFLinx will shutdown when Pinball FX2 stops and you return to your
menu, ie PinballX.

!!! Note
    This mode of opereration is not recommended

## `R_FLIPPER_KEY=KK`

See L_FLIPPER_KEY and just think right.

## `R_FLIPPER_OUTPUT=DOOO`

See L_FLIPPER_OUTPUT and just think right.

## `RGB_MIN_TIME=SSSS`

Default is 5000, this parameter can be left out of the INI file.

The time, in milliseconds, used by the RGB_STYLE to change RGB_OUTPUT.

## `RGB_OUTPUT=DOOO,DOOO,DOOO`

No default, leave if out or blank if you don't want or have RGB devices.

A comma separated list of DOOO for the RGB devices you want to cycle
through colours. The DOOO is the port of the red device, the Green is
assumed to be DOOO + 1 and the Blue assumed to be DOOO + 2.

The RGB_OUTPUT sets RGB colours from the entire, or GAME_COLOUR palette,
according to RGB_STYLE, RGB_TRIGGER and RGB_MIN_TIME parameters.

## `RGB_STYLE=[RAINBOW|RAINBOW_ALTERNATE|RANDOM|CCCC]`

Default is RAINBOW, this can be left out of the INI file.

This parameter determines how colours are selected for the RGB_OUTPUT
devices.

RAINBOW cycles through the current colour palette list from beginning to
end. So that could be the default entire colour palette, or the sub-set
defined by GAME_COLOUR.

RAINBOW_ALTERNATE cycles through the current colour palette list from
beginning to end. So that could be the default entire colour palette, or
the sub-set defined by GAME_COLOUR. Uses the next two colours from the
palette and applies then alternately to each RGB device in the list. If
the two colours were red and blue, and you had four RGB devices then
device #1 and #3 would be red and #2 and #4 would be blue.

RANDOM, as the name implies, picks the next colour at random from the
current colour palette.

RANDOM_DIFF, picks a new random colour from the current colour palette
that is different for each RGB device provided.

RAINBOW_DIFF, picks a new random colour from the entire colour range
that is different for each RGB device provided.

CCCC, is any valid colour name in the entire colour palette. This has
the effect of setting the RGB output to a fixed colour. Note you must
set the RGB_TRIGGER to FIXED

## `RGB_TRIGGER=[FLIPPER|TIME|FIXED]`

Default is TIME, this parameter can be left out of the INI file.

This parameter is not relevant if RGB_STYLE has been set to CCCC being a
fixed colour as there is nothing to change.

When set to FLIPPER, at each flipper press, not more often than
RGB_MIN_TIME, the RGB_OUTPUT colour will change using the RGB_STYLE.

When set to TIME, the RGB_OUPUT colour will change ever RGB_MIN_TIME.

When using a fixed colour via RGB_STYLE=CCCC set this parameter to
FIXED.

## `SCORE_SCREEN=`

Default is 0, off

Seet to 1 to enable the displaying of the building MAME score screen.
This screen can then be dragged to any monitor or position.

Note, this is not related to displaying scores on Pixelcade devices.

## `SETTING=IIII,DOOO,LLLL,DDD,S[,DOOO,PPP]`

No default, only required if using the settings functionality.

This item is repeated for each setting required. Settings are displayed
in the order they appear in the INI file.

IIII is a unique identifier for the setting. This is used internally to
differentiate each setting, as well as for the suffix in the registry if
the setting is saved. It can be any length, but probably best to keep it
below 10 characters. There is a special unique identifier being "NIGHT",
this does not require a DOOO setting, it allows the toggling of
DOFLinx's night mode setting

DOOO is the device port to turn on / off for this setting. In the case
of the special identifier "NIGHT", just leave the field empty

`LLLLL`is the label that appears on screen for this setting. For example,
"Under cabinet lighting".

`DDD` is the default setting, either "ON" or "Off" without the quotes

S is either "Y" or "N" without the quotes indicating if this setting
should be saved upon exit and reloaded in the same state next time the
system starts.

If an optional second output device / port and pulse width (`PPP`) is
provided, then this setting is treated as a latch based setting. That
means the first port will pulse to turn the setting device on, and the
second port will pulse to turn the setting device off. This sort of
setting device requires a latching relay, so a relay with some
additional circuitry. You use a latching relay circuit when you need
your setting device's status to survive the DOF framework outputs being
reset due to different programs taking control.

A latching relay circuit is ideal when you have a DOFLinx settings item
turning the power on / off to internal devices. In my case the power
supply to my addressable LED array. The power being on / off needs to
persist programs starting stopping that may impede the use of a simple
single output being turned on to control the power relay.

The pulse (`PPP`) for setting / unsetting the latch is in milliseconds. It
shouldn't really be larger than 100, that is 1/10^th^ of a second.

## `SETTING_ACTIVATE=KK[,KK,KK]`

No default, only required if using the settings functionality.

One or more key codes used to activate the settings pop up menu. If more
than one key code is used then all keys must be pressed at the same time
to achieve activation. For example SETTING_ACTIVATE=A0,A1,A2,A3 would
require four keys to be held down simultaneously being left shift, right
shift, left control, right control. For many this would be the pressing
of both flipper and magna save buttons.

## `SETTING_CHANGE=KK`

No default, only required if using the settings functionality.

The key code identifying the key used to change setting values.

## `SETTING_DOWN=KK`

No default, only required if using the settings functionality.

The key code identifying the key used to move down in the settings menu.
Ie SETTING_DOWN=A1 would set the right shift, often the right flipper,
for this task.

## `SETTING_EXIT=KK`

No default, only required if using the settings functionality.

The key code identifying the key used to exit the settings menu.

## `SETTING_UP=KK`

No default, only required if using the settings functionality.

The key code identifying the key used to move up in the settings menu.
Ie SETTING_UP=A0 would set the left shift, often the left flipper, for
this task,

## `SETTING_MESSAGE=TTTTTTT`

No default, only required if using the settings functionality.

## `SKIP_RGB_FLASHER_TEST=[0|1]`

The default is 0, meaning the test is performed.

Normally you would not add or use this parameter. It is for a specific
override of the test that removes flashers (LINK_FLxx) from the
RGB_OUTPUT list. In some cases you can define devices output devices as
both RGB and flashers. Normally you want DOFLinx to make a device only
operate as either a RGB device or flasher device. So don't use it unless
you really know why.

## `SSF_ENABLED=[0|1]`

The default is 0 and this can be left out of your INI file

For enabling / disabling SSF, 0 is disabled, 1 is enabled.

## `SSF_DEVICE=N`

The default is -1 and this can be left out of your INI file. This is the
number of the output sound device according to Windows. Using -1 gives
you the default Windows output sound device. Otherwise use a valid
output device number, this is usually done if you are not using the
default output sound device. With DEBUG= set to 1 or 2, DOFLinx will
display your output sound devices, their number and what is the default
device.

## `SSF_SOUND_PATH=`

This is the path to the sounds used by the LOAD_SOUND= command in your
table.FX file. The DOFLinx installation zip places the sounds setup by
default in the \sounds folder.

## `TRIGGER_DEBOUNCE_TIME=`

The default is 100Ms. Only required if you want to set it away from the
default.

This parameter sets the minimum time between triggers. This was added
for FX3 where some very quick retriggering for things like flippers was
being generated. It stops the same trigger from causing an action within
the time set.

## `XBOX_RUMBLE= XX,C,M,SS,DDD[,XX,C,M,SS,DDD]`

No default, only required if using this functionality.

This functionality allows Xbox rumble controls to be driven from linked
toy events in FP and FX2/3. By setting this parameter you can drive the
selected Xbox motor on the selected controller at any valid speed for a
settable number of milliseconds.

XX is the toy trigger event, valid events are;

```ascii
LF = Left flipper
RF = Right flipper
LS = Left slingshot
RS= Right slingshot
ML = Mid field left solenoid
MC = Mid field centre solenoid
MR = Mid field right solenoid
BL = Back left solenoid
BC = Back centre solenoid
BR = Back right solenoid
SH = Shaker motor
GR = Gear motor
KN = Knocker
FN = Fan
```

C is the Xbox controller from 1 to 4. You can use the GamePad test
screen in DOFLinx (available when in DEBUG and visible) to determine the
controller number.

M is the motor, so L, R or B for both.

SS is the motor speed. Valid values for an XBox motor speed are 0 to
65535 (100%)

`DDD` is the duration in milliseconds.

XBOX_RUMBLE=LS,1,L,50000,1000,RS,1,R,50000,1000 will turn on either the
left or right rumble motor to a speed of 50000 (about 75%) for 1 second
when the left or right slingshots are hit.

Note: For the various 'colour' based commands the special colour name
"Random" can be used. This will cause a random colour from the current
colour palette to be displayed. The current colour palette is by default
all colours unless a set of GAME_COLOUR= has been set up, then that is
the current colour palette.
