---
layout: post
title: Dual Booting Linux with Windows
---

## Potential Pitfalls

A couple of months ago I decided to make the switch from Windows to Ubuntu for my development environmen. It was a lot easier than I thought it was going to be to set up dual booting Windows and Ubuntu, and there is a [great guide that I followed](http://www.pcworld.com/article/2955460/operating-systems/dual-booting-linux-with-windows-what-you-need-to-know.html). However, I did run into a few problems that weren't brought up in that guide that I want to go into here.

The first problem was that even after I installed Ubuntu (and even though I installed it after Windows), when I rebooted my computer after installation it went straight back to Windows, with no option to go to Ubuntu. Thankfully, there's a very easy fix for this. All you need to do is reboot Ubuntu from your installation flash drive, this time choosing the Try Ubuntu option to go directly into the operating system from the flash drive. After that, go to the main Ubuntu website and download and run a program called Boot Repair. You should see something like this:



![An image of the Boot Repair software window]({{ site.baseurl }}/images/Boot Repair.png "Boot Repair")

After running that, you should be able to restart and then come across the boot loader screen that looks something like this and allows you to pick the operating system you want to boot:



![An image of the grub boot loader window]({{ site.baseurl }}/images/Ubuntu boot loader.png "Boot Load Screen")


Another issue that I ran into was that every so often my computer would freeze and I wouldn't be able to do anything expect move the mouse (often triggered by opening a Chrome tab). I discovered that this was due to having a dedicated graphics card for my computer, and that I needed to switch from the default graphics drivers to proprietary drivers developed by NVIDIA. You can go to their website and follow their instructions to download a driver, but there is fortunately a much better way!

Just go to System Settings and select Sofware & Updates:



![An image of the system settings window]({{ site.baseurl }}/images/Settings.png "System settings")

Then tab over to additional drivers, and you should see your graphics card listed with several different drivers. At first, the X.Org driver was selected, which I changed to the most recent NVIDIA proprietary driver for my card:



![An image of the driver settings window]({{ site.baseurl }}/images/Drivers.png "Driver settings")


After that, just restart the computer and you should be crash free!


The final problem that I ran into was when I was trying to install software, like Skype, that only have a 32-bit version for download on Ubuntu. I was running into a problem where it kept telling me I wasn't connected to the internet when I clearly was. The problem turned out to be a missing 32-bit ssl library that Skype needed for authentication. Thankfully this too was an easy fix, I just ran the following on the command line:

```
sudo apt-get install libssl:i386

```

