---
layout: post
title: Fixing a Broken Subwoofer
categories: Projects
# thumbnail_file: subwoofer.png
---

One of the central tenents of college life is having a good stereo system. Everybody knows that. So, when my friend offered me a broken subwoofer from his parents, I had a new project.

<!-- Correct specs below -->
The sub is a [*insert model name*](), with twin 12-inch, 4-ohm speakers. The cones were perfectly intact, and a quick impedence check with a multimeter shows that the coils were as well. The issue was the amplifier. I pulled the **heavy** power supply/amplifier assembly out of the cabinet and poked around a bit, but some research and continuity testing showed that the problem was likely a transistor that would be prohibitively difficult to replace. Instead, I decided to replace the amplifier altogether. 

<!-- 
TODO:
- Add link to amp circuit
- Correct price for amp
- Get correct voltage range for amp circuit
- Get correct power draw for amp
 -->
Finding the amp was easy. [this unit]() is readily available on Amazon for around $20. It takes a monaural line-level input signal and 15-24V DC power (up to ??W). Because it's designed for an output impedance of 4&Omega;, I kept the two 2&Omega; speakers in series and wired them directly to the output of the amplifier.

I considered buying a new 24V power supply, but a decent quality unit that supplies enough current costs more than I spent on the amplifier itself. Instead, I got my hands on a free, used 19V laptop charger whose connector had frayed. Soldering on a new barrel jack gave me the power supply at a fraction of the cost of buying new. 

Now, the last issue: Getting a volume-adjusted line-level signal into the amplifier. Sadly, my $10 receiver lacks a dedicated active subwoofer output. I tried probing the internals of the receiver to find a signal that I could tap, but the only place I could find with any hope was on the op-amps which were thermal epoxied to a heat sink, and hence were inaccessible without a lot of disassembly.

Instead, I went the route of many car subwoofer installations: using a "line-out converter" (LOC) to drop the speaker level signal out of the receiver down to a level I can pass to the sub's amp. As with the power supply, a decent LOC could run a similar price to the amplifier itself, so I just built one. It was as simple as a voltage divider for each channel (left and right) with a pair of resistors to sum the outputs without too much crosstalk (putting the summing after the voltage dividers instead of before also minimizes the crosstalk affecting the main speakers). 