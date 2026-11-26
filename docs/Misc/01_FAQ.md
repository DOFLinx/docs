# Common Issues Over Time / FAQ

Here are some issues that have been encountered over time that might help you.
If you think there is something that should be added in this list feel free to contact me or simply fork a branch and do an edit yourself.

## Confused about setting up the DOFLinx.INI file

Manually editing the DOFLinx.INI file was the original way to configure DOFLinx.  It still remains the most granular way to do this as well.  However, to get started you can just run DOFLinxConfig.exe and press "Configure" to use the menu.  Doing this will read your current DOFLinx.INI file if you have one and write a new DOFLinx.INI file when you are done.

## Should I run DOFLinx as 'Administrator'
No, nothing should need to run as Administrator.  Having said that, if you want to and it works for you, it will not hurt DOFLinx.  Do note however I do not test or support this.

## Mame.INI file keeps losing "output network" setting

Some front end menus have been setup to use multiple Mame.ini files.  Sometimes they are copied into place before certain types of games, ie horizontal or vertical games (ie horizontal.ini copied to mame.ini).  So, if you edit "output network" into your mame.ini it may seem to disappear.  You can solve this by changing your emulator setup in your front end menu and adding "-output network" to the command line arguments.

## I Need a 32 bit version of DOFLinx

Err, it is extremely unlikely that you do.  Unless you have a 32 bit version of Windows running on your cabinet then you do not need 32 bit DOFLinx.  Provided that you have 64 bit DOF installed, and you can easily install both 32 bit and 64 it DOF if you need 32 bit DOF for something else, then all will be good.

## My toys trigger my own nudge!

Yes, I found this out when I built my new 4K FUturama cabinet and mounted a decent accellerometer on my Pinscape Pico.  For this reason the concept of being able to pause nudge for a period of time after one or more of your toys fire was introduced.  Look up the NUDGE_PAUSE parameter.

## Should I stop or kill DOFLinx via my front end or some other way

No you should not.  DOFLinx is designed to start with Windows startup and run at all times.  It will only activate when an emulator you specify is running.  Killing the DOFLinx process runs the risk of not saving parameters and risking startup next time.  In addition there is an overhead startup time for DOFLinx and you really don't want that as you are starting a table, it both slows your system and runs the risk of creating timing issues due to DOFLinx not being ready when your emulator starts.
If you need to stop DOFLinx while working on your machine, ie changing your INI file, then simply run "DOFLinxMsg QUIT" for a neat exit.

## When I run with DEBUG=1 my DOFLinx window is not white

DOFLinx will change the background of the logging box to pale green when it is a Beta version, yellow if being run as administrator, royal blue when in night mode and hot pink if it has logged serious error.

