---
layout: post
title:  "ESP32 power supply with battery"
date:   2021-03-28 13:00:00 +0200
categories: ESP32 Battery Low-Power
---
I have a project running on solar power with Li-ion batteries. To save power and avoid unneccesary losses I want to find the optimal power supply.

### Assumptions:

- Li-ion Battery provides power: 3.0 - 4.2V
- Esp accepts power supply: 2.3V – 3.6V
- Esp accepts external power supply: 5V – 12V
- Esp uses < 100mA when not using Wifi and >200mA when using Wifi

### Verification via experiment:

#### Esp accepts power supply: 2.3V – 3.6V
Test with bench power supply via vin:

| Voltage  |  Boots  |  Connects  |  Kepp Connection  |
|:--------:|:-------:|:----------:|:----------:|
|  3.6     |      X  |     X      |     X      |
|  3.5     |      X  |     X      |     X      |
|  3.4     |      X  |     X      |     X      |
|  3.3     |      X  |     X      |     X      |
|  3.2     |      X  |     X      |     X      |
|  3.1     |      X  |   -/X      |     X      |
|  3.0     |      X  |     -      |     X      |
|  2.9     |      X  |     -      |     -      |
|  2.8     |      X  |     -      |     -      |
|  2.7     |      -  |     -      |     -      |

Already with 2.7 Volts the device does not boot (simple blink script). And Wifi has even higher power requirements. Below 3.2 Volts it is not possible to get a reliable connection to the Wifi network. This means that there is not much room to vary the voltage. Since 3.2 Volts are already at the end of the li-ion discharge curve it would be no problem for the minimum voltage.

It turns out that the minimum voltage is 3.0 Volts. See [here](https://www.espressif.com/sites/default/files/pcn_downloads/PCN-02-20190815%20ESP32%20Series%20Products%20Technical%20Document%20Change.pdf)

The maximum voltage with my ESP32 Wroom is 3.95 volts with active Wifi. It still works with 4.00 and even sometimes with 4.05, but not with 4.10. Since it did not get warmer than normal, this is probably ok. Of course this could be different for different models or even the same model.


#### Esp accepts external power supply: 5V – 12V
Test with bench power supply via vin:

| Voltage  |  Boots  |
|:--------:|:-------:|
|  12      |      X  | 
|   7      |      X  | 
|   5      |      X  | 
|  4.8     |      X  | 
|  4.7     |      X  | 
|  4.6     |      -  | 


After the voltage was lower than operating power, the ESP automatically restarts when the voltage level is high enough. Altough it runs with 4.6Volts, it does not boot and connect to WiFi, so a minimum of 4.7 Volts is needed. For all voltages the current is 73mA i.e. the power consumption is linear to the voltage. During Wifi transfers it goes up to about 150mA


#### Esp uses < 100mA when not using Wifi and >200mA when using Wifi

Tested with 3.3 Volts. Before activating Wifi, the power consumption was 51mA. To check the power consumption with Wifi, I have set my power supply to limit to 200mA and tried to connect to Wifi, but it didn't connect. It took me 350 mA to connect. Adding a 47 yF capacitor makes it more stable. Adding another 150 yF capacitor and 300 mA are enough. Adding another 6800 yF capacitor and 150 mA are the absolute minimum. 
After connecting the power consumption is 73 mA during no transmission.

### Conclusion

Powering the ESP is far more difficult than thought when using Wifi. Without Wifi the power consumption stays relatively low. When Wifi is activated there may be peaks of 350 mA. These peaks may be difficult to provide especially when you are using weak step/up down converters, long cables, voltages near the limit.

For battery power we have the following alternatives:

* Use a step-up module to 5V and use the Vin or usb port to power the ESP.

    Advantage: Works reliably when the step-up module can provide 500 mA

    Disadvantage: Only about 64% of the energy is used sind both converters have an efficiency of about 80% (0.8 * 0.8 = 0.64).

* Use a Voltage regulator.

    Advantage: Already on the ESP

    Disadvantage: The battery does not provide enough voltage. You need to use 2 Batteries. Power loss is linear to the voltage difference i.e. 8v->3.3V = 41% effieciency

* Use a zenner (avalance) diode 
    Advantage: Simple

    Disadvantage: Burns the excess voltage until it is lower as the diode voltage. This caps the battery capacity
    