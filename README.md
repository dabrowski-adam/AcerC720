# Notes on ArchLinux on the Acer C720 Chromebook.

So the [Archwiki](https://wiki.archlinux.org/index.php/Acer_C720_Chromebook) has most of the must have info. These are just my notes on what I'm doing to keep my new linux laptop happy!

## Enable the watchdog
Copying system.conf to /etc/systemd or setting RuntimeWatchdogSec to a value should have systemd enable the hardware watchdog.

## Trackpad
Well as of 3.18 it is working acceptably.  ~~My main issue is that the trackpage has a physical "click" which does nothing.  You have to tap on the trackpad to register a click which is the opposite of how most of my other machines work.~~ **(The non-function clicking appears to be me specific.  Others report it working!)**  I'm still using a mouse most of the time.

Another option I haven't had a chance to play with is [Hugh Greenberg's port of the cmt trackpad driver from ChromiumOS](https://github.com/hugegreenbug/xf86-input-cmt).  That should in theory work better than the synaptics.

## RAM
yaourt -S zramswap; systemctl enable zramswap; systemctl start zramswap
This will add zram compressed memory to the system as swap.

## TRIM
Either mount ext4/btrfs with discard, or systemctl enable fstrim.timer which will periodically run fstrim to clean up the HD.

## SOUND
Just setting the index=1 in the modprobe is usually enough to make the internal speakers the default audio source
