---
description: >-
  Integrate additional sensors into the temperature graph. For example Raspberry
  Pi cpu temperature.
---

# Additional Sensors

### Raspberry Pi temperature sensor

Append the following section to your printer.cfg:

```text
[temperature_sensor raspberry_pi]
sensor_type: rpi_temperature
min_temp: 10
max_temp: 100
```

### ATSAM, ATAMD, and STM32 temperature sensor

Append the following section to your printer.cfg:

```text
[temperature_sensor mcu_temp]
sensor_type: temperature_mcu
min_temp: 0
max_temp: 100
```

{% hint style="info" %}
For more information on this topic, please refer to Klipper's documentation:  
[https://www.klipper3d.org/Config\_Reference.html\#builtin-micro-controller-temperature-sensor](https://www.klipper3d.org/Config_Reference.html#builtin-micro-controller-temperature-sensor)
{% endhint %}

