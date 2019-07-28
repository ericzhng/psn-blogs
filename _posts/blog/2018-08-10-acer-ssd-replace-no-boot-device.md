---
layout: post
title: 'Laptop SSD "No Bootable Device"!'
categories: blog
excerpt:
tags: [Hardware]
image: 
  feature: hardware/acer-no-boot-device.jpg
date: 2018-08-10
comments: true
share: true
---

When you got a new SSD drive and want to use it for operating system on a laptop. Later on you install the SSD, there was such an error showing "No Bootable Device". You panic!

<!--more-->

Don't worry, in this case, it is probably because you are in the wrong Boot mode.

As soon as your computer starts, press F12 or F2 to reach BIOS. Go to Boot tab and change your UEFI/BOIS Boot Mode from UEFI to Legacy. For normal SATA hard drives, it is OK to be in UEFI mode, but for SSD, in order for it to boot normally, you have to go back to Legacy mode. After this, restart and the computer's operating system should turn on and run normally.
