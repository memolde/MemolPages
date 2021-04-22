---
layout: post
featured_img: /assets/images/2021-04-22-PowerConnector.jpg
title:  "Power connector load test"
date:   2021-04-22 20:04:59 +0200
categories: Power Connector Load Amps Ohm
---

![PowerConnectors]({{ site.baseurl }}/assets/images/2021-04-22-PowerConnector.jpg)
I have bought some power connectors and want to see how much power can be transferred with them. Measuring the resistance showed about 0.4 Ohms. My multimeters do now show more accuracy. 

The following table shows experiments with an adjustable power drain and a power supply. Up to 1 Amps seems to be Ok, everything above I would not reccomend. Also see the voltage drop. 

According to:

 U = R * I. 
 
 R = U/I 
 
 The resistance is 0.9 Ohms for 3.6 Volts / 4.0 Amps.

|  mA      | Voltage |   Cabling Status       |
|:--------:|:-------:|:-----------------------|
|     0    |   10.1  |                        |
|   200    |    9.9  |                        |
|   500    |    9.6  |                        |
|  1000    |    9.2  | No temparature cange   |
|  1500    |    8.7  |                        |
|  2000    |    8.3  | Gets warm              |
|  2500    |    7.8  |                        |
|  3000    |    7.3  | Gets hot after a while |
|  3500    |    6.9  |                        |
|  4000    |    6.4  | Gets hot quick         |


