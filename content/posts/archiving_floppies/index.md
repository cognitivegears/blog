+++
author = "Nathan Byrd"
title = "Archiving floppies to the Internet Archive"
date = "2023-07-25"
showFullContent=false
readingTime=true
description = "Protect the past by backing up physical media to the web using Greaseweazle and the Internet Archive as a method of digital preservation."
tags = [
    "greaseweazle",
    "floppy",
    "preservation",
]
+++

# Introduction
Today we are going to talk about using Greaseweazle and the Internet Archive to back up old programs. With a reasonably inexpensive setup it is possible for hobbyists to own a near-professional floppy archiving system as well as upload backups for digital preservation. We'll explore the setup and use of this software while backing up and preserving an example program.

<!-- more -->


# Challenge

{{< imgwrap src="disks.jpg" alt="Image of disks" >}}
A while back on [Shop Goodwill](https://shopgoodwill.com) I ran across a copy of an old utility from Berkeley Systems, Star Trek Stardate, a themed version of the Expresso calendar/address book/todo list program for Windows 3.1+. Intrigued, I did a quick search online for it. To my suprise, I was not able to find hardly any information on the web, and absolutely no download links for the program itself. So I bid, and won the auction. After I received it, however, I was at a little bit of a loss about how to back it up. While I have several computers from the time period and a modern machine I could run an emulator on, I didn't have a great way to faithfully back up the source material. Even worse, the disks themselves seemed to have errors and were not reading consistently.

I decided it was time to try out an open-source project that I had heard about some time ago, the oddly-named Greaseweazle.

# Greaseweazle

A [Greaseweazle](https://github.com/keirf/greaseweazle) is not, as you might imagine, a rodent* covered in oil. Instead it is an open-source project from [Keir Fraser](https://github.com/keirf). As the [GitHub repository](https://github.com/keirf/greaseweazle) describes it, it is "tools for accessing a floppy drive at the raw flux level." In other words, it performs low-level access of floppy drives in order to read and write data that would otherwise be difficult to access. Sounds interesting, right? Let's get it setup.

\* also, a weazle isn't a rodent

## setup

The setup of Greaseweazle is split into two parts, software and hardware. This guide will be setting up Greaseweazle v4, as that is the version of the board that I have. More information is available on the repository as well if you are using a different configuration.

### The hardware

{{< imgwrap src="setup.jpg" alt="Image of disks" >}}
First, we need to procure a Greaseweazle. You can build your own Greaseweazle via the [Design Files](https://github.com/keirf/greaseweazle/wiki/Design-Files), but most people will likely prefer to [Purchase](https://github.com/keirf/greaseweazle/wiki/Purchase-a-Greaseweazle) one instead. As of time of this writing in the US one can be had for about $30 plus shipping.

In addition to the Greaseweazle v4 itself, you will also need a few additional items:

* floppy drive(s)
* matching floppy cables
* USB-A to USB-B cable
* maybe a power supply (see below)

Which type of floppy drive you get depends on the media you are looking to back up. The Greaseweazle can handle some very odd hardware (even 8" disks with an adapter!) In my case, I only needed to back up a 3.5" drive, so it wasn't too hard to get ahold of one for this. As to the power supply, there is a header on the Greaseweazle to supply power, though that won't work with all drives. In my case I decided to play it safe and go with an external power supply. At first I just used an old ATX power supply I had laying around (jumpered to run,) but replaced it with a simple power supply from Amazon** (search for "molex power supply" to find one that will work.) In either case you may need a molex to 3.5" power adapter as well.

\*\* Note: I don't generally recommend Amazon, I prefer to shop with smaller stores when possible but in this case it was the easiest way to find one quickly. The drive cable and molex to 3.5" adapter I bought from a local computer / electronics supply store, but in a pinch those can be had from Amazon as well.


### The software

This part is super easy, just follow the Installation instructions from the [GitHub repo](https://github.com/keirf/greaseweazle). I installed it on my laptop running Linux, though I have plans someday to see if I can get it running on a Raspberry Pi Zero, I think it would be fun to house both of them in a single enclosure with a web interface or something, but for now I just kept it simple. For my case the following command was all I needed:

```$ python3 -m pip install git+https://github.com/keirf/greaseweazle@latest```


## running

{{< imgwrap src="greaseweazle_run.png" alt="Image of disks" >}}
Before doing anything else I enabled the read-only jumper on my Greaseweazle, as I wasn't planning on doing any writing to the drive and it just seemed safer all around with a new setup. The [Greaseweazle Wiki](https://github.com/keirf/greaseweazle/wiki) has the [jumper configuration](https://github.com/keirf/greaseweazle/wiki/V4-Setup#jumper-configuration) as well as everything else you need to know to set up and use your Greaseweazle effectively.

Depending on your drive setup and configuration, the command line for running Greaseweazle to read a disk will vary. In my case, the following did the trick for me:

```gw read --retries 20 --seek-retries 10 --drive a --format ibm.1440 filename.img```

One note: the retries and seek-retries attributes are there since the floppy disks were not reading reliably - giving it multiple retries succeeded in getting a clean read of the disk.

# Internet Archive

Now that I had the images I was all done, right? Not so fast! We need to archive them to a safe place to digitally protect them and make them available for other people to use as well. Also, the .img file is useful as an archive, but for many floppies we can also create a zip file of the contents to make it easily accessible. The steps to do this vary depending on your operating system, but under Linux all I had to do was to mount the floppy image and then zip the contents:

    sudo mkdir -p /mnt/floppy
    sudo mount -o loop filename.img /mnt/floppy
    zip filename.zip /mnt/floppy/*

Now that we have our zip file(s) and image(s), we can upload them for safekeeping. One of the best places to do this is the [Internet Archive](https://archive.org/).

## Internet Archive

The Internet Archive is a huge repository covering many topics, including the [Wayback Machine](https://web.archive.org/), a [Book Library](https://archive.org/details/inlibrary?tab=collection) and much more, including the [Software Collection](https://archive.org/details/software?tab=collection). While you are there, consider giving them a [donation](https://archive.org/donate) as they do important work for the community.

In this case, we want to add a new software title. To do so, first sign up for an account on archive.org, then click the "UPLOAD" button at the top right of the screen, then click on "Upload Files". From there, choose the files to upload. Don't forget to include cover art, screenshots, as well as the .img and .zip files produced earlier. Also add metadata about the publisher, year, title, and other data to help people find your project. Submit the new project and that's it! To see my completed entry, see [Startdate](https://archive.org/details/stardate).

# Conclusion

Using Greaseweazle to back up old floppies is a great way to preserve them. Once you have the Greaseweazle setup, backing up these old disks is very quick and easy. You may even be able to read some old disks that you haven't been able to get to work otherwise. Have fun and let me know how it goes for you!

