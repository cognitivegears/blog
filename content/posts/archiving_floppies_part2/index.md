+++
author = "Nathan Byrd"
title = "Archiving floppies to the Internet Archive - Part 2"
date = "2023-07-26"
showFullContent = false
readingTime = true
description = "In part 2 of the archiving floppies series we are going to get Greaseweazle running and get the resulting archive uploaded. Nobody can stop us now!"
tags = [
    "greaseweazle",
    "floppy",
    "preservation",
]
+++

## Introduction

In [Part 1](../archiving_floppies_part1/) we discussed how to purchase and setup a Greaseweazle in order to back up disk media. This time we are going to put that to use to actually backup our project and get it uploaded to the Internet Archive. As an example, I am backing up Stardate by Berkeley software. Because who couldn't use a little more Star Trek in their lives?

<!-- more -->

### running

{{< imgwrap src="greaseweazle_run.png" alt="Image of disks" >}}
Before doing anything else I enabled the read-only jumper on my Greaseweazle, as I wasn't planning on doing any writing to the drive and it just seemed safer all around with a new setup. The [Greaseweazle Wiki](https://github.com/keirf/greaseweazle/wiki) has the [jumper configuration](https://github.com/keirf/greaseweazle/wiki/V4-Setup#jumper-configuration) as well as everything else you need to know to set up and use your Greaseweazle effectively.

Depending on your drive setup and configuration, the command line for running Greaseweazle to read a disk will vary. In my case, the following did the trick for me:

```gw read --retries 20 --seek-retries 10 --drive a --format ibm.1440 filename.img```

One note: the retries and seek-retries attributes are there since the floppy disks were not reading reliably - giving it multiple retries succeeded in getting a clean read of the disk.

Now that I had the images I was all done, right? The .img file is useful as an archive, but for many floppies we can also create a zip file of the contents to make it easily accessible. The steps to do this vary depending on your operating system, but under Linux all I had to do was to mount the floppy image and then zip the contents:

    sudo mkdir -p /mnt/floppy
    sudo mount -o loop filename.img /mnt/floppy
    zip filename.zip /mnt/floppy/*

### Internet Archive

Now that we have our zip file(s) and image(s), we can upload them for safekeeping. One of the best places to do this is the [Internet Archive](https://archive.org/).

The Internet Archive is a huge repository covering many topics, including the [Wayback Machine](https://web.archive.org/), a [Book Library](https://archive.org/details/inlibrary?tab=collection) and much more, including the [Software Collection](https://archive.org/details/software?tab=collection). While you are there, consider giving them a [donation](https://archive.org/donate) as they do important work for the community.

In this case, we want to add a new software title. To do so, first sign up for an account on archive.org, then click the "UPLOAD" button at the top right of the screen, then click on "Upload Files". From there, choose the files to upload. Don't forget to include cover art, screenshots, as well as the .img and .zip files produced earlier. Also add metadata about the publisher, year, title, and other data to help people find your project. Submit the new project and that's it! To see my completed entry, see [Startdate](https://archive.org/details/stardate).

## Conclusion

Using Greaseweazle to back up old floppies is a great way to preserve them. Once you have the Greaseweazle setup, backing up these old disks is very quick and easy. You may even be able to read some old disks that you haven't been able to get to work otherwise. Have fun and let me know how it goes for you!
