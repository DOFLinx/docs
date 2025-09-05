# What is DOFLinx?

DOFLinx is pinabll and arcade "middleware".  It runs on your cabinet monitoring events from the game emulator and then traslates those into cabinet actons.  For example in Pinball FX game table events like bumpers hits, slingshots, drop targets, loop passovers, etc are fed to DOFLinx, these are then turned into actions that drive your unique set of toys (solenoids, flashers, RGB buttons, shaker, addressable LEDs etc).  Another exmaple is arcade games in Mame, DOFLinx gets events from the game along with real time scores, and then triggers toy actions, LED / LCD screen animations and large screen live score output.

There is a Linux version of DOFLinx that can be used for Mame arcade games and some limited output boards.

# What Can DOFLinx Do?

- Drive toys on the following output boards in any combination
  - LEDWiz
  - Pinscape
  - Dude's Cab
  - Pinscape Pico
  - PinOne
  - PacDrive
  - PacLED64
  - Ultimate I/O
  - PinControl 1
  - PinControl 2
  - Sainsmart
  - Teensy -- Addressable LEDs
  - Wesmos -- Addressable LEDs
- In Basic or Fallback mode trigger solenoids for flipper force
    feedback for any pinball game emulator based on the flipper keys
- Use keyboard, Xbox controller and joystick buttons for input
- For Pinball FX and Pinball FX3 generate nudge in game by physically
    nudging your table using a Pinscape accelerometer
- Use direct integration from Pinball FX built with Zen to get table
    events
  - Map those events to cabinet actions for
    - Use back glasses that illuminate based on table events (not simply animated), just like a real pinball machine
    - Solenoids / contactors for flippers, slings, bumpers and
            drop targets
    - 5 x RGB Flashers
    - RGB cabinet lighting
    - Addressable LED effects
    - Fan / Blower
    - Shaker
    - Gear motor
    - 3 x Chimes
    - Bell
    - Strobe
    - Beacon
    - Knocker
    - Run a shell script / external program
    - Load and drive animations in DirectB2S backglasses
    - Play surround sound force feedback sounds for stereo, 5.1 or
            7.1 sound systems
    - Output to Pixelcade LED and LCD displays
    - Set a table specific colour palette
    - Set RGB buttons such as flipper and magna save to any colour
            combination per table
    - Illuminate mono buttons
  - Comes with a default set of FX mapping files that you can edit
        to add or change what table events create cabinet actions
- Combined with the DOFLinx specific MAME version monitor key emulator
    events and real time scores to derive events that drive actions
  - Map those events to cabinet actions for
    - Solenoids / contactors for flippers, slings, bumpers and
            drop targets
    - 5 x RGB Flashers
    - RGB cabinet lighting
    - Addressable LED effects
    - Fan / Blower
    - Shaker
    - Gear motor
    - 3 x Chimes
    - Bell
    - Strobe
    - Beacon
    - Knocker
    - Run a shell script / external program
    - Load and drive animations in DirectB2S backglasses
    - Play surround sound force feedback sounds for stereo, 5.1 or
            7.1 sound systems
    - In built live score screen
    - In built high score screen
    - Drive Pixelcade LED, LCD, dot matrix and meta data displays
    - Present MAME marquee artwork on Pixelcade LED and LCD, plus
            any DMD using DMDExt
    - Show animations on Pixelcade LED and / or LCD screens based
            on in game achievements
    - Show scores and animations on any DMD using DMDExt via
            DOF2DMD
    - Show high scorces
    - Set a table specific colour palette
    - Set RGB buttons such as flipper and magna save to any colour
            combination per table
    - Illuminate mono buttons
    - Drive any DMD using DMDExt via DOF2DMD
  - Comes with a default set of MAME mapping files that you can edit
        to add or change what table events create cabinet actions
  - Cabinet buttons to used as a trigger for actions. Allows things
        like "fire" button the be set to run something like a "flash
        blast" effect on addressable LEDs, or a fire sound in SSF
- Monitor Pinball FX3 and derive events to run table actions
  - Map those events to cabinet actions for
    - Use back glasses that illuminate based on table events (not simply animated), just like a real pinball machine
    - Solenoids / contactors for flippers, slings, bumpers and
            drop targets
    - 5 x RGB Flashers
    - RGB cabinet lighting
    - Addressable LED effects
    - Fan / Blower
    - Shaker
    - Gear motor
    - 3 x Chimes
    - Bell
    - Strobe
    - Beacon
    - Knocker
    - Load and drive animations in DirectB2S backglasses
    - Surround Sound Force feeback via Pinup Popper
    - Set a table specific colour palette
    - Set RGB buttons such as flipper and magna save to any colour
            combination per table
    - Illuminate mono buttons
  - Comes with two default sets of FX3 mapping files for physical
        and surround sound cabinets
- Monitor Pinball FX2 and derive events to run table actions
  - Map those events to cabinet actions for
    - Use back glasses that illuminate based on table events (not simply animated), just like a real pinball machine
    - Solenoids / contactors for flippers, slings, bumpers and
            drop targets
    - 5 x RGB Flashers
    - RGB cabinet lighting
    - Addressable LED effects
    - Fan / Blower
    - Shaker
    - Gear motor
    - 3 x Chimes
    - Bell
    - Strobe
    - Beacon
    - Knocker
    - Load and drive animations in DirectB2S backglasses
    - Set a table specific colour palette
    - Set RGB buttons such as flipper and magna save to any colour
            combination per table
    - Illuminate mono buttons
  - A default sets of FX2 mapping files are availble
- Monitor Future Pinball for actions coded to drive toys for
  - Solenoids / contactors for flippers, slings, bumpers and drop
        targets
  - 5 x RGB Flashers
  - RGB cabinet lighting
  - Addressable LED effects
  - Fan / Blower
  - Shaker
  - Gear motor
  - 3 x Chimes
  - Bell
  - Strobe
  - Beacon
  - Knocker
- Cabinet attract mode
  - Run any series or parallel pattern for your lighting, LEDs,
        button lights, RGB lighting and flashers, plus any other
        directly attached toy
  - Change pattern at any time
  - Stop and start by simply sending DOFLinx a message
  - Start via inactivity timer
  - Display marquees on Pixelcade or DMD device(s)
- Front and menu system navigation allows
  - display of game information and high scores for currently
        displayed game
  - display of current marquee via Pixelcade
  - display of a directB2S backglass
  - Fully configurable use of any output and combination of outputs
        for any navigation event, ie forward, back, page forward, page
        back, select. Outputs are the same as in game actions, ie
        solenoids, flashers, addressable LED effects
  - Currently has been setup for Pinup Popper
- Drive Xbox rumble motors
- Light any combination of RGB or mono buttons
- Comprehensive set of test screens for devices, flashers, back
    glasses, ROM effects, Pixelcade, etc.
- Built in configuration tool for all core setup parameters
- Ability to change most configuration while running allowing for
    different behaviour between emulators and game / tables. Usually run
    from the front end menu system when a game / table is selected
- Local on screen and log file for debug, or monitor the debugging
    from a different machine via a TCP link
- Push focus back to MAME, Pinball FX, Pinball FX3 or Pinball FX2 to
    avoid the emulator not being in focus at start
- Setup any number of colours using a name and RGB FFFFFF format
- Link a button press to turning on an output device
- Link a button to turn on a RGB device with any colour
- Set buttons to toggle RGB devices on / off with any colour
- Night mode to suppress noisy toys when others want to sleep
- RGB cabinet lighting to be random, multiple colours, fixed
- Trigger RGB lighting changes by timer, flipper press or remain fixed
- Built in settings menu that pops up like a pinball configuration on
    the DMD, used to turn various items on / off while running in
    cabinet mode, ie night mode, RGB lighting or with the assistance of
    some hardware flip-flop an output
- Use real time messaging to DOFLinx to do things such as
  - stop (kill) other processes
  - Light buttons
  - Shutdown DOFLinx
  - Run a INI file with updated parameters
  - Turn on a RGB device for a specified time with a specified
        colour

<meta name="google-site-verification" content="pZEq4BDBtIzT02hL6EaRwYYeR-ejQ2SBjzCrC2VtpFE" />
