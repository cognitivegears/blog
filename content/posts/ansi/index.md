+++
draft = true
author = "Nathan Byrd"
title = "ANSI and bANSI and VT100, oh my!"
date = "2023-09-20"
showFullContent=false
readingTime = true
description = "Investigating the world of terminals, compatibility, and BBS software with Enigma ½ BBS."
tags = [
    "greaseweazle",
    "floppy",
    "preservation",
]
+++

## Introduction

Welcome readers! Herein lies a tale of woe. A tale of competing standards and compatibility. Yep, today we are talking about ANSI.

<!-- more -->

## Project

{{< imgwrap src="enigma.png" alt="Enigma BBS" >}}
I've been working with the fantastic [Enigma ½ BBS](https://enigma-bbs.github.io/) for a while now (and yes, I have to go grab that ½ unicode character every time I post something about it lol.) Enigma ½ is retro BBS software using a modern programming language (node.js) and technologies. It is almost more of a platform than a specific BBS software, incredibly flexible and extensible, with a wide range of supported protocols and functionality. As an example, one of the projects that is in progress currently is to enable ActivityPub integration so that it can talk to Mastodon and other fediverse systems. I'm not going to go into detail about that here, but you should check out more information about it on [NuSkooler's Blog - ActivityPub Beta](https://l33t.codes/2023/04/20/ActivityPub-Beta-on-Xibalba-BBS/). Lately, I've been working to reduce the backlog of issues on Enigma ½, particularly high priority ones. Specifically, right now I'm working on small incompatibilities between ANSI drawing programs, Enigma ½, and various terminals.

## ANSI

And oh-boy are there incompatibilities. I always knew that the standards were not always strict, but I didn't realize how much the BBSes and terminals had to assume based on the loose standards, and that it made a real difference whether your art was drawn with [TheDraw](http://www.syaross.org/thedraw/), [ACiDDraw](https://www.acid.org/apps/apps.html), or the newer [PabloDraw](https://github.com/cwensley/pablodraw), [Moebius](https://blocktronics.github.io/moebius/) or upcoming [IcyDraw](https://github.com/mkrueger/icy_draw), among many others. A partial list of ANSI editors can be found at: [Ansi Editors](http://wiki.synchro.net/resource:ansi_editors). And then it makes a huge difference which client is used. Enigma ½ works with many different clients, from old terminals running on original hardware (Procomm / Procomm Plus for example, or even programs running on old 8-bit hardware,) all the way to brand new terminals like [Alacritty](https://github.com/alacritty/alacritty), with many, many others in-between. We can broadly categorize them as:

* VT-100 terminals with UTF-8 character encoding
* VT-100 terminals with (some other) encoding
* ANSI terminals with CP-437 encoding
* ANSI terminals with (some other) encoding
* Something else completely

## A word about Encoding

What is this CP-437 and UTF-8? These are known as character encodings, and describe what byte or bytes make up a particular character. At the base is 7-bit ASCII, which is the base of _most_ of the software we use. [Here](https://www.ascii-code.com/ASCII) is a chart that shows the commonly used ASCII characters. There are variations on this, like ATASCII (Atari Ascii) and Petscii (Commodore Ascii) but for the most part this is the same on most of the systems we'll be communicating with. Beyond 7-bit ASCII though there are differing ways of displaying extended characters, including the "semigraphics" characters used for drawing ANSI art. [CP-437](https://www.ascii-codes.com/) is one such character set that became popular from early IBM PC's and clones. A more modern encoding, UTF-8, is an encoding of the much larger and more complete [Unicode](https://unicode.org/charts/) standard, that sometimes takes two bytes to display a single character due to the number of available characters.

Enigma ½ internally uses UTF-8 for all of it's processing, and converts into and out of CP-437, UTF-8 and ASCII (with more coming hopefully soon!) as needed. This is a great solution, as it means that we can support many terminals without code specific to each type. All we need to know is the mapping between the native encoding (such as CP-437) and UTF-8, and Enigma can then use either interchangeably.

## Control Codes

The name "VT100" comes from a range of video terminals created by Digital Equipment Corporation. This line of terminals helped define the standards used up to today when sending control codes to/from a terminal client and server. These control codes could tell the terminal to clear the screen, move the cursor to a position, change text styles, and many more similar operations. Since these communications needed to be "in-band" - meaning that they share the same communications channel as the text communications, they use escape sequences to differentiate them normal content.

A related standard is (confusingly) known as ANSI. This terminology is confusing because while ANSI simply stands for the [American National Standards Institute](https://ansi.org/), what people are really talking about when they say ANSI in relation to BBS communications is the set of control codes that are _mostly_ compatible with VT100 codes used in BBS software. A great resource for learning more about the ANSI BBS specification is at: (http://ansi-bbs.org). Information from the ANSI body itself can be found in their [blog](https://blog.ansi.org/2019/10/ansi-art-ascii-art-iso-standards-x3-64/). The ANSI X3.64-1979 standard which it is based on was later withdrown in favor of an international standard, ISO/IEC 6429. So "ANSI terminal" is just a term now, better described in other documents - such as the [ansi-bbs](http://ansi-bbs.org) site.

ANSI and VT-100 are only _mostly_ the same, and most of the differences can be glossed over. Enigma ½ takes the pattern of accepting input from either ANSI terminals or VT-100, and outputting only a subset that works on both known as bANSI (although, this also depends on what art files a sysop has created for their system.)

And what is this bANSI you ask? In 1995 (updated 1999) the author of a BBS client software named Bananacom, Paul Wheaton, authored an article called [bansi.txt](http://www.ansi-bbs.org/BANSI/bansi.txt) that spelled out how Banacom interpreted the various standards and common extensions to support a wide range of terminals. bANSI is what Enigma ½ and others use to help navigate the differing implementations of the existing standards and private extensions. Anyone looking to write a BBS terminal, software, or editor should definitely become familiar with this standard.

## Back to the Project

One of the first things that bothered me is that on terminals like 