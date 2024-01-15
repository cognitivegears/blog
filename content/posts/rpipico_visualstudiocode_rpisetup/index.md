+++
author = "Nathan Byrd"
title = "Visual Studio Code Setup - Pico Development"
date = "2024-01-15"
showFullContent=false
readingTime = true
description = "Easy setup for getting started with developing for Rasperry Pi Pico"
tags = [
    "rasperrypi",
    "development",
    "pico",
    "visualstudiocode",
]
+++

## Introduction

A somewhat belated Happy New Year to everyone! This is my first post of the year getting back into things. This one is a little different as it isn't directly retro computer related, but rather development focused. Ultimately this is for a retro project, but not one I'm quite ready to talk about yet. In the meantime, below is a bit of information about how I setup the development environment to code for a Rasperry Pi Pico.

<!-- more -->

## Overview

Rasperry Pi makes a fantastic [Getting Started](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf) guide available, along with an _excellent_ script for getting started on a Rasperry Pi to build Rasperry Pi Pico firmware from a Rasperry Pi device (the article lists Rasperry Pi 4B and 400, but I ran it on my new Rasperrry Pi 5 with no issues as well.) To get setup, all you have to do is run a couple of commands!


## Problem

This is great, but I didn't want to have to hook a monitor and keyboard to a Raspberry Pi and use that exclusively for development. It's much more comfortable to use my laptop for this kind of coding. The setup instructions for this, however, are much more involved and frankly I couldn't be bothered. There is an easier way, however.

## Solution

Enter one of my favorite extensions for Visual Studio Code, `Remote - SSH`. This extension allows you to treat a remote machine almost exactly the same as if it were local. In this case, I used my new Rasperry Pi 5 running headless, and I can connect to it over `Remote - SSH` from one of my other computers to do the actual development. At the same time, I can even still connect the Rasperry Pi to the Pico and perform remote debugging, etc.

## Steps

First, you need to setup your Rasperry Pi and configure SSH. I'm not going to go into too much detail here as there are many great guides on how to do this, but one thing to note is that I did setup ssh keys for the machines I normally use to talk to it for ease of connecting.

For now I'm only using the computer off my local network, but if you want to have it available remote something like [ngrok](https://ngrok.com/) or [tailscale](https://tailscale.com/)

Second, after finishing the Rasperry Pi setup, update packages via `sudo apt update && sudo apt upgrade` and then run the following commands to install the Pico C SDK support:

```console
$ wget https://raw.githubusercontent.com/raspberrypi/pico-setup/master/pico_setup.sh
$ chmod +x pico_setup.sh
$ ./pico_setup.sh
```

Third, in Visual Studio Code, install the extensions for SSH. I recommend the following extensions:
* Remote - SSH: Editing Configuration Files (ms-vscode-remote.remote-ssh-edit)
* Remote Explorer (ms-vscode.remote-explorer)
* Remote - SSH (ms-vscode-remote.remote-ssh)

Fourth, connect to the SSH host. Open up the command palette (Control-Shift-P or F1) and find `Remote-SSH: Add New SSH Host` (on mine, typing `newssh` finds this quickly) and press enter. Enter the command for connecting to your pi, something like `ssh pi@rasperrypi -A` where `pi` is the username to connect as and `rasperrypi` is the host name or IP address to connect to.

To connect to the host, from the command palette find `Remote-SSH: Connect to Host` (i.e. `sshconn`) and connect to the host you setup. Then use Open Folder to open up the `pico/pico-examples` folder.

Finally, setup the remote extensions for working with the Rasperry Pi Pico. I used the following:

* C/C++ Extension Pack (ms-vscode.cpptools-extension-pack)
* CMake (twxs.cmake)
* Cortex Debug (marus25.cortex-debug)
* debug-tracker-vscode (mcu-debug.debug-tracker-vscode)
* MemoryView (mcu-debug.memory-view)
* Peripheral Viewer (mcu-debug.peripheral-viewer)
* RTOS Views (mcu-debug.rtos-views)

## Conclusion

That's it, if everything worked you should have a fully functional Raspberry Pi Pico setup with a minimum of fuss. This makes for a simple setup while still allowing a lot of flexibility. Please let me know if you have any questions or following this guide. Thanks!
