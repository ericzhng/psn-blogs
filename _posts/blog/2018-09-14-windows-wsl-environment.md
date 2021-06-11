---
layout: post
title: "Setup Linux environment (WSL) in Windows"
modified:
categories: blog
excerpt:
tags: [Windows, WSL]
image:
  feature: wsl-cygwin-mingw/wsl.png
date: 2018-09-14
comments: true
share: true
---

In this blog, I want to talk about how to setup Ubuntu environment (WSL) in Windows 10 system, where you can run Linux programs.

<!--more-->

## 1. Setup Linux subsystem in Windows 10

* In Windows 10, go to Settings -> Update & Security -> For Developers, select Developer Mode under "Use developer features".
* Navigate to Control Panel -> Programs and Features, Click "Turn Windows features on or off", and toggle "Windows Subsystem for Linux" to on and click OK to return.
* Restart your computer to take effects.
* After restart, open Bash by searching it in search box, and type "y" to install the linux subsystem.
  >Note that sometimes you will be prompted to go to Microsoft Store to download and install it, then choose ubuntu in the store and click "Get" to download and install.*
* Create a user name and password for an account.
* If everything goes successfully, you should be able to run common linux commands such as `clear` and `ls` in the Bash.

## 2. Install necessary libraries in WSL
* Open Bash in Windows 10, and update our repo lists and packages
  - `sudo apt-get update -y`
  - `sudo apt-get upgrade -y`

Reference:
------
* 1. [How to Enable the Linux Bash Shell in Windows 10](https://www.laptopmag.com/articles/use-bash-shell-windows-10).
