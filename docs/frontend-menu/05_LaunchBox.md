# LaunchBox / BigBox

With thanks to Olivier Jacques, there is a plugin to integrate LaunchBox / BigBox with DOFLinx called DOFConnect.  While the instllation is included in the DOFLinx download the project can be found here [https://github.com/DMDTools/DOFConnect](https://github.com/DMDTools/DOFConnect)

Installation is simple:
1. Copy the "DOFLinx LauchBox Integration" folder and its contents from DOFLinx to your LaunchBox plugins folder, ie "\LaunchBox\Plugins\DOFLinx LauchBox Integration"
2. Make sure your emaultor "Titles" are the same as you emaulator folder names for DOF2DMD
3. Edit the DOFLinx MENU.INI to have the customisations actions you want LaunchBox to trigger

Your installation should look like this

![](../img/media/LaunchBox-Installed_Plugin.jpg)

For an emulator named "MAME" in LaunchBox like this

![](../img/media/LaunchBox-Set_Emulator_Name.jpg)

youu should a MAME artwork folder for your marquess to go on your DMD like this

![](../img/media/LaunchBox-Alignment_of_Name_to_DOF2DMD_Artwork.jpg)

!!! Note

    You can use either the Platform or Emulator as the Source Category being sent to DOFLinx.
    By default this is the Emulator.
    To change to this to be the Platform, edit the DOFConnect.json file in with your DOFConnect.dll and set the "SourceCategory" to be "Platform"
