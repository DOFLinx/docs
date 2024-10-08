# After its Running

Once you have a working DOFLinx installation then you may want to do some of these things to make it more enjoyable

1.	If you have the Direct Output Framework (DOF) loaded (usually pinball users or MAME cabinet users without output toys), normally located in C:\DirectOutput folder, then delete the DirectOutput.dll file in your C:\DOFLinx folder.  This will ensure that DOFlinx uses your current installation and not a local copy of the dll.  It will help you out later on when you upgrade DOF.
	
2.	If you have an output device (Dude’s Cab, PinOne, Pinscape, LEDWiz, PacLED, etc) with toys (solenoids, flashers, etc) then run DOFLinxConfig and use “Configure” to setup your toys.  Alternatively read the detailed guide and edit your C:\DOFLINX\Config\DOFLinx.INI directly
3.	If you’ve got Pinball FX then follow the “Enabling Pinball FX for DOFLinx” guide to get full integration from Pinball FX.
4.	If you’ve got MAME then follow the “Guide for Setting up DOFLinx with MAME” guide to get full integration from MAME.

#	Building Your Software Installation

Let’s get the software loaded.

1.	Install your game.

    1.	PinballFX, download the Steam or Epic versions

    2.	MAME

    a)	Install MAME from here [https://www.mamedev.org/release.html](https://www.mamedev.org/release.html)

    b)	Substitute in the correct MAME_XXX.exe, where XXX is the version number) from the \MAME_EXE folder in the DOFLinx installation zip to be MAME.exe in your MAME folder

2.	If you are running PinBall FX then install all of the xxx.directb2s files into the folder you pointed to with the PATH_FX_B2S= parameter (default C:\DOFLINX\B2S\) from here [https://github.com/DOFLinx/B2S-Back-Glasses/releases](https://github.com/DOFLinx/B2S-Back-Glasses/releases)
