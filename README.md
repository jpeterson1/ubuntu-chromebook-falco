# Ubuntu Installation Instructions (HP Chromebook 14)

Chromebooks come with [ChromeOS](http://en.wikipedia.org/wiki/Chrome_OS) installed by default. This repository contains everything I used to install Ubuntu on my [HP Chromebook 14](http://www.google.com/intl/en/chrome/devices/hp-chromebook-14/) (code name Falco).

These steps produce a dual-boot system where ChromeOS runs off the built-in SSD and Ubuntu runs off of a SD card.

## Prerequisites

* HP Chromebook 14 (Falco)
* Another computer (Linux, Mac, or Windows)
* 4GB+ USB thumb-drive or SD card
* 16GB+ high performance (UHS3) SD card + reader (different than above)
* USB Mouse

## Installing Ubuntu onto the SD card

On my other computer:

1. [Download](http://www.ubuntu.com/download/desktop) Ubuntu 14.04+ Desktop 64-bit ISO
2. Create a bootable USB/SDCard (4GB+) from the ISO ([linux](http://www.ubuntu.com/download/desktop/create-a-usb-stick-on-ubuntu), [mac](http://www.ubuntu.com/download/desktop/create-a-usb-stick-on-mac-osx), [windows](http://www.ubuntu.com/download/desktop/create-a-usb-stick-on-windows))
3. Plug in both cards (4GB+, 16GB+) into the computer and reboot
  * Note: Boot options in the BIOS may need to be updated
4. Install Ubuntu as normal onto the larger (16+GB) SD card.
  * Do not set up a swap partition/file as this will cause excessive
    wear and tear on the SD card
  * Bonus points: use full disk encryption

## Preparing the Chromebook

**WARNING: This will erase your Chromebook!!**

1. Backup any local data on your chromebook
2. Enter developer mode (Esc+Refresh+Power)
3. Press Ctrl-D at the prompt and confirm
4. Wait for the machine to be wiped and reboot
5. Login as Guest and open a terminal (CTRL+Shift+T)
6. Enable booting from SD Card:
  * `$ sudo crossystem dev_boot_usb=1`
  * `$ sudo crossystem dev_boot_legacy=1`
7. Insert 16GB+ SD card and reboot
8. At the scary screen, hit CTRL-L
9. Boot from the SD card

At this point Ubuntu is booted and partially functional. Notably, the trackpad does not work. Plug in a USB mouse or rely on keyboard shortcuts.

## Configure Ubuntu

1. Open a terminal window
2. Make sure Ubuntu is up-to-date
  * `$ sudo apt-get update && sudo apt-get -u upgrade`
3. Copy the config files in this repository into their respective places
4. [Download](http://kernel.ubuntu.com/~kernel-ppa/mainline/) and install the latest [stable](http://www.kernel.org) kernel (v3.18+, generic, amd64)
  * `$ sudo dpkg -i linux-*.deb`
  * `$ sudo update-grub`
5. Reboot and enjoy

## Cleanup and other notes
* Installing the mainline kernel fixes numerous issues but has a few drawbacks:
  1. Need to periodically check for security updates to the mainline
     kernel
  2. Keep getting updates to the (unused) standard Ubuntu kernels.
    * Remove the standard kernels to fix this.

## References
* [http://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices/hp-chromebook-14](http://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices/hp-chromebook-14)
* [https://github.com/eyecreate/ubuntu-chromebook-installer](https://github.com/eyecreate/ubuntu-chromebook-installer)
* [https://wiki.archlinux.org/index.php/Chromebook](https://wiki.archlinux.org/index.php/Chromebook)
