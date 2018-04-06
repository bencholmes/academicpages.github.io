---
title: 'Component meters: DE-5000 and M328'
date: 2018-02-18
permalink: /posts/2018/02/component-meters
mathjax: true
tags:
  - equipment
  - testgear
  - measurements
  - de-5000
  - M328
---

Recently I've been in need of measuring linear component values to a high degree of accuracy, so decided to purchase a couple of component meters. The first of these is the M328 "transistor tester", which is a favourite of the DIY community as it is cheap and has all of the plans available on the internet. I put transistor tester in quotes as the meter is designed to measure resistance, capacitance, inductance, transistor type and basic characteristics, and even some parasitic properties. This is quite an impressive boast for a product which I purchased for £6.32!

The only problem with this is that it does not satisfy the need of precision and accuracy. To accomplish this, I purchased a dedicated LCR meter, the DER EE DE-5000. This LCR meter appears to have been designed to rip off the IET Labs DE-5000, and sell at a fraction of the price. A [teardown at the EEVblog forum](http://www.eevblog.com/forum/testgear/der-ee-de-5000-unboxing-and-teardown/) shows that the equipment, while being budget, is of decent quality.

## Quick specs

### M328
- Price: £6.38
- Power supply: 9 V battery
- Measures:
  - Resistance
  - Capacitance
  - Inductance
  - hFE and Uf of BJTs
  - Many other factors
- [Manual](/files/Ttester_english.pdf)
- [Hackaday Review](https://hackaday.com/2015/04/24/review-transistor-tester/)

### DE-5000
- Price: £80
- Power supply: 9 V battery or external PSU
- Measures:
  - Resistance
  - Capacitance
  - Inductance
  - Secondary factors including ESR, dissipation and quality.
- [Manual](/files/DE-5000_manual_english.pdf)
- [Youtube review](https://www.youtube.com/watch?v=sYRxi3BmS_U)


## Meter operation

To illustrate the performance of both meters I have uploaded videos demonstrating how they perform when measuring a 1 MΩ potentiometer.

### M328
<video width="400" height="280" controls>
 <source src="/images/MTester.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>

What is really useful about the M328 is that it has three connections, enabling it to measure the minimum resistance of the potentiometer, here measured to be 0.2 Ω.

### DE-5000
<video width="320" height="560" controls>
 <source src="/images/DE-5000.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>

Obviously the dedicated LCR meter that costs over 10x the price offers better precision with the resistance measurement, however the measured values seem pretty close!

## Gutshots

I had to disassemble the DE-5000 due to the meter indicating a short at all times. This actually turned out to be a calibration issue that was fixed by simply recalibrating. This did help in two ways however: calibration holds even when powered down so that recalibrating isn't necessary each use, and I took some shots of the inside of the meter.
![Component-side DE-5000](https://i.imgur.com/CrPVbRg.jpg)
![Button/screen-side DE-5000](https://i.imgur.com/cHPD5DT.jpg)
