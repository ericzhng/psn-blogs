---
layout: post
title: "Compare Cygwin, MinGW and WSL"
excerpt: "A ton of text to test readability."
categories: blog
tags: [Linux, WSL, Cygwin, MinGW]
image:
  feature: wsl-cygwin-mingw/wsl-cygwin-mingw.png
comments: true
share: true
date: 2019-07-25
---

This blog shows some differences among three alteratives to compile open source codes in Windows. 

<!--more-->

## Cygwin

* Cygwin makes porting Unix-based applications to Windows much easier, by emulating many of the small details that Unix-based operating systems provide, and are documented by the POSIX standards. Your application can use Unix feature such as pipes, Unix-style file and directory access, and so forth, and it can be compiled with Cygwin which will act as a compatibility layer around your application, so that many of those Unix-specific paradigms can continue to be used.

* You can compile codes in Cygwin, and it will run on Cygwin. If you distribute it along with the Cygwin runtime library (cygwin1.dll), you have to compile with its open source license.
	
* Cygwin applications by principle are not considered a “Native Win32 application” because it relies on the Cygwin POSIX Emulation DLL or cygwin1.dll for Posix functions and does not use win32 functions directly.
	
* From Cygwin's website: Cygwin is a Linux-like environment for Windows. It consists of two parts: A DLL (cygwin1.dll) which acts as a Linux API emulation layer providing substantial Linux API functionality; and a collection of tools which provide Linux look and feel.

## MinGW

* MinGW is simply a Windows port of the GNU compiler tools, such as GCC, Make, Bash, and so on. It does not attempt to emulate or provide comprehensive compatibility with Unix, but instead it provides the minimum necessary environment to use GCC (the GNU compiler) and a small number of other tools on Windows.
	
* MinGW does not have a Unix emulation layer like Cygwin. By default, code compiled in MinGW's GCC will compile to a native Windows X86 target, including .exe and .dll files, though you could also cross-compile with the right settings, since you are basically using the GNU compiler tools suite.

* MinGW is essentially an alternative to the Microsoft Visual C++ compiler and its associated linking/make tools. It may be possible in some cases to use MinGW to compile something that was intended for compiling with Microsoft Visual C++, with the right libraries and in some cases with other modifications.

* MinGW includes some basic standard libraries for interacting with the Windows operating system, but as with the normal standard libraries included in the GNU compiler collection these don't impose licensing restrictions on software you have created.

* Best option to port Linux codes to Windows native.
	
* MinGW on the other hand, provides functions supplied by the Win32 API. While porting applications under MinGW, functions not native to Win32 such as fork(), mmap(), or ioctl() will need to be reimplemented into Win32 equivalents for the application to function properly.
	
* In MinGW, the MSYS is a collection of GNU utilities such as bash, make, gawk and grep to allow building of applications. The problem is there’s no /usr directory psychically. The root (/) is considered as usr (/usr) path – so you cannot create one either. The problem arises while a program depends on third party library – there is no place to put this third party library so that the default search path can find the library file. Usually in linux /usr/local/lib is the default library search path. So the client program cannot configure with ”./configure”. You will need special modification on LIBRARY_PATH environment variable which is very tedious and cumbersome. So to run the program which needs lots of dependency on other libraries, I would prefer Cigwin over minGW.
	
* You can also get a small UNIX/POSIX like environment, compiled with MinGW called MSYS. It doesn't have anywhere near all the features of Cygwin, but is ideal for programmers wanting to use MinGW.

* From Mingw's website: MinGW ("Minimalistic GNU for Windows") is a collection of freely available and freely distributable Windows specific header files and import libraries combined with GNU toolsets that allow one to produce native Windows programs that do not rely on any 3rd-party C runtime DLLs

* MinGW is higher performance than Cygwin, but it's also 32-bit which may be a problem with your applications. There is a 64-bit environment similar to MinGW but it's a different project.

* MinGW-w64 is in all senses the successor to MinGW.org's version. They provide 32 and 64 bit compilers, along with some arm support as well.

## WSL

* WSL is a real Linux kernel built on a lightweight VM.
	
* There is a separate post talking about how to setup Linux subsystem in Windows, please find it within this website.


Reference:
------
* 1. [Cygwin vs. MinGW – What to Prefer When](https://www.codeproject.com/Articles/472809/Cygwin-vs-MinGW-What-to-Prefer-When)

* 2. [What is the difference between Cygwin and MinGW?](https://stackoverflow.com/questions/771756/what-is-the-difference-between-cygwin-and-mingw)

* 3. [Targeting the Windows Subsystem for Linux from Visual Studio
](https://devblogs.microsoft.com/cppblog/targeting-windows-subsystem-for-linux-from-visual-studio/)
