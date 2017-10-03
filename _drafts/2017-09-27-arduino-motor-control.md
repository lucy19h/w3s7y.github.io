---
layout: post
title:  "Driving a Universal Motor with a triac and an Arduino"
date:   2017-09-27 19:46:00 +0100
categories: blog
---
Disclaimer
---
**THIS PROJECT USES 240 VOLTS AC (MAINS POWER) WHICH CAN (AND PROBABLY WILL)
KILL YOU.**  

**DO NOT DO THIS UNLESS YOU KNOW WHAT YOU ARE DOING**

_Worth noting, I don't know what I am doing.  But don't say I didn't
warn you if you end up letting the smoke out of yourself_

Introduction
---
In this blog I'm exploring more traditional electronics including discrete
components and semiconductors.  Namely using a triac to switch mains power and
drive a high power washing machine motor recovered from my old clapped out Bosch.  
The ultimate aim will be to attach this to an apple scratter which simply takes
whole apples and mulches then into smaller pieces ready for pressing.  
Currently our scratter is hand cranked and takes an amazing amount of time to
get everything scratted and ready to press.  My 9 to 5 is generally automating
software processes.  Time to apply what I know to manufacturing processes!

Ripping apart an old washing machine
---
So when my old washing machine packed up most people would have simply resigned
it to their local recycling facility however I wanted to use the electrical
components of it to give our scratter mach 2 capabilities.  So I took a Torx 20
bit to it and a pair of pliers and did the old "see a screw, remove it" style
teardown.  It wasn't long before I had the following components liberated from
their steel prison:
* 1 No. BTB16-600CW triac (the heart of the operation)
* 2 No. 10A SPDT relay
* 1 No. 10A SPST relay
* 1 No. 1360W Universal Motor
* 1 No. drive belt & large reduction gear (off the back of the drum)
* 1 No. UK 3 pin plug, fuse and cord
* 1 No. Potted EMI filter (mandatory to use when connecting inductive/noisy loads to the grid)
* Various capacitors, diodes, etc. of different sizes and ratings

Not a bad haul... Certainly all the components I _think_ I need.
After doing a lot of research into the components and pulling the various data
sheets (see appendix) I started to work on a circuit.

Prototyping a board
---
After pinched fingers and bared knuckles pulling the washing machine apart
it was time to break out the breadboard, jumpers and DC bench power supply
(made out of an old salvaged ATX power supply, more of that in another blog) and
start prototyping.  First of all I checked all the parts and went online to obtain
the data sheets for all of the parts that I had collected from the main board inside
the machine.  After this I plugged the Triac into the breadboard and started to
have a investigate on it with 5V DC.  Unfortunately they do not behave the same
way with AC as they do DC.  However, this was useful to see the latching and
holding currents in action.  Keeping the triac closed (conductive) when the gate
is energised and their is a load exceeding 60mA (as per the datasheet) attached
even when the gate has been disconnected. AC behaves diffrently to this as when
the supply voltage crosses the "zero point" it has the effect of very briefly
also reducing the current to zero as well due to Ohms law.  This is however
desirable in our case as we will be supplying 250V AC to the triac and a small 5V
DC supply from my Arduino to hit the gate with.

Making the board
---

Testing the board
---


Appendix
---
[BTB16-600CW Triac datasheet](http://docs-europe.electrocomponents.com/webdocs/12d5/0900766b812d50e6.pdf)
