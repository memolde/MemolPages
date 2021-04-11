---
layout: post
title:  "Step up/down buck-boost module"
date:   2020-07-01 13:00:00 +0200
categories: Voltage Power Stepup Stepdown BuckBoost
---
I have bought a step up/down module. It should convert 2.5v-15v to 3.3 volts. Maximum current should be 600mA. This would be a good way to power an ESP32 with an li-ion battery.
![Pump]({{ site.baseurl }}/assets/images/2020-07-01-BuckBoost.jpg)
<!--more-->
The following voltages have been tested
<br>


| Voltage  | Watts in |      mA   | Efficiency |
|---------:|---------:| ---------:|:----------:|
| 2.5      |  0.0     |    0.0    |     0% |
| 3.0      |  0.0     |    0.0    |     0% |
| 3.1      |  0.44    |   100    |    80% |
| 3.3      |  0.44    |   100    |    80% |
| 4.0      |  0.44    |   100    |    80% |
| 5.0      |  0.44    |   100    |    80% |
| 5.0      |  0.84    |   200    |    80% |
| 5.0      |  1.25    |   300    |    80% |
| 5.0      |  1.70    |   400    |    77% |
| 5.0      |  2.35    |   500    |    69% |
| 5.0      |  3.10    |   600    |    61% |



<br>
The module does not really comply with the specifications. Input voltages below 3.1 volts do not produce any output voltage. The promised 600 mA output current leads to strange noises, voltage drops and a lot of heat. The following table shows the combinations which voltage / Amperage combination produces a valid output:


|         | 3.1 | 3.3 | 4.0 | 5.0 |
|--------:|:---:|:---:|:---:|:---:|
| 100 mA  |  X  |  X  |  X  |  X  |
| 200 mA  |  X  |  X  |  X  |  X  |
| 300 mA  |  -  |  X  |  X  |  X  |
| 400 mA  |  -  |  X  |  X  |  X  | 
| 500 mA  |  -  |  -  |  X  |  X  |
| 600 mA  |  -  |  -  | (X) | (X) |


<br>
Beginning with 400 mA the output voltage drops to 3.2 volts. With 500 mA it drops to 3.1 volts and the module gets hot. At 600 mA it also produces noises.
<br>
So for powering an ESP32 it could work fine as long as the batteries do not drop below 3.1 volts.