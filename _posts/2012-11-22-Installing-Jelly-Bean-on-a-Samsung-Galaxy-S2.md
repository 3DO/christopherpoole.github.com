---
layout: minimal_post
title: Installing Jelly Bean on a Samsung Galaxy S2
comments: True
introduction: I have a Samsung Galaxy S2 (GT-I9100T) running VodafoneAU Android ICS and associated VodafoneAU crapware. As it turns out, rooting and installing the CyanogenMod flavour of Android Jelly Bean from Linux is rather straight forwards.
---

*NO WARRANTY*

Following are the exact steps that I took which resulted in [CyanogenMod](http://www.cyanogenmod.org/) [Android Jelly Bean](http://www.android.com/about/jelly-bean/) running on my device; you should do your own research before trying this yourself. 
Remember to backup everything on your phone if it is important to you.

## Flashing the Kernel
Firstly you require [Heimdall](https://github.com/Benjamin-Dobell/Heimdall) for flashing Samsung Galaxy S class devices from Linux, which you will need to compile from source.
At the `autoconf` stage, the required dependencies (if any) will become apparent - install them.

    git clone https://github.com/Benjamin-Dobell/Heimdall.git
    cd Heimdall/
    ./configure
    make
    sudo make install

Next you need to acquire an appropriate kernel and flash it to your device.
I used [this one](http://forum.xda-developers.com/showthread.php?t=1118693), and followed the steps described on the same page:

1. Turn device off
2. Restart in 'Download Mode' with volume down/home/power
3. Connect USB cable between device and computer
4. Flash kernel: `heimdall flash --6 zImage`
5. Restart device
6. Disconnect USB cable

## Installing the new OS
This bit is easy, I used [these instructions](http://forum.xda-developers.com/showthread.php?t=1794758) as a guide.
Download the [CyanogenMod 10 nightly build](http://www.get.cm/?device=i9100) for the Samsung Galaxy S2 as well as the corresponding CyanogenMod 10 [Google Apps](http://goo.im/gapps) package.
Put your phone in USB mass storage mode, and copy the 2 zip files to the SD card.

1. Turn device off
2. Restart in 'Recovery Mode' with volume up/home/power
3. Navigate to the 2 zip files and confirm installation
4. Perform a factory reset
5. Restart device

## Annoyances
- When I first signed in, all apps that I have installed previously started syncing automatically.
- On the S2 boot splash there is a nice new exclamation mark in a yellow triangle; apparently this can be removed, but I do not really care.
