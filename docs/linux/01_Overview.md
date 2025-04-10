# Linux Version Overview

DOFLinx has been around since 2016.  Until 2025 it has been Windows based and grown to include monitoring of many emulators including a DOFLinx specific version of Mame.  Now a Linux version has been created.  The Linux version does much of what the Windows version does but not everything.  The reason for this is that not all functions of Windows are available in Linux and not all emulators under Windows exist for Linux.
DOFLinx functions and setup can be found through the main guide.  All configuration parameters are the same, but of course some don’t make sense for Linux, ie Future Pinball related items.  Here I will explain the material points.

What it _**does**_

-	Monitor Mame for outputs, scores and other actions
-	Drive Pixelcade devices
-	Run output devices for toys such as RGB and mono button LEDs, solenoids, flashers, etc.  Output devices supported are
    -	Pinscape Pico
    -	Pinscape
-	Attract mode for LED buttons and marquees
-	Get Mame high scores via Hi2txt
-	Key to commands
-	Work with front ends via the MENU_ROM and other commands

What it _**doesn’t do**_

-	Addressable LEDs
-	Use the Direct Output Framework
-	Monitor Pinball FX2 / FX3 / FX or Future Pinball
-	Take input from Xbox or Joystick controllers
-	Provide a built-in score screen
-	No GUI front end or GUI configuration
