---
layout: post
title:  "Water pump"
date:   2020-07-01 13:00:00 +0200
categories: Voltage Power Pump Water
---
I have a small water pump to water my flowers. To control it, I want to know how much power is used. So I put it in a jar and powered it on.
![Pump]({{ site.baseurl }}/assets/images/2020-07-01-Pump.jpg)
<!--more-->
I connect the pump to my bench power supply and test:
<br>

| Voltage  | Amps    | Watts   | Remark            |
|---------:|--------:| -------:|------------------:|
| 3.3      |   0.33  |    1.1  | Slow, but working |
|   5      |   0.43  |    2.1  | Already ok        |
|  6.6     |   0.57  |    3.8  | Good flow         |
|  8.4     |   0.77  |    6.4  | Even more flow    |
|  10      |   0.97  |    9.7  | Strong flow       |
|  12      |   1.25  |   15.0  | Very strong flow  |


The flow seems to increase exponentially with the voltage and is corresponding with the Wattage. Since my project uses li-ion batteries which can provide 6.6 to 8.4 volts with 2 batteries the flow is ok, but not too strong. Maybe another battery would be an idea to increase the voltage to 9.9-12.6 volts.<br> 
On the other hand my batteries are solar powered and should therefore have enough power when the weather is nice and more water is needed.
<br>
<br>
I will use a IRLD024 mosfet which can switch 1.8 amps to control the pump since the relay was not reliable enough and drained too much power.