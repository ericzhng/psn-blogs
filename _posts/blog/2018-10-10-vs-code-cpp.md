---
layout: post
title: "Setup vs-code for C/C++ in Windows 10"
modified:
categories: blog
excerpt:
tags: [Windows, vs-code, WSL]
image:
  feature: vscode/vscode_cpp.png
date: 2018-10-10
comments: true
share: true
---

Visual Studio Code (vs-code) is a very light and convenient IDE for programming using C/C++, Python and so many other languages. Thus in this blog, I want to show users how to setup **vs-code** for C/C++ programming using Linux subsystem in Windows 10. The subsystem is usually referred to as Windows Subsystem for Linux (WSL). 

<!--more-->

## Introduction

I've started using vs-code long time ago, first in Ubuntu, then in Windows. But I've never actually debugged C/C++ code in Windows using vs-code, mainly because there isn't a C/C++ compiler free of charge provided in Windows, and usually you have to configure a virtual machine to run Linux to debug/run C/C++ program in Windows.

There are some major steps you need to take in order to run/debug C/C++ code using vs-code in Windows 10. Please follow steps provided below.

### 1. Enable Linux Bash shell in Windows 10

Please refer to my post titled "Setup Linux environment (WSL) in Windows" for more details.

### 2. Install vs-code in Windows 10

* Downloading newest version vs-code [here](https://code.visualstudio.com/).

* Install it in Windows 10.

* After installation, you probably want to install a few extensions for C/C++ programming as well. Here is a list of possible extensions you might want to use.
	`C/C++`
	`C/C++ Intellisense`

* The [official website](https://code.visualstudio.com/docs/languages/cpp) contains some pretty good tutorials where you can learn configuring vs-code. 

### 3. Debug and run C/C++ code in vs-code

* Create a new folder named **test-cpp-vs-code**, and use vs-code to open the folder. You can create a test.cpp file in vs-code and copy the following code:
```
	#include <stdio.h>
	#include <math.h>
	#include <iostream>

	int main() {
		char strName[] = "Eric";
		std::cout<< "Hello" << strName << std::endl;
		return 0;
	}
```

* Next step, setting up configuration files for vs-code.

- IntelliSense: generate a `c_cpp_properties.json` file by running **C/Cpp: Edit configurations** command from the Command Palette (Ctrl+Shift+P) and add missing include header directories.

- Build your code: create a `tasks.json` file by running **Tasks: Configure Tasks** comand in Command Palette, add the compiler information and tasks. To build the prject, run **Tasks: Run Build Tasks** (Ctrl+Shift+B).

- Debug your code: generate a `launch.json` file, by going to Debug view, click the configure icon and then select C++ (Windows) from teh Select Environment dropdown.

- Some common shortcuts: 

 | Functions | Shortcuts |
 |-------|-------|
 |Format document    | **Shift+Alt+F** or **Ctrl+K/Ctrl+F**|
 |Search for symbols | **Ctrl+Shift+O**|
 | Go to definition  | **F12**|
 |Build the project  | **Ctrl+Shift+B**|

- You can refer to my GitHub repository for [sample source code](https://github.com/ericzhng/test-vs-code-windows-subsysytem-linux). I've also attached the configuration files for vs-code, so you can have a glimpse.


## Intellise configuration:
* Refer to file **c_cpp_properties.json**.

```
{
    "configurations": [
        {
            "name": "WSL",
            "intelliSenseMode": "gcc-x64",
            "compilerPath": "/usr/bin/gcc",
            "includePath": [
                "${workspaceFolder}/**",
                "${localappdata}/Packages/CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc/LocalState/rootfs/usr/include/c++/5",
                "${localappdata}/Packages/CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc/LocalState/rootfs/usr/include/x86_64-linux-gnu/c++/5",
                "${localappdata}/Packages/CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc/LocalState/rootfs/usr/include/c++/5/backward",
                "${localappdata}/Packages/CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc/LocalState/rootfs/usr/lib/gcc/x86_64-linux-gnu/5/include",
                "${localappdata}/Packages/CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc/LocalState/rootfs/usr/local/include",
                "${localappdata}/Packages/CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc/LocalState/rootfs/usr/lib/gcc/x86_64-linux-gnu/5/include-fixed",
                "${localappdata}/Packages/CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc/LocalState/rootfs/usr/include/x86_64-linux-gnu",
                "${localappdata}/Packages/CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc/LocalState/rootfs/usr/include"
            ],
            "defines": [
                "__linux__",
                "__x86_64__"
            ],
            "browse": {
                "path": [
                    "${localappdata}/Packages/CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc/LocalState/rootfs/usr/include/c++/5",
                    "${localappdata}/Packages/CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc/LocalState/rootfs/usr/include/x86_64-linux-gnu/c++/5",
                    "${localappdata}/Packages/CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc/LocalState/rootfs/usr/lib/gcc/x86_64-linux-gnu/5/include",
                    "${localappdata}/Packages/CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc/LocalState/rootfs/usr/local/include",
                    "${localappdata}/Packages/CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc/LocalState/rootfs/usr/lib/gcc/x86_64-linux-gnu/5/include-fixed",
                    "${localappdata}/Packages/CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc/LocalState/rootfs/usr/include/x86_64-linux-gnu",
                    "${localappdata}/Packages/CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc/LocalState/rootfs/usr/include/*"
                ],
                "limitSymbolsToIncludedHeaders": true,
                "databaseFilename": ""
            },
            "cStandard": "c11",
            "cppStandard": "c++17"
        }
    ],
    "version": 4
}
```
 
### Tasks configuration: refer to file **tasks.json**.

```
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "command": "bash",
    //"runner": "terminal",
    "tasks": [
        {
            "label": "build",
            "type": "shell",
            "command": "g++ -g test.cpp -o maintest.out && echo 'success!'",
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "problemMatcher": []
        },
        {
            "label": "run",
            "type": "shell",
            "command": "./maintest.out",
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "problemMatcher": []
        }
    ]
}

```

### Debug configuration: refer to file **launch.json**.

```
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(gdb) Bash on Windows Launch",
            "type": "cppdbg",
            "request": "launch",
            "program": "./maintest.out",
            "args": [],
            "stopAtEntry": false,
            // NOTE: you have to specify explicitly the location of files
            "cwd": "/mnt/e/Repos/MyRepos/test-vs-code-windows-subsysytem-linux",
            "environment": [],
            "externalConsole": true,
            "windows": {
                "MIMode": "gdb",
                "setupCommands": [
                    {
                        "description": "Enable pretty-printing for gdb",
                        "text": "-enable-pretty-printing",
                        "ignoreFailures": true
                    }
                ]
            },
            "pipeTransport": {
                "debuggerPath": "/usr/bin/gdb",
                "pipeProgram": "c:\\Windows\\WinSxS\\amd64_microsoft-windows-lxss-bash_31bf3856ad364e35_10.0.17134.1_none_251beae725bc7de5\\bash.exe",
                "pipeArgs": ["-c"],
                "pipeCwd": ""
            },
            "sourceFileMap": {
                "/mnt/c": "c:\\",
                "/mnt/e": "e:\\"
            }
        }
    ]
}
```

## Common errors

Sometimes after you specified everything above, you might come to some errors shown below:

- ![image missing](pycharm/error.png) **Commands not found!**
  * **Reason**: When running the build or run, you are executing in **Windows command prompt**, which doesn't have a compiler installed. The **gcc** compiler is installed in Linux subsystem, so you should refer to **bash** to run the build command.
  * **Solution**: 
    * Open settings in vs-code, using the keyboard shortcut `CTRL+,`, or File → Preferences → Settings. 
    * Search for `terminal.integrated.shell.windows`, use your bash.exe path to substitute the original exe path.
    * For me, it is `C:\Windows\WinSxS\amd64_microsoft-windows-lxss-bash_31bf3856ad364e35_10.0.17134.1_none_251beae725bc7de5/bash.exe`. 
    * Then re-run your code, using shortcut **CTRL+SHIFT+B**, you should have the compiler running in WSL bash now.

## Reference
------

* 1. [Configure complier path using Windows Subsystem for Linux](https://github.com/Microsoft/vscode-cpptools/blob/master/Documentation/LanguageServer/Windows%20Subsystem%20for%20Linux.md).
* 2. [Windows 10's Windows Subsystem for Linux](https://github.com/Microsoft/vscode-cpptools/blob/master/Documentation/Debugger/gdb/Windows%20Subsystem%20for%20Linux.md).
