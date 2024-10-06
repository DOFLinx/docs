# Pinball FX2 Memory Triggers -- Full Force Feedback

If a specific FX2 table has been memory mapped, then full force feedback
is possible. DOFLinx looks for a trigger configuration file named
"GameName.FX2" first, then "default.fx2", if neither are found then
basic keyboard monitoring will be used.

DOFLinx will first look in the PATH_FX2= path if configured, if not
found there it will look in the DOFLinx.exe folder. It is recommended
that you do set the PATH_FX2= parameter to a separate folder just for
FX2 trigger files to keep things neat and tidy.

The trigger configuration file will look a bit like this:

```ini
##################
#
# Bob's Burgers Pinball
# DOFLinx force feedback configuration file v6
#
##################
[STARTUP]
FF_ROM=fx2_bb
[MEMORY TRIGGERS - CORE]
GAMEMODE=8879B4,FF
SCOREMODE=887919,FF
ANIMEMODE=88791B,FF
LAUNCHMODE=88791A,FF
LAUNCHBALL=883CF4,FF
LeftFlipper=88781C,FF
RightFlipper=88781C,FF00
Nudge=88B8F4,FF000000
[MEMORY TRIGGERS - TABLE BASED]
Left_Slingshot=882FC0,FF,2E4,0C,20,08
Right_Slingshot=882FC0,FF,2E4,14,20,08
Bumper1=882FC0,FF,2E4,00,20,08
Bumper2=882FC0,FF,2E4,04,20,08
Bumper3=882FC0,FF,2E4,08,20,08
Bumper1_Flasher=882FC0,FF,2B0,0C,00,04,A4
Bumper2_Flasher=882FC0,FF,2B0,0C,04,04,A4
Bumper3_Flasher=882FC0,FF,2B0,0C,08,04,A4
Left_SlingShot_Flasher=882FC0,FF,2B0,0C,0C,04,A4
Right_SlingShot_Flasher=882FC0,FF,2B0,0C,14,04,A4
Crane_Flasher=882FC0,FF,2B0,0C,1C,04,A4
FerrisWheel_Flasher1=882FC0,FF,2B0,0C,20,04,A4
FerrisWheel_Flasher2=882FC0,FF,2B0,0C,24,04,A4
Lamp1_Flasher=882FC0,FF,2B0,0C,28,04,A4
Lamp2_Flasher=882FC0,FF,2B0,0C,2C,04,A4
Lamp3_Flasher=882FC0,FF,2B0,0C,30,04,A4
Lamp4_Flasher=882FC0,FF,2B0,0C,34,04,A4
SinkHole_Flasher=882FC0,FF,2B0,0C,38,04,A4
WonderWharf_Left_Flasher=882FC0,FF,2B0,0C,3C,04,A4
WonderWharf_Right_Flasher=882FC0,FF,2B0,0C,40,04,A4
[COMMANDS]
GAMEMODE|ON|FF_Colour Black,RGB_DF,0|FF_Flasher
DV_FLOL,FL_FD,6,750,50,Orange|FF_Flasher
DV_FLOR,FL_FD,6,750,50,Orange|FF_Flasher
DV_FLIL,FL_FD,6,750,50,Yellow|FF_Flasher
DV_FLIR,FL_FD,6,750,50,Yellow|FF_Flasher
DV_FLCN,FL_FD,6,750,50,Orange|FF_B2S B2SStartAnimation Sign
LAUNCHMODE|ON|FF_Button BUT_LB,BA_FL,10000,500|FF_DOF E310,5000
LAUNCHMODE|OFF|FF_Button BUT_LB,BA_OFF,0,0
LAUNCHBALL|OFF|FF_Dev DV_MR,-1|FF_B2S B2SStartAnimation
Sign|FF_DOF E310,0
SCOREMODE|ON|FF_Flasher DV_FLOL,FL_OFF,1,1,100,Random|FF_Flasher
DV_FLIL,FL_OFF,1,1,100,Random|FF_Flasher
DV_FLCN,FL_OFF,1,1,100,Random|FF_Flasher
DV_FLIR,FL_OFF,1,1,100,Random|FF_Flasher
DV_FLOR,FL_OFF,1,1,100,Random|FF_Dev DV_SR,0|FF_Dev DV_BK,0|FF_B2S
B2SStopAllAnimations|FF_DOF E415,-1
LeftFlipper|ON|FF_Dev DV_LF,10000
LeftFlipper|OFF|FF_Dev DV_LF,0
RightFlipper|ON|FF_Dev DV_RF,10000
RightFlipper|OFF|FF_Dev DV_RF,0
Nudge|ON|FF_Dev DV_SH,10000|FF_Colour Red,RGB_TT,1500|FF_Flasher
DV_FLCN,FL_ON,1,1,100,Red|FF_Flasher
DV_FLOL,FL_ON,1,1,100,Red|FF_Flasher
DV_FLOR,FL_ON,1,1,100,Red|FF_B2S B2SStartAnimation,BurgerBall|FF_DOF E402,-1
Nudge|OFF|FF_Dev DV_SH,250|FF_Flasher
DV_FLCN,FL_OFF,1,1,100,Red|FF_Flasher
DV_FLOL,FL_OFF,1,1,100,Red|FF_Flasher DV_FLOR,FL_OFF,1,1,100,Red
Left_Slingshot|ON|FF_Dev DV_LS,-1|FF_DOF E110,-1
Right_Slingshot|ON|FF_Dev DV_RS,-1|FF_DOF E111,-1
Bumper1|ON|FF_Dev DV_BL,-1|FF_DOF E120,-1
Bumper2|ON|FF_Dev DV_BC,-1|FF_DOF E121,-1
Bumper3|ON|FF_Dev DV_BR,-1|FF_DOF E122,-1
Bumper1_Flasher|ON|FF_Flasher DV_FLIL,FL_ON,1,1,100,Random|FF_B2S
B2SStartAnimation,LouiseFace
Bumper1_Flasher|OFF|FF_Flasher DV_FLIL,FL_OFF,1,1,100,Random
Bumper2_Flasher|ON|FF_Flasher DV_FLCN,FL_ON,1,1,100,Random|FF_B2S
B2SStartAnimation,GeneFace
Bumper2_Flasher|OFF|FF_Flasher DV_FLCN,FL_OFF,1,1,100,Random
Bumper3_Flasher|ON|FF_Flasher DV_FLIR,FL_ON,1,1,100,Random|FF_B2S
B2SStartAnimation,TinaFace
Bumper3_Flasher|OFF|FF_Flasher DV_FLIR,FL_OFF,1,1,100,Random
Left_SlingShot_Flasher|ON|FF_Colour Yellow,RGB_TT,125|FF_B2S
B2SStartAnimation,BobFace
Right_SlingShot_Flasher|ON|FF_Colour Yellow,RGB_TT,125|FF_B2S
B2SStartAnimation,LindaFace
Crane_Flasher|ON|FF_Flasher DV_FLOR,FL_ON,1,1,100,Yellow|FF_B2S
B2SStartAnimation,Windows|FF_DOF E413,-1
Crane_Flasher|OFF|FF_Flasher DV_FLOR,FL_OFF,1,1,100,Yellow
FerrisWheel_Flasher1|ON|FF_Flasher
DV_FLOL,FL_ON,1,1,100,Silver|FF_B2S B2SStartAnimation,Windows|FF_DOF
E410,-1
FerrisWheel_Flasher1|OFF|FF_Flasher DV_FLOL,FL_OFF,1,1,100,Silver
FerrisWheel_Flasher2|ON|FF_Flasher
DV_FLOL,FL_ON,1,1,100,Silver|FF_B2S
B2SStartAnimationReverse,Windows|FF_DOF E412,-1
FerrisWheel_Flasher2|OFF|FF_Flasher DV_FLOL,FL_OFF,1,1,100,Silver
Lamp1_Flasher|ON|FF_Dev DV_SR,2000|FF_B2S B2SSetData 51,1|FF_B2S
B2SSetData 58,1|FF_DOF E140,-1
Lamp2_Flasher|ON|FF_Dev DV_SR,2000|FF_B2S B2SSetData 52,1|FF_B2S
B2SSetData 57,1|FF_DOF E141,-1
Lamp3_Flasher|ON|FF_Dev DV_SR,2000|FF_B2S B2SSetData 53,1|FF_B2S
B2SSetData 56,1|FF_DOF E301,-1
Lamp4_Flasher|ON|FF_Dev DV_SR,2000|FF_B2S B2SSetData 54,1|FF_B2S
B2SSetData 55,1|FF_DOF E308,-1
SinkHole_Flasher|ON|FF_Flasher DV_FLOL,FL_ON,1,1,100,Lime|FF_B2S
B2SStopAnimation Windows|FF_DOF E407,-1
SinkHole_Flasher|OFF|FF_Flasher DV_FLOL,FL_OFF,1,1,100,Lime|FF_B2S
B2SSetData 51,0|FF_B2S B2SSetData 52,0|FF_B2S B2SSetData
53,0|FF_B2S B2SSetData 54,0|FF_B2S B2SSetData 55,0|FF_B2S
B2SSetData 56,0|FF_B2S B2SSetData 57,0|FF_B2S B2SSetData 58,0
WonderWharf_Left_Flasher|ON|FF_Flasher
DV_FLOL,FL_ON,1,1,100,Yellow|FF_B2S B2SSetData 1,1|FF_DOF E411,-1
WonderWharf_Left_Flasher|OFF|FF_Flasher
DV_FLOL,FL_OFF,1,1,100,Yellow
WonderWharf_Right_Flasher|ON|FF_Flasher
DV_FLOR,FL_ON,1,1,100,Yelow|FF_B2S B2SSetData 2,1|FF_DOF E414,-1
WonderWharf_Right_Flasher|OFF|FF_Flasher
DV_FLOR,FL_OFF,1,1,100,Yelow
```

There are three sections, but only two types of section. They are
TRIGGERS and COMMANDS. TRIGGERS are the detected events that initiate
the COMMANDS. All of the triggers need to be discovered by research and
memory mapping of FX2 tables. Never change a provided trigger unless you
have really good reason to, it will likely screw things up considerably.

The two different TRIGGER sections are CORE and TABLE BASED. ***DO
NOT*** rename the CORE triggers. The Table based triggers can have any
name you like, so long as it matches the name used for its commands in
the COMMAND section.

The COMMANDS are the instructions to carry out when the trigger event
occurs. Every trigger event can have an ON and OFF command, ie
LeftFlipper ON action would be to turn your left flipper solenoid on,
the LeftFlipper OFF command would be to turn it off. Not all triggers
need both ON and OFF commands. If a trigger does not need any commands
its command line can be left with no commands or simply omitted
altogether.

The commands are a subset of those available for Future Pinball and
documented in the previous section. The available commands are

- FF_Dev
- FF_Colour
- FF_Button
- FF_Flasher
- FF_ROM
- FF_DOF

Please note, all times used are in milliseconds. For Future Pinball they
are in hundredths of a second. So for a FX2 command, 1000 = 1 second.

You can have as many commands on a line as you like separated with a
pipe (|) character.

There is one additional command for Pinball FX2 for use with B2S back
glasses, FF_B2S

### FF_B2S CCC,PPPP -- Send a command with parameter(s) to the B2S back glass

The command is subset of the standard B2S commands. The valid commands
are;

- B2SSetData
- B2SStartAnimation
- B2SStartAnimationReverse
- B2SStopAnimation
- B2SStapAllAnimations

For example

- FF_B2S B2SStartAnimation,MyAnimation -- start the animation you called MYANIMATION in the B2S
- FF_B2S B2SStopAllAnimation -- cease all animations
- FF_B2S B2SSetData 15,1 -- turn on Lamp 15
- FF_B2S B2SSetData 4,0 -- turn off Lamp 4

Details of these commands and their parameters can be found in the B2S
documentation.

One special note, when using DOFLinx to communicate with a B2S back
glass all animation names must be IN CAPITAL LETTERS ONLY when you make
/ edit your back glass (directb2s) file.

B2S back glass files are placed in the path as set by PATH_FX2_B2S and
should have the same name as the FX2 file for that same game.

For B2S back glasses to be visible you will need to turn off the
relocation of the back glass within Pinball FX2 cabinet settings (Back
Glass Repositioning = Off). This does turn it off for all games, so we'd
better get directB2S files for every game happening soon!

FX2 trigger configuration files have been setup with a default set of
commands, you don't need to edit them if you don't want to.
