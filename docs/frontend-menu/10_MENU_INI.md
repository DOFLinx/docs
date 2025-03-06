# Configuring Actions for Front End Menus

At startup DOFLinx loads a file called MENU.INI from the base DOFLinx folder.  A default MENU.INI is shipped with DOFLinx.  This file contains the actions that DOFLinx will initiate when sent commands from a front end menu system such as Pinup Popper or LaunchBox.

It will be normal to customise your MENU.INI file to get the effects you want.  Once customised, make a safe copy of the file so that you do not accidentally copy over the top of it when upgrading DOFLinx at a later point in time.

The MENU.INI file will look something like this:

    [STARTUP]
    LOAD_SOUND=LFlipper,100,LEFT_REAR,Flipper_L01,Flipper_L02,Flipper_L03,Flipper_L04,Flipper_L05,Flipper_L06,Flipper_L07,Flipper_L08,Flipper_L09,Flipper_L10,Flipper_L11
    LOAD_SOUND=RFlipper,100,RIGHT_REAR,Flipper_R01,Flipper_R02,Flipper_R03,Flipper_R04,Flipper_R05,Flipper_R06,Flipper_R07,Flipper_R08,Flipper_R09,Flipper_R10,Flipper_R11
    LOAD_SOUND=BallColl,100,REAR,Ball_Collide_1,Ball_Collide_2,Ball_Collide_3,Ball_Collide_4,Ball_Collide_5,Ball_Collide_6,Ball_Collide_7
    LOAD_SOUND=DropTarget,100,SIDE,Drop_Target_Down_1,Drop_Target_Down_2,Drop_Target_Down_3,Drop_Target_Down_4,Drop_Target_Down_5,Drop_Target_Down_6

    [COMMANDS]
    BLANK|ON|FF_DMD,U,blank
    STARTUP|ON|FF_DMD,U,display/text?text=My%20Arcade%20Cabinet&size=L&font=BTTF&color=FFD700&cleanbg=true&animation=ScrollLeft&loop
    STARTUP|OFF|FF_DMD,U,loopstop
    LAUNCH|ON|FF_DMD,U,display/text?text=Launching&size=XL&font=Matrix&color=00BFFF&cleanbg&duration=4
    MAME|ON|FF_Colour Cyan,RGB_TT,20000|FF_CMD START_DOF2DMD
    MAME|OFF|FF_Colour Black,RGB_TT,1|FF_CMD STOP_DOF2DMD|FF_CMD SCORE_SCREEN_CLOSE
    NEXT|ON|FF_SSF LFlipper|FF_Flasher DV_FLOL,FL_TT,1,100,100,White|FF_Dev DV_ML,-1|FF_DOF E212,-1
    PRIOR|ON|FF_SSF RFlipper|FF_Flasher DV_FLOR,FL_TT,1,100,100,White|FF_Dev DV_MR,-1|FF_DOF E215,-1
    NEXTPAGE|ON|FF_SSF BallColl|FF_Flasher DV_FLIL,FL_TT,1,100,100,Cyan|FF_Flasher DV_FLOL,FL_TT,1,100,100,Cyan|FF_Dev DV_LF,-1|FF_DOF E120,-1
    PRIORPAGE|ON|FF_SSF DropTarget|FF_Flasher DV_FLIR,FL_TT,1,100,100,Cyan|FF_Flasher DV_FLOR,FL_TT,1,100,100,Cyan|FF_Dev DV_LF,-1|FF_DOF E121,-1
    MOVE|ON|FF_SSF LFlipper|FF_Flasher DV_FLOL,FL_TT,1,100,100,Cyan|FF_DOF E212,-1|FF_Flasher DV_FLOR,FL_TT,1,100,100,Cyan|FF_DOF E212,-1|FF_DOF E215,-1

The file takes the same form as the *.FX3, *.FX and *.MAME files, but will not execute anything in the [STARTUP] section other than loading commands.  This is due to the fact that the file is loaded by DOFLinx at start up and executing anything then for a front end menu wouldn't make sense.

The [STARTUP] section above contains the loading of surround sound force feedback (SSF) sounds that are using by a command in the [COMMAND] section.

The [COMMAND] section contains the key trigger names, ie BLANK, PRIOR, MAME, a definition of them executing when the trigger starts, "ON", or when the trigger finishes, "OFF".  Triggers do not need both ON and OFF commands, it depends what you're trying to do.

It doesn't matter if you are not using a command, just leave it there, it will get loaded, but it takes so little space and no impact on speed, so it doesn't matter.

Names used can be anything, but must match what your front end menu sends through.  The DOFConnect.dll for Launchbox is coded to use BLANK, STARTUP, LAUNCH and MOVE.  Any other command names are then your emulator Title.  The example PinUp Popper code uses NEXT, PRIOR, NEXTPAGE and PRIORPAGE, but you can change those in the Popper script if you really want to.

For Launchbox the specific command names explained are:
STARTUP - executes when you start Launchbox, so use this for a banner, triggering flashers or addressable LEDs, showing your favourite animation on the DMD, etc.
LAUNCH - executes when you select a game to play
MOVE - executes when you move from one selected item to another
BLANK - executes when Launchbox determines that outputs should be closed / blanked, ie when exiting

Pinup Popper doesn't have some of the above, although I'm sure it could be coded if you wanted it given Popper's flexibility.  It does have far more granular navigation items available though, ie movement direction and paging.

The "MAME" lines are executed when you enter and leave the menu section for MAME games, ie the emulator / platform.  You can add as many of these as you have emulators, ie "Pinball FX", "Nintendo", etc.

You will see both ON and OFF actions for the MAME lines.  This means that MAME|ON is executed when you enter the MAME submenu / select the first MAME game, MAME|OFF is executed when your last game selected / highlighted was a MAME game, but the next game is not.

In the example above when the first MAME game is selected the undercab lighting is set to Cyan and DOF2DMD is started.  When the first non MAME game, after having been in the MAME game area is selected, the undercab lighting is turned off and DOF2DMD is stopped.

There is no practical limit to how many things you can have DOFLinx do from your front end menu.  If you can't find the right toy via DOFLinx, remember there is always the FF_RUN= command for external programs as well.
