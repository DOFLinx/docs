# Run DOFLinx with Sufficient Access

DOFLinx needs to run with access to the /dev/input/ path.
Some versions of Linux, such as that on the Raspberry Pi have this access by default, others do not.
The reason for this is that DOFLinx needs to monitor the raw keyboard and joystick inputs of all keyboard and joystick devices such as an iPac, Pinscape, etc.
This is so that DOFlinx can determine when a button is pressed while Mame (and other things) are the in focus / foreground applications.

If DOFLinx does not have access to input devices then button input cannot be monitored.
The use of input buttons in DOFLinx will be logged and disabled for that session.
Without being able to check on pressed keys then DOFLinx cannot determine when Coin, Pause, P1, P2, Exit, and all other Mame input keys are pressed.
DOFLinx needs this monitoring for proper operation and triggering. 

If you are using output controllers for LEDs and toys such as Pinscape Pico, Pinscape, etc then write access to /dev/hidraw* is also required.

A good solution to granting access is to use udev rules.  Using udev rules will ensure that security is set as you want and need it at every system boot and plugging of USB devices.  The security required on various flavours of Linux varies, so giving a single answer on how to do this is difficult.

My current /etc/udev/rules.d/69-doflinx.rules file looks like this.

    KERNEL=="event[0-9]*", MODE="0777"

    KERNEL=="hidraw*", MODE="0777"

    KERNEL=="js[0-9]*", MODE="0777"

I take the point of view that my Linux arcade machine is not used as a multiuser server, nor is it high security, as such, I keep it really simple.
