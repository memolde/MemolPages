---
layout: post
title:  "5Volt relay"
date:   2020-06-30 15:00:00 +0200
categories: Relay Voltage Control Power
---
I want to control a small pump for watering my plants from an ESP32. I try to battery power the device, so the voltage is either 3,3V or something between 2.9 and 4.2 volts from a lithium-ion battery. How will the relay perform at these voltages?
![Relay]({{ site.baseurl }}/assets/images/2020-06-30-Relay.jpg)
<!--more-->
I connect the relay to my bench power supply and test: The control signal is not 5v, but has to be 0v (ground). Weird, but ok, I just need to know.
<br>
5 volts works as expected, but the power consumption is alreay 72mA (360 mW). This is a lot. There are  So I reduce to the voltage and at 3.5 volts it stops to be reliable. 

| Voltage       | Works         | Power(mA) | Remark      |
|:-------------:|:-------------:| ---------:|------------:|
| 5V            | Perfectly     |       72  | As designed |
| 4V            | Perfectly     |       56  | Still good  |
| 3.5V          | Randomly      |       48  | Not usable  |
| 3.3V          | No            |       44  | Not at all  |

This means it will work only when the batteries are not discharged too much. And the 3.3 volts from the ESP are not possible at all.