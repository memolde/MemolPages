---
layout: post
title:  "Corrosion Resistant Capacitive Soil Moisture Sensor Part 2"
date:   2021-04-24 18:00:00 +0200
categories: Corrosion Sensor Water Moisture Capacitive
---
Last year I tried acrylic paint to protect my Soil Moisture Sensors.
![Sensor Protected]({{ site.baseurl }}/assets/images/2020-05-30-sensor_green.jpg)
See my post [here]({{ site.baseurl }}{%post_url 2020-05-30-Corrosion-free-sensor%})
 
This is how some of them looked after one year:
![Sensor1]({{ site.baseurl }}/assets/images/2021-04-24-sensor1.jpg)
This sensor looks fine except of some minor optical changes. But it is not working anymore. It returns just 0.3 Volts, and what is worse: It constantly draws 100mA! I thought my battery has gotten a defect during winter, but it seems that this sensor is causing the battery power drain faster as expected.

![Sensor2]({{ site.baseurl }}/assets/images/2021-04-24-sensor2.jpg)
It looks a little bit worn, but still works
![Sensor3]({{ site.baseurl }}/assets/images/2021-04-24-sensor3.jpg)
This one looks extremely worn, but it still works correctly. It will probably break sometime due to corrosion. It has a higer power consumption of 22 mA while the others have 7 mA

This worked fine, but I had problems to interpret the measurements. 

I thought about problem sources:
- Voltage changes result in different measurements
- Different types of sensors have different charateristics
- Inaccurate analog measurement in the ESP
- Long cables and connectors have unpredictable resistances
- Temperature may influence the readings

### First of all I experimented with voltage changes and water:

|  Input Voltage    | Output Voltage Dry | Output Voltage 20ml Water |Output Voltage 50ml Water |
|:-----------------:|:------------------:|:-------------------------:|:-----------------------:|
|     3.0           |      2.53 V        |       2.46 V              |       1.71 V            |
|     3.33          |      2.83 V        |       2.74 V              |       1.92 V            |
|     3.5           |      2.83 V        |       2.74 V              |       1.92 V            |
|     4.0           |      2.83 V        |       2.74 V              |       1.92 V            |
|     4.5           |      2.83 V        |       2.74 V              |       1.92 V            |
|     5.0           |      2.83 V        |       2.74 V              |       1.92 V            |

The sensors are compensated for voltage changes as long as you have at least 3.33 Volts. 

### Different sensors (Measured with 5Volts):

|  Sensor Number    | Output Voltage Dry |Output Voltage 50ml Water |
|:-----------------:|:------------------:|:-----------------------:|
|     A-1           |      2.83 V        |       1.92 V            |
|     A-2           |      2.84 V        |       1.93 V            |
|     A-3           |      2.83 V        |       1.86 V            |
|     B-1           |      3.24 V        |       2.05 V            |
|     B-2           |      3.16 V        |       2.25 V            |
|     B-3           |      3.16 V        |       2.08 V            |
|     C-1           |  drifting 2.9 V    |  Drifting  2.4 V        |

The Sensors have a different characteristic. 

Sensor A from DIY More is reacting instantly to wetness changes. Sensor B takes several (around 5) minutes to adapt to new values. I guess Sensor B just has a bigger capacitor to smooth the readings. When you want to record a value only once every 5 Minutes it is not an option to power down the sensor. Since the power usage is 7-8 mA this draws substantially power which is especially important for battery powered installations.
Sensor C seems to be broken it drifts for about 0.1 Volts. I don't have a new one to compare with, so it may be broken.

 The sensors have differnt values for dry and wet, but are quite similar compared to the same group. 

To be comparable, it makes sense to use similar sensors or have a good compensation in the software. Since I didn't check for different wetnesses of the soil, I cannot say if the measuring curve is similar. The wet value is alreay different since it is difficult to place all sensors in the same way into the earth.

Mounting the sensor is also tricky. Compressing the earth around the sensor leads to lower values for wet earth. It is also important how deep the sensor is in the earth.

### Inaccurate analog measurement in the ESP

The measurement from the ESP was between 2167 and 2208  for the same ADC (1115) converter reading of 1.86V an extreme was 1959, but this was a single value. the middle is 2188 / 1.86 V = 1176/Volt. The readings would be 1.84 to 1.88. Ok, but not accurate. Especially since they are just jumping around randomly and sometimes have unexplainable extremes.

### Long cables
I haven't done experiments here. But the other results already showed the weak points. But since I want to use an ADC ADS1115 to measure the values this will be solved. The ADC is connected via I2C bus. This makes it possible to add sensors later on and connect them to the same bus.

### Temperature may influence the readings


|  Temperature     | Output Voltage |
|:-----------------:|:-------------:|
|     40            |      1.74 V   |
|     30            |      1.76 V   |
|     20            |      1.78 V   |

Temperature seems to have an effect, but only a small one. Since the humidity usually also changes when the temperature changes, this can probably be ignored.


### Conclusion
- Paint the bottom of the sensor as well
- Don't mix sensors of different types
- make sure the sensors are positioned similar in the earth
- Prefer an analog digital converter near the sensors instead of using long cables and the ADC of the ESP32.