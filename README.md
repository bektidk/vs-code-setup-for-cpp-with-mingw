# Visual Studio Code Setup for C++ with MinGW

This repository provides a guide for setting up Visual Studio Code (VS Code) for C++ development using MinGW as the compiler.

## Table of Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Setup Instructions](#setup-instructions)
- [Configuration](#configuration)
- [Additional Resources](#additional-resources)

## Introduction

Setting up Visual Studio Code for C++ development involves installing and configuring the necessary tools and extensions. This guide will walk you through the steps to configure VS Code with MinGW, a popular compiler for C++ development on Windows.

## Prerequisites

Before you start, make sure you have the following installed:

1. **Visual Studio Code**: [Download and install VS Code](https://code.visualstudio.com/)
2. **MinGW**: [Download and install MinGW](https://sourceforge.net/projects/mingw/)

## Setup Instructions

1. **Install Visual Studio Code**
   - Follow the [official instructions](https://code.visualstudio.com/docs/setup/setup-overview) to install VS Code on your system.

2. **Install MinGW**
   - Download and install MinGW from [SourceForge](https://sourceforge.net/projects/mingw/).
   - Add the `bin` directory of MinGW to your system's PATH environment variable. This typically involves adding a path like `C:\MinGW\bin` to the PATH variable.

3. **Install Required Extensions in VS Code**
   - Open VS Code and navigate to the Extensions view (`Ctrl+Shift+X`).
   - Install the following extensions:
     - **C/C++** by Microsoft
     - **Code Runner** (optional, for running code snippets quickly)

## Configuration

1. **Configure `tasks.json`**
   - Create a `tasks.json` file in the `.vscode` directory of your project to define build tasks.
   - Example configuration:

     ```json
     {
       "version": "2.0.0",
       "tasks": [
         {
           "label": "Build",
           "type": "shell",
           "command": "g++",
           "args": [
             "-g",
             "${file}",
             "-o",
             "${fileDirname}/${fileBasenameNoExtension}.exe"
           ],
           "group": {
             "kind": "build",
             "isDefault": true
           },
           "problemMatcher": ["$gcc"]
         }
       ]
     }
     ```

2. **Configure `launch.json`**
   - Create a `launch.json` file in the `.vscode` directory to set up debugging configurations.
   - Example configuration:

     ```json
     {
       "version": "0.2.0",
       "configurations": [
         {
           "name": "Debug C++",
           "type": "cppdbg",
           "request": "launch",
           "program": "${fileDirname}/${fileBasenameNoExtension}.exe",
           "args": [],
           "stopAtEntry": false,
           "cwd": "${workspaceFolder}",
           "environment": [],
           "externalConsole": false,
           "MIMode": "gdb",
           "setupCommands": [
             {
               "description": "Enable pretty-printing for gdb",
               "text": "-enable-pretty-printing",
               "ignoreFailures": true
             }
           ],
           "preLaunchTask": "Build",
           "miDebuggerPath": "C:/MinGW/bin/gdb.exe",
           "internalConsoleOptions": "openOnSessionStart",
           "logging": {
             "engineLogging": true
           }
         }
       ]
     }
     ```

## Additional Resources

For more detailed instructions on configuring MinGW with Visual Studio Code, refer to the [official documentation](https://code.visualstudio.com/docs/cpp/config-mingw).
