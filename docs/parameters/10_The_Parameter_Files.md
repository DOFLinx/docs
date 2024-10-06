# The Parameter Files

By default, all parameters are in the `DOFLinx.INI` file. Many parameters
have a default, so may not be required. Check each parameter in the
section below.

When using DOFLinx in a Launch Before setup you may want different keys
to do different things for a different emulator or even at the table
level. To do this, place the parameters you don't want to change in
DOFLinx.INI and the ones you want to change in XYZ.INI where XYZ is any
valid file name.

Some parameters can be overridden by redefining them in your SUP_INI
file, others cannot. Honestly, I haven't tested them all. The design is
for them to appear once only. If you want to try overriding, feel free
to give it a go, I have done so for KEY_TO_RGB and it works like a
treat.

Note: If you're running DOFLinx as Set and Forget, and edit your
DOFLinx.INI file, you will need to restart the DOFLinx process. This can
be done by simply rebooting, or kill it off in Task Manager and restart
it by double clicking on it. Remember, unless you are in debug mode you
will not see a window pop up in front of you, so avoid trying to start
it twice!
