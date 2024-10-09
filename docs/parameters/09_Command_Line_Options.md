# Command Line Options

There are a few optional command line options for DOFLinx. They are:

## DISABLEDOF=YES

This parameter set to YES will disable the search and startup of DOF
based controllers. It is used for people running DOFLinx on desktop and
VR configurations where there are no DOF based toys being run but you do
want B2S backglasses with FX2/3 or you want Xbox rumble output.

## DOF2DMD=NO

Used to stop the automatic startup of DOF2DMD when DOFLinx starts. Use
this if you have a cabinet and front end that runs both pinball using
your DMD and MAME all together. Not required on a MAME or pinball only
cabinet. You shouldn't run this command line argument until after you
are sure everything is setup correctly as some of the more informative
DOF2DMD startup messages from DOFLinx will be suppressed.

## DUDESCAB=NO

Add this parameter if you do not want DOFLinx to search for a Dude's Cab
controller.

## FTDI=NO

Add this parameter if you do not want DOFLinx to search for any FTDI
(SainSmart devices). This parameter is intended for those people with
other non-Pinball based FTDI chip based devices connected, ie
Fan-o-Matic Pro. If DOFLinx detects a FTDI controlled device that is not
a SainSmart relay board, because FTDI devices can only have one program
controlling them, there is a remote risk of conflict, hence the ability
to switch this test off.

## GAME_NAME=

This option is technically valid in both modes, but realistically only
useful in Launch Before mode. For Set and Forget mode you can message a
GAME_NAME to the running process.

Adding this parameter to the command line allows you to force the Game
Name for the GAME_COLOUR parameter palette selections. Read about the
GAME_COLOUR parameter below.

## PATH_DOF=
If for some reason you need to force the path to where the appropriate DIrectOutput.dll resides.  In normal operation this should not be required.

## PATH_INI=

The path to locate INI files in. This value can be set as a command line
argument, via a real-time command or in an INI file. Obviously if you
wish to locate your `DOFLinx.INI` in this path then you must use the
command line to set this value.

The path can be absolute, ie `C:\DOFLinx\INI\` or relative from the
location where the program executes from, ie if the program is in
`C:\DirectOutput` and you have a DOFLinx_INI folder below that the value
can be `DOFLinx_INI\`

## PINONE=NO

Add this parameter if you do not want DOFLinx to search for a PinOne
controller.

## PINSCAPE=NO

Add this parameter if you do not want DOFLinx to search for a Pinscape
controller (native Pinscape, not a Pinscape in LEDWiz emulation mode).
This parameter is really intended for people running DOFLinx from V5.0
onward who have the DOF Framework branch that does not have Pinscape
support. Regardless of having a Pinscape device or not, if you do not
have a DOF Framework version that supports Pinscape you need this
setting or you will get a .NET framework error.

## SUP_INI=

This option is valid in both modes, but realistically only useful in
Launch Before mode as command line option. For Set and Forget mode you
can message a SUP_INI file to the running process.

To enable game specific settings you can place common parameters (see
below for parameter descriptions) in the default `DOFLinx.INI` file and
other in XXX.INI. You then supply DOFLinx with that supplementary INI
file via this command line option. Ie DOFLinx SUP_INI=MyGame where
MyGame.ini contains your game specific key and colour information.

If you want to keep things neat and tidy you can create a sub-folder
under your DOF folder for INI files. If you do this just add a path name
to the SUP_INI= parameter. If your folder is MyINIs, then
SUP_INI="MyINIs\TheINI". The path is relative to where you start the
program from, being the DOF folder.

!!! note

    Don't add the ".ini" to the end of the name.
