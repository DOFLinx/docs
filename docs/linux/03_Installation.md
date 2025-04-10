# Installation and Upgrade

To install or upgrade DOFLinx simply use the installation shell script setup-doflinx.sh .  This will download the DOFlinx files and Mame then place them in the correct spot.
Logon as your arcade user.  Start a command prompt if you are with a GUI.  Run the following:

**wget https://github.com/DOFLinx/DOFLinx-for-Linux/setup-doflinx.sh && chmod +x setup-doflinx.sh && ./setup-doflinx.sh**

If you need to install manually or fix up an installation, then core folders should end up looking something like this:

- ~/doflinx – contains DOLinx and DOFLinxMsg programs
- ~/doflinx/mame – contains *.MAME configuration files for configured games
- ~/doflinx/config – contains the colours.ini and DOFLinx.ini files

Your DOFLinx.ini file contains two important things:

1.	Paths to a number of important locations for such things as the MAME files, colours.ini file, Mame program, Pixelcade, Hi2txt
2.	LINK_BUT_XX= parameter lines that detail the button LED port, if you are using lit buttons, plus the button keyboard input key code.  The key codes are standard Linux key codes.  A copy of the key codes can be found in the ~/doflinx folder
