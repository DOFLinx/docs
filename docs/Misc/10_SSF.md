# Enabling SSF

# What is SSF?

**SSF** (Surround Sound Feedback) is an audio system that utilizes multiple speakers strategically arranged to create a virtual sound environment. A common use case for **SSF** is in virtual pinball tables.

Consider the sounds in a real pinball machine: the background music, sound effects, and the physical sounds produced by flippers, the pinball, and various mechanical components. While these sounds can be played through a single speaker, they all originate from the same source, reducing the realism of the experience.

**SSF** addresses this by incorporating additional speakers positioned in specific locations within the table to simulate the authentic auditory experience of a real pinball machine.

# How Does SSF Work?

**SSF** is typically implemented using one or two sets of speakers. These may include standard speakers or tactile transducers such as exciters and bass shakers (discussed further in the Hardware Components section below).

When setting up a virtual pinball table, the speakers are typically placed under each corner of the playfield. The entire speaker system is connected to a 7.1 sound card and configured using the card’s surround sound settings.

# Hardware Components
To enable **SSF** (Surround Sound Feedback) effectively, the following hardware components are required:

- A 5.1 or a 7.1 soundcard.
  - The sound card is the central component of the system, combining multiple sets of speakers to create a virtual soundscape within a physical space.
  - A 7.1 sound card is preferred for more advanced configurations, providing additional channels for enhanced surround sound effects.
- Audio Amps
  - Connect each set of exciters and your bass shaker amps.
- A Set of Standard Speakers and a Subwoofer
  - This set of speakers is responsible for outputting.the music and sound effects of the system.
  - The subwoofer handles the low-frequency sounds, enriching the overall audio experience by providing deep bass tones.
- One or Two Sets of Exciters and an Optional Bass Shaker
  - 
  - Exciters are tactile transducers that emit sound through the material they are attached to, allowing the user to feel the sound physically. For example, when pressing the flipper button, you feel the vibration through the hand operating it.
  - The bass shaker functions similarly to a subwoofer but focuses on low-frequency tactile feedback, enhancing the physical sensation of in-game actions.
  - Exciters are strategically placed to represent specific components, creating an immersive audio-physical experience.

## Speaker Placement Example: Virtual Pinball Table
In the case of a virtual pinball table, speaker placement is crucial for accurately replicating the sound environment of a real machine:
- Main Speakers: Typically placed in the backbox, these speakers handle music and sound effects.
- Exciters: Positioned on the sidewalls near the corners of the playfield. These simulate the physical sounds of flippers, bumpers, and other mechanical components.
- Bass Shakers: Installed under the front and back of the playfield, these provide tactile feedback for low-frequency sounds, such as ball impacts and flipper movements.

## Sound Localization in Action
With speakers placed in specific locations, **SSF** allows for precise sound localization, making the virtual experience feel realistic. For example:
- Pressing the left flipper triggers sound from the bottom-left exciter, providing both auditory and tactile feedback.
	•	If the bumpers are located at the back-right of the table, the back-right exciter will emit the corresponding sound effect, matching the in-game action to the physical response.

# Software Configuration
There are two main systems that are used to configure **SSF**: Your sound card configuration and **DOFLinx**. The sound card configures the layout of your speakers and DOFLinx triggers the exciters according to what is happening in the software you are wanting to be represented by your physical setup.

## Configuring your soundcard
To begin, locate the sound configuration software for your device. For demonstration purposes, this guide will reference the default sound settings available in Windows.

1. Press Windows+R, type mmsys.cpl, press Enter
2. Select the Playback tab
3. Select your speakers from the list
4. Click Configure
5. Select 7.1 surround (even if you're not actually using surround speakers). Click Next.
6. Un-check Subwoofer and Center. Check-mark Side Pair and Rear Pair if you're using playfield effects speakers, un-check them if not. Click Next.
7. Make sure Front left and right is checked for Full-range speakers
8. Click Next then click Finish

***Make sure your sound card is set to the default sound device**

## Configuring DOFLinx
**DOFLinx** is the main system that is used to trigger sounds in your **SSF** system. You will need to make sure you have the latest version of DOFLinx installed. You can download the latest version here: https://github.com/DOFLinx/DOFLinx/releases. Use this guide to install DOFLinx: https://doflinx.github.io/docs/getting-started/04_Installation.html

1. Locate where you installed **DOFLinx**
   - Typically this is installed in C:\DOFLinx
   - Make sure that before you unzipped the package that you have it unblocked. If it is not unblocked, either delete your install and replace it with the unblocked zipped files or you can manually unblock all of the files.
2. Open the **DOFLinx.ini** file in your editor of choice
3. Add the following lines to your INI file
   **FX_PATH=C:\DOFLinx\FX**
   
   **SSF_ENABLED=1**
   
   **SSF_SOUND_PATH=C:\DOFLINX\sounds**

   **SSF_DEVICE=-1**

   - Setting your sound device to -1 will make **DOFLinx** use your default sound device. If you want to manually set the device number, you will need to enable debug mode in your INI by adding the line **DEBUG=1**. When you start **DOFLinx** it will output your sound devices and it will show the devide number for each of them. You can replace **SSF_DEVICE=-1** with whatever your device number is.

## Enabling SSF for Pinball FX
1. Locate the **DOFLinxTrigger.dll** file in your C:\DOFLinx folder
2. Copy the file to **C:\Program Files (x86)\steam\steamapps\common\pinball fx**
3. 


# Testing
1. Open your **DOFLinx.ini** file and add the following line:

    **DEBUG=1**

2. Start **C:\DOFLinx\DOFLinx.exe**
3. Open the application you want to test with. For example, open Steam and launch Pinball FX
4. Load a table
5. Start the game and hit the left flipper button and you should hear your left exciter and bass shaker make the flipper sound that is set in C:\DOFLinx\sounds


# Troubleshooting



# More Information
A lot of additional information can be found at http://mjrnet.org/pinscape/BuildGuideV2/BuildGuide.php?sid=audio


# Surround Sound Feedback (SSF)

1. What is SSF
2. Pre-reqs
3. Hardware Components
    1. Soundcard
    2. Exciters
    3. Bass Shakers
4. Software Configuration
    1. Sound Device settings
    2. FX folder and how to update
    3. INI
5. Testing
6. Upgrading
7. Troubleshooting
    1. Common mistakes
    1. Log investigations