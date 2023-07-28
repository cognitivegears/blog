+++
author = "Nathan Byrd"
title = "Archiving floppies to the Internet Archive - Part 1"
date = "2023-07-25"
showFullContent=false
readingTime = true
description = "Protect the past by backing up physical media to the web using Greaseweazle and the Internet Archive as a method of digital preservation."
tags = [
    "greaseweazle",
    "floppy",
    "preservation",
]
+++

## Introduction

Today we are going to talk about using Greaseweazle and the Internet Archive to back up old programs. With a reasonably inexpensive setup it is possible for hobbyists to own a near-professional floppy archiving system as well as upload backups for digital preservation. We'll explore the setup and use of this software while backing up and preserving an example program.

<!-- more -->

## Challenge

{{< imgwrap src="disks.jpg" alt="Image of disks" >}}
A while back on [Shop Goodwill](https://shopgoodwill.com) I ran across a copy of an old utility from Berkeley Systems, Star Trek Stardate, a themed version of the Expresso calendar/address book/todo list program for Windows 3.1+. Intrigued, I did a quick search online for it. To my suprise, I was not able to find hardly any information on the web, and absolutely no download links for the program itself. So I bid, and won the auction.

_Side note: I know why everyone waits until the last minute to bid on items there, but I wish everyone would just bid their max when they find the item and leave it at that, losing items at the last minute is so disheartening._

After I received the Stardate utility, however, I was at a little bit of a loss about how to back it up. While I have several computers from the time period and a modern machine I could run an emulator on, I didn't have a great way to faithfully back up the source material. Even worse, the disks themselves seemed to have errors and were not reading consistently.

I decided it was time to try out an open-source project that I had heard about some time ago, the oddly-named Greaseweazle.

## Greaseweazle

A [Greaseweazle](https://github.com/keirf/greaseweazle) is not, as you might imagine, a rodent* covered in oil. Instead it is an open-source project from [Keir Fraser](https://github.com/keirf). As the [GitHub repository](https://github.com/keirf/greaseweazle) describes it, it is "tools for accessing a floppy drive at the raw flux level." In other words, it performs low-level access of floppy drives in order to read and write data that would otherwise be difficult to access. Sounds interesting, right? Let's get it setup.

\* also, a weazle isn't a rodent

### setup

The setup of Greaseweazle is split into two parts, software and hardware. This guide will be setting up Greaseweazle v4, as that is the version of the board that I have. More information is available on the repository as well if you are using a different configuration.

#### The hardware

{{< imgwrap src="setup.jpg" alt="Image of disks" >}}
First, we need to procure a Greaseweazle. You can build your own Greaseweazle via the [Design Files](https://github.com/keirf/greaseweazle/wiki/Design-Files), but most people will likely prefer to [Purchase](https://github.com/keirf/greaseweazle/wiki/Purchase-a-Greaseweazle) one instead. As of time of this writing in the US one can be had for about $30 plus shipping.

In addition to the Greaseweazle v4 itself, you will also need a few additional items:

* floppy drive(s)
* matching floppy cables
* USB-A to USB-B cable
* maybe a power supply (see below)

Which type of floppy drive you get depends on the media you are looking to back up. The Greaseweazle can handle some very odd hardware (even 8" disks with an adapter!) In my case, I only needed to back up a 3.5" drive, so it wasn't too hard to get ahold of one for this. As to the power supply, there is a header on the Greaseweazle to supply power, though that won't work with all drives. In my case I decided to play it safe and go with an external power supply. At first I just used an old ATX power supply I had laying around (jumpered to run,) but replaced it with a simple power supply from Amazon** (search for "molex power supply" to find one that will work.) In either case you may need a molex to 3.5" power adapter as well.

\*\* Note: I don't generally recommend Amazon. I prefer to shop with smaller stores when possible but in this case it was the easiest way to find one quickly. The drive cable and molex to 3.5" adapter I bought from a local computer / electronics supply store, but in a pinch those can be had from Amazon as well.

#### The software

This part is super easy, just follow the installation instructions from the [GitHub repo](https://github.com/keirf/greaseweazle). I installed it on my laptop running Linux, though I have plans someday to see if I can get it running on a Raspberry Pi Zero, I think it would be fun to house both of them in a single enclosure with a web interface or something, but for now I just kept it simple. For my case the following command was all I needed:

```$ python3 -m pip install git+https://github.com/keirf/greaseweazle@latest```

## Conclusion

That's all for now. In the next post I'll discuss how to run Greaseweazle and upload the result to the Internet Archive.
