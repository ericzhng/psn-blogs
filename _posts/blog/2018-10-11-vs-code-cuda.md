---
layout: post
title: "Enable CUDA C/C++ support in vs-code in Windows 10"
modified:
categories: blog
excerpt:
tags: [Windows, vs-code, WSL, cuda]
image:
  feature: vscode/vscode-cuda.png
date: 2018-10-11
comments: true
share: true
---

In this blog, I want to show users how to set up vs-code for CUDA C/C++ code in Windows 10.

<!--more-->

## Introduction

I've been working on cuda programming in Visual Studio, which can be set up easily. However, since I play with vs-code, I would like to use vs-code for cuda as well. So In this blog, I want to show users how to set up vs-code for cuda in Windows.

There are some major steps you need to take, in order to run/debug cuda code using vs-code.
 0. (Optional, if done already) Enable Linux Bash shell in Windows 10 and install vs-code in Windows 10.
 1. Download the extension in vs-code: vscode-cudacpp. It is mainly for syntax and snippets.
 2. Download the [sample code](https://github.com/ericzhng/test-cuda-vs-code) from my GitHub repository. 
 3. Press Ctrl+Shift+B in vs-code, choose build to compile the code. Choose run to run the executable.
 4. Currently it is not able to enable cuda-debugger for cuda in vs-code in Windows. If you were to do everything in bash, then there might be a possibility to configure cuda-debugger.
 5. But it is OK to use Windows C/C++ debugger, to only debug CPU code.

 **c_cpp_properties.json**
 
 ```
{
    "configurations": [
        {
            "name": "Linux",
            "includePath": [
                "${workspaceRoot}",
                "/usr/include",
                "/usr/local/include"
            ],
            "defines": [],
            "browse": {
                "path": [
                    "/usr/include",
                    "/usr/local/include",
                    "${workspaceRoot}"
                ],
                "limitSymbolsToIncludedHeaders": true,
                "databaseFilename": ""
            },
            "intelliSenseMode": "clang-x64"
        },
        {
            "name": "Win32",
            "includePath": [
                "${workspaceRoot}",
                "C:/Program Files (x86)/Microsoft Visual Studio/2017/Community/VC/Tools/MSVC/14.10.25017/include/*",
                "C:/Program Files (x86)/Windows Kits/10/Include/10.0.15063.0/um",
                "C:/Program Files (x86)/Windows Kits/10/Include/10.0.15063.0/ucrt",
                "C:/Program Files (x86)/Windows Kits/10/Include/10.0.15063.0/shared",
                "C:/Program Files (x86)/Windows Kits/10/Include/10.0.15063.0/winrt",
                "C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v9.1/include",
                "C:/Program Files (x86)/Microsoft Visual Studio 12.0/VC/bin"
            ],
            "defines": [
                "_DEBUG",
                "UNICODE"
            ],
            "browse": {
                "path": [
                    "C:/Program Files (x86)/Microsoft Visual Studio/2017/Community/VC/Tools/MSVC/14.10.25017/include/*",
                    "C:/Program Files (x86)/Windows Kits/10/Include/10.0.15063.0/um",
                    "C:/Program Files (x86)/Windows Kits/10/Include/10.0.15063.0/ucrt",
                    "C:/Program Files (x86)/Windows Kits/10/Include/10.0.15063.0/shared",
                    "C:/Program Files (x86)/Windows Kits/10/Include/10.0.15063.0/winrt",
                    "C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v9.1/include",
                    "C:/Program Files (x86)/Microsoft Visual Studio 12.0/VC/bin",
                    "${workspaceRoot}"
                ],
                "limitSymbolsToIncludedHeaders": true,
                "databaseFilename": ""
            },
            "intelliSenseMode": "msvc-x64"
        }
    ],
    "version": 4
}
 ```
 
 **tasks.json**
 
 ```
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "echoCommand": true,
    "tasks": [
        {
            "label": "build",
            "command": "nvcc",
            "args": ["-g", "-o", "maintest.exe", "src/hellocuda.cu"],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "problemMatcher": []
        },
        {
            "label": "run",
            "command": "./maintest.exe",
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "problemMatcher": []
        }
    ]
}
 ```
 
 
 **launch.json**
 
 ```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(Windows) Launch",
            "type": "cppvsdbg",
            "request": "launch",
            "program": "${workspaceFolder}/maintest.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": true
        }
    ]
}
 ```
<!-- 
 
Reference:
------
* [1] []().
 -->
