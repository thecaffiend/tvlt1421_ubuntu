# Thinkvision LT1421 Initializer

This script is used to turn on or off a ThinkVision LT1421 USB monitor in 
Ubuntu. It has been tested on Ubuntu 13.10 using mainline kernel 
3.12.0-031200-generic. I was unable to get things to work using the Ubuntu
patched kernel (there are posts that displaylink support may have suffered a 
regression in those kernels).

I am not a guru on bash scripting, nor am I an expert on DisplayLink, so any
advice, expertise, questions, comments or concerns are all welcome such that
I may learn something. Bring it!

Also, this works for me as is. I can't guarantee it'll work for anything,
especially something other than an LT1421 on Ubuntu 13.10 (for good measure,
running on aything other than a System76 Gazelle Pro) with the proper kernel.
Best of luck though ;).

References I gleaned info from for this script:

* Jochen Kirstaetter's [excellent writeup](http://jochen.kirstaetter.name/blog/linux/using-aoc-usb-monitor-in-ubuntu-1304-displaylink-e1649fwu.html) got me quite a bit of the way there. I ended here with an upgraded kernel (not Ubuntu patched) and to the point of the "works, but only paints around the cursor" (you'd know it if you saw it, it's mentioned in the comments of the post)
* This post on [using a thinkvision usb monitor in arch](https://bbs.archlinux.org/viewtopic.php?pid=1321200#p1321200) which got me the right xrandr settings to fix the painting only around the cursor issue. 
* The [how to](http://ubuntuhandbook.org/index.php/2013/11/linux-kernel-3-12-released-install-ubuntu-or-linux-mint/) on upgrading to the latest (3.12.0-031200-generic as of this writing) kernel.  

## Notes
* No mucking with xorg.conf files was needed
* After upgrading the kernel, no additional packages were needed.
* I have not tried booting with the USB monitor plugged in already (this is all tested via hotplug when already booted). I did at one point try this when I was half way to working (the monitor was only displaying the maroon and azure lines many have posted about), and booted to blank screens. Unplugging the monitor got me to "you're in low graphics mode", but still never came back to an x-session. Had to drop into a console and reboot. I have not looked into it further. 
* I still occasionally get some error messages when turning on the monitor, but everything still seems to work, so unless it becomes an issue, I'll let it be. The error is generally of the form:

```
X Error of failed request: BadName (named color or font does not exist)
Major opcode of failed request: 140 (RANDR)
Minor opcode of failed request: 16 (RRCreateMode)
Serial number of failed request: 44
Current serial number in output stream: 44
```

## Assumptions
* The script assumes there will only be one device that comes up as "DVI-X" (where X is the device number) from the output of xrandr, and that this device is the USB monitor. It would be nice if this was not the case and that I could determine the DisplayLink device among more than one DVI-X. I don't see anything in xrandr's out put that would make this easy, but perhaps it could be mixed wih some other command to figure this out (lsusb maybe?).
* The script also assumes that the primary monitor is identified as eDP1 in the output of xrandr. This could use some work for robustness.

# Usage
thinkvision.bash [on/off]
