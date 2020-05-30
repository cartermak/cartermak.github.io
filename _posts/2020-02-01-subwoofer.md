---
layout: post
title: Fixing a Broken Subwoofer
categories: Projects
thumbnail_file: subwoofer.png
---

One of the central tenents of college life is having a good stereo system. Everybody knows that. So, when my friend offered me a broken subwoofer from his parents' basement, I had a new project.

The sub is a Polk Audio PSW650, with twin 10-inch drivers. The cones were perfectly intact, and a quick impedance check with a multimeter shows that the coils were as well. The issue was the amplifier. I pulled the **heavy** power supply/amplifier assembly out of the cabinet and poked around a bit, but I couldn't identify the problem component (although I suspect it was one of the transistors glued to the massive heat sink). Instead, I decided to replace the amplifier altogether. 

<div style="text-align:center;margin:40px">
    <img src="{{ site.baseurl }}/assets/projects/subwoofer/psw650.jpeg" alt="Polk Audio PSW 650" align="center" style="width:50%" hspace=25px>
</div>

Finding the amp was easy. [This unit](https://www.amazon.com/AOSHIKE-Subwoofer-Amplifier-TPA3116D2-Amplifiers/dp/B01N0PXEN4) is readily available on Amazon for $10-20. It takes a monaural line-level input signal and 8-25V DC power, with a rated output power of 100W (presumably RMS). This is less than the 165W RMS output of the original amp, but it's pretty fantastic for the price. Because it's designed for an output impedance of 8&Omega;, I kept the two 4&Omega; speakers in series and wired them directly to the output of the amplifier.

I considered buying a new 24V power supply, but a decent quality unit that supplies enough current costs more than I spent on the amplifier itself. Instead, I got my hands on a free, used 19V laptop charger whose connector had frayed. Soldering on a new barrel jack gave me the power supply at a fraction of the cost of buying new. 

Now, the last issue: Getting a volume-adjusted line-level signal into the amplifier. Sadly, my $10 receiver lacks a dedicated active subwoofer output. I tried probing the internals of the receiver to find a signal that I could tap, but the only place I could find with any hope was on the op-amps which were glued to a headsink with thermal epoxy, and hence were inaccessible without a lot of disassembly.

Instead, I went the route of many car subwoofer installations: using a "line-out converter" (LOC) to drop the speaker level signal out of the receiver down to a level I can pass to the sub's amp. As with the power supply, a decent LOC could run a similar price to the amplifier itself, so I just built one. It was as simple as a voltage divider for each channel (left and right) with a pair of resistors to sum the outputs without too much crosstalk (putting the summing after the voltage dividers instead of before also minimizes the crosstalk affecting the main speakers). I feed stereo speaker-level signals into one end and get an amp-friendly mono signal out the other.

Here's a quick schematic:

<img src="{{ site.baseurl }}/assets/projects/subwoofer/schematic.png" alt="LOC Schematic" align="center" style="width:70%" hspace=25px>
<!-- ![LOC Schematic]({{ site.baseurl }}/assets/projects/subwoofer/schematic.png) -->

Soldering this together with some through-hole resistors, pin headers, and a small protoboard produced a package that I conveiniently screwed on to an existing terminal on the back of my receiver. Fed into the subwoofer's amplifier, I get respectable bass that I can easily tune across a full range from tasteful to absurd.