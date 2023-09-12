+++
title = "Projects"
description = "Current and upcoming projects"
date = "2023-09-11"
aliases = ["projects","deveopment"]
author = "Nathan Byrd"
+++

Below is a list of current and possible upcoming projects. To be honest, I have more projects than time. So if you want to beat me to one of these projects please be my guest. Please drop me a note if you work on one of these, I'd love to chat with you about it.

## Software Projects ##

Please jump into these! I could use lots of help, I've linked Github repositories where appropriate.

### Enigma ½ BBS ###

I've been helping contribute tothe Enigma ½ BBS software. Thre are an almost unlimited number of things that can be done with this. A few of the things I've been focusing on:

* Terminal software compatibility, including 40 column mode, hunting down particular bugs, increasing ANSI / screen positioning compatibility, and maybe extending into Petscii, plain Ascii, Atascii, etc.
* Replace existing file transfer using external programs with internal implementations, to hopefully also squash some current bugs with file transfers.
* Implement JS Door support. This comes in several forms:
  * Javascript x86 engine to run doors without running external emulators
  * WASM compilation of C / etc open-source doors
  * Implement synchronet js door library support
* Implement graphics. Sixel, RIPscript, Videotex (with conversion between them,) maybe others

Level of effort: **varies**

### New MOO / MUD ###

Just an idea at this point, but I would love to see a new MOO / MUD software, similar to what was done for modern BBS systems. I've always been surprised that there has not been more work in this area already. Some ideas (random for now):

* Javascript / WASM programming by users. Small core, similar to MOO
* Web interface a must-have
* Integration with AI? Maybe ability to auto expand the world, etc, as well as to interpret commands in more fluid ways, etc.
* Integrated editor for objects, programming

Level of effort: **huge**

## New Hardware Projects ##

### Beepy ###

Hopefully I'm getting my [Beepy](https://beepy.sqfmi.com/) back soon, and I have a few projects in mind for it, including:

* Workaround for power issue that fried the last one
* Use an ESP32 instead of Raspberry Pi for the main processor to save power. Run circuitpython on both it and the rp2040.

Level of effort: **medium**

### CoCo 3 Becker Made Real ###

This is another slightly pie-in-the-sky type project. I'd love to see the Becker port that is used in emulators on the CoCo made "real" with a cartridge that uses a Raspberry Pi Pico to actually serve pydrivewire to implement all the functionality all on one card. It would be similar in vein to [PicoGUS](https://github.com/polpo/picogus) on the PC for example.

A couple of notes about this project:

* [PyDrivewire](https://github.com/n6il/pyDriveWire) already exists and could be used for this effort. However, it would need to be converted to work under circuitpython and to interface it with the hardware.
* ROM would be needed in order to load the initial OS - [this article](https://www.hackster.io/news/which-microcontroller-can-emulate-a-vintage-eprom-the-raspberry-pi-rp2040-748c76bae633) seems to suggest that this should be possible, even with circuitpython with supporting hardware.
* We need to use fast level shifters - look at 74lvc245 and similar

Level of effort: **high**

## Hardware Restoration Projects ##

Listing my current hardware restoration projects below. I'm not sure how anyone could work on any of these, so these are probably just for me. Let me know if you are interested in any of them however!

### DisplayPhone ###

I was lucky enough to find a [Nortel DisplayPhone](http://dunfield.classiccmp.org/disphone/), but unlucky enough to find a non-working one. Unfortunately, the internal battery leaked over the ribbon for the membrane keyboard. It also did not come with a power adapter. I was able to hack together a power adapter out of a ATX power supply, but am somewhat stuck with the keyboard. Unfortunately a replacement keyboard will be difficult if not impossible to find. So far I have scanned the membrane to make a circuit diagram of it, next I plan to try to get a flex-pcb printed and see if I can use that as a replacement. Another option may be to create an external keyboard and re-use the interface, though I'd rather not go that route if possible. The good news is that the display does come on, though without the keyboard no testing is possible beyond that.

Level of effort: **high**

### Osborne 1 ###

I happened across an Osborne 1 at a Hamfest a while back and picked it up for cheap. Luckly the system starts up and has a display, although the drive appears to be non-functional. I likely just need to work on the disk drive to get this one going.

Level of effort: **low**

### Tandy Color Computer 3 ###

Another system that I need to work on is a Tandy Color Computer 3 I picked up from Shop Goodwill a while back. Unfortunately it does not show any signs of life when powering on. I do have another working CoCo 3, so I do have a known good machine to compare with.

Level of effort: **unknown**

### RGB2HDMI ###

I'd like to get many of my retro machines setup to use the excellent [RGB2HDMI](https://github.com/hoglet67/RGBtoHDMI) project. In particular, I'd like to build a RGB2HDMI with an analog interface, and then setup cables off of individual machines with the analog cable to plug into it. That way I can take a retro machine off the shelf, plug it in and go. The challenge with this is to do the modifications to each machine without damaging them (trying not to add new holes or make non-reversible mods where possible.) The machines I'd like to get setup with this include:

* Tandy Color Computer 2
* Tandy MC-10
* TRS-80 Videotex Terminal
* Commodore 64
* Timex Sinclair 1000

Level of effort: **varies**

### Others ###

Other smaller hardware projects to do at some point:

* Powerbook G4 - fix bent hinge
* IBM Aptiva desktop - cleanup and minor repairs, check functioning
* IBM VGA monitor - Power light, no display, but feel static / hear flyback