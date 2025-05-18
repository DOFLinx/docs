# DOFLinx Linux Test Functions

Given that the Linux version of DOFLinx is a console application the many test routines built into the Windows GUI version of DOFlinx are not directly available.
To deliver test functionality a number of commands have been included that can be sent to DOFLinx using DOFLinxMsg.

## TEST_HISCORE=RRR

Used to check that high scores can be read by DOFLinx.
Provide a ROM as RRR and the high scores will be shown in the log and on screen if debug is one, DEBUG=1
For Galaga high scores the command "DOFLinxMsg TEST_HIGH_SCORE=galaga"

## TEST_INPUT=x

Used to turn on / off reporting of input codes in the log.
1 = turn on, 0 = turn off.
The command "DOFLinxMsg TEST_INPUT=1" will turn on logging of input codes for keyboard presses and joystick buttons.

## TEST_PORT=dooo,mm

Used to turn on a defined device / output for mm milliseconds.
To turn on output device #1, port #12 for 3/4 of a second use the command "DOFLinxMsg TEST_PORT=1012,750"

## TEST_PORTS_CYCLE=dooo,eppp,mm

Used to turn on / off a series of ports across a single output device.  The output is turned on for mm milliseconds, then a gap of mm milliseconds before the next port.
To cycle device #1 ports 5 to 14 for 100 milliseconds each the command would be "DOFLinxMsg TEST_PORTS_CYCLE=1005,1014,100"
