# Notes on ArchLinux on the Acer C720 Chromebook.

So the [Archwiki](https://wiki.archlinux.org/index.php/Acer_C720_Chromebook) has most of the must have info. These are just my notes on what I'm doing to keep my new linux laptop happy!

## Enable the watchdog
Copying system.conf to /etc/systemd or setting RuntimeWatchdogSec to a value should have systemd enable the hardware watchdog.

## Trackpad
Ugh, buy a mouse.
If you're stuck with the trackpad, the synclient.sh can run on X startup.  Its ssets the trackpad to some more sensible defaults.  Still a bit of a challenge and I end up reaching for a mouse most of the time.

## RAM
yaourt -S zramswap; systemctl enable zramswap; systemctl start zramswap
This will add zram compressed memory to the system as swap.

### Controlling Chromium with cgroups
So of late, Chromium's memory usage has been causing the machine to hardlock so I'm experimenting with using kernel cgroups to limit it to 1G of the ram.

* Install libgroups from the AUR
* copy the cgconfig.conf and cgrules.conf to /etc
* systemctrl enable and systemctrl start cgconfig and cgrules
* `cgget -a browsers` should show the cpu / memory limits

This should in theory limit Chromium from going crazy with resources and you could add Firefox or Midori or whatever to cgrules.  It's pretty extensible but I haven't fully tested it yet.  It doesn't seem to be used as much in Arch as I'd expect.

This was based initially on a [gist](https://gist.github.com/juanje/9861623) by @juanje.

## TRIM
Either mount ext4/btrfs with discard, or systemctl enable fstrim.timer which will periodically run fstrim to clean up the HD.

## SOUND
Just setting the index=1 in the modprobe is usually enough to make the internal speakers the default audio source
