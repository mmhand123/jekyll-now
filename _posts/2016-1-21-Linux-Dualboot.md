---
layout: post
title: Dual Booting Linux with Windows
---

## Some problems you might run into

A couple of months ago I decided to make the switch from Windows to Ubuntu for my development environmen. It was a lot easier than I thought it was going to be to set up dual booting Windows and Ubuntu, and there is a great guide that I followed at http://www.pcworld.com/article/2955460/operating-systems/dual-booting-linux-with-windows-what-you-need-to-know.html . However, I did run into a few problems that weren't brought up in that guide that I want to go into here.

The first problem was that even after I installed Ubuntu (and even though I installed it after Windows), when I rebooted my computer after installation it went straight back to Windows, with no option to go to Ubuntu. Thankfully, there's a very easy fix for this. All you need to do is reboot Ubuntu from your installation flash drive, this time choosing the Try Ubuntu option to go directly into the operating system from the flash drive. After that, go to the main Ubuntu website and download and run a program called Boot Repair. You should see something like this:

![An image of the Boot Repair software window]({{ site.baseurl }}/images/Boot Repair.png "Boot Repair")

After running that, you should be able to restart and then come across the boot loader screen that looks something like this and allows you to pick the operating system you want to boot:

![An image of the Boot Repair software window]({{ site.baseurl }}/images/Ubuntu boot loader.png "Boot Repair")
