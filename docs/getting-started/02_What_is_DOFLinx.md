# What is DOFLinx

DOFLinx is a utility program designed to work with the DOF (Direct
Output Framework) R3 (from version 6.20 onward this is the R3++ version
of DOF) to provide some additional functionality for pinball emulators
that don't do it directly. It started life just adding flipper force
feedback to Pinball FX2 and was called DOFFX2.

Some of the features are:

- Basic Fire flipper solenoids / contactors from with Pinball FX2,
  Pinball FX3, Pinball Arcade, etc using keyboard intercept
- Full force feedback for Pinball FX2 and FX3 for games that have been
  memory mapped
- Link to Future Pinball and process messages to enable fully scripted
  force feedback
- Add flipper force feedback and RGB easily to tables with no force
  feedback coded
- Have RGB devices automatically cycle colours based on a variety of
  triggers
- Link a key to turn on one or more outputs while pressed
- Link a key to set an RGB device to a colour
- Link a key to turn an RGB device to a colour while pressed then
  revert back
- Game specific colour sets
- Control your LEDs and solenoids from various places, just for fun
- Respond to messages sent from other scripts or applications to
  trigger outputs and colours
- Settings menu to control relays and other devices in your cabinet
  that turn on / off features
- Link to B2S backglasses from Pinball FX2 and FX3
- Drive addressable LEDs setup in the DOF from Pinball FX2 and FX3 and
  Future Pinball triggers
- Run PUPlayer videos from FP and FX2 / 3
- Produce nudge into FX3 from Pinscape accelerometer
- Support for XBox (XINPUT) and Joystick (DINPUT) controllers
- Joystick based analogue joystick to trigger FX2 and FX3 ball launch
- Drive Xbox rumble motors from table trigger events in FX2, FX3 and
  FP
- Connection to MAME for inputs and outputs
- Drive Pixelcade devices
- SSF 7.1
- Drive DMD's via DOF2DMD using DMDExt

DOFLinx can operate in a number of ways, in fact it can do them all in
combination to get the best effect. There are a couple of levels of
force feedback available, full force feedback where specific triggers
make DOF devices "fire" and light up. Then there is simple force
feedback, where flipper keys as the input are "listened" for and when
press "fire" DOF devices. When fully configured DOFLinx will attempt to
use the most detailed level of force feedback first, then progressively
drop back to simple force feedback dependant on what's been configured
and what is available.

Full force feedback is available via Future Pinball tables scripted for
DOFLinx and for Pinball FX2 / 3 games with memory map files.

Simple force feedback "listens" for flipper (and other configured key)
presses and activates the configured DOF devices. It can also run a
background colour display providing automated colour for tables with
nothing specifically coded.

The fall-back process is quite simple. For Future Pinball DOFLinx will
first check if the table has been coded for DOFLinx, if so you have a
fully active and full featured force feedback link. If not DOFLinx will
check if the table has been flagged specifically, or simply setup in the
absence of a full force feedback link, to selectively use simple force
feedback.

The fall-back process for Pinball FX2 and FX3 is similar. DOFLinx will
first check for a trigger configuration file for the table being played.
If one is present, then full force feedback is turned on and scripted
actions are taken when the various trigger events occur. If no trigger
configuration file exists then simple force feedback is enabled.
