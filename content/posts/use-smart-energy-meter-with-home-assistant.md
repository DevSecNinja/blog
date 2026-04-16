---
title: 'Use Smart Energy Meter with Home Assistant'
date: 2018-08-04T06:30:42+00:00
draft: false
tags: ['Domotica', 'DSMR', 'Hass', 'Hass.IO', 'Home Assistant', 'Liander', 'Slimme meter']
description: ""
cover:
  image: ""
  alt: ""
---

**The Dutch Government is aiming on providing smart meters to every household before Q4 2020. All the smart meters need to comply to DSMR (Dutch Smart Meter Requirements). DSMR allows us to read data from the smart meter by using a cable. In this guide, I will explain how I got this to work with Home Assistant.**

## Prerequisites

- Home Assistant (Hass.io) running on a Raspberry Pi
- One of the [supported smart meters](https://www.home-assistant.io/components/sensor.dsmr/). I'm using the Landis+Gyr ZMF110 with DSMR 4.2 from Liander
- [A cable](https://www.sossolutions.nl/slimme-meter-kabel) to connect from USB on your Pi to the smart meter
- (Optionally) a second Raspberry Pi running on a Linux distro to send the data over the network to your Hass.io Pi

## Connect your Raspberry Pi to the smart meter

Insert the USB cable in the Raspberry Pi and the other side of the cable into your smart meter. A data connection should now be established.

### Optional: Use Ser2Net on another Raspberry Pi if your Pi isn't close to the smart meter

I have two Pi's and only one of the Pi is close to the smart meter, while the other Pi hosts the Hass.io image. Luckily there is a great Linux package called Ser2Net. This tool will make the serial connection available over the network. Install and configure it with the following commands:

```bash
sudo apt-get update
sudo apt-get install ser2net
sudo nano /etc/ser2net.conf
sudo service ser2net restart
```

At step 3, make sure you grab the example code from the [official Home Assistant component page](https://www.home-assistant.io/components/sensor.dsmr/) and save the file.![chrome_2018-08-04_07-01-23](/images/2018/08/chrome_2018-08-04_07-01-23.png) _Please note that I assume that the USB cable is connected to /dev/ttyUSB0. If that's not the case, change this value to the correct port._

## Enable the DSMR component in Home Assistant

Open your Configuration.yaml file or your Sensors.yaml file and specify the following configuration if the Smart Meter is directly connected to USB:

```yaml
# Example configuration.yaml entry for USB/serial connected Smartmeter
sensor:
  - platform: dsmr
    port: /dev/ttyUSB1
    dsmr_version: 5
```

If you are using the Ser2Net on another Pi, use the following configuration:

![chrome_2018-08-04_07-07-04](/images/2018/08/chrome_2018-08-04_07-07-04.png) Don't forget to check the DSMR version on your smart meter and the USB port on the Raspberry Pi. Now all the sensors will be available in Home Assistant. You might want to structure this as a group in the configuration.yaml file or like me in a separate groups.yaml file:

```yaml
meter_readings:
  name: Meter readings
  entities:
    - sensor.power_consumption
    - sensor.power_consumption_low
    - sensor.power_consumption_normal
    - sensor.power_consumption_phase_l1
    - sensor.power_consumption_phase_l2
    - sensor.power_consumption_phase_l3
    - sensor.power_production
    - sensor.power_production_low
    - sensor.power_production_normal
    - sensor.power_production_phase_l1
    - sensor.power_production_phase_l2
    - sensor.power_production_phase_l3
    - sensor.power_tariff
    - sensor.voltage_sags_phase_l1
    - sensor.voltage_sags_phase_l2
    - sensor.voltage_sags_phase_l3
    - sensor.voltage_swells_phase_l1
    - sensor.voltage_swells_phase_l2
    - sensor.voltage_swells_phase_l3
    - sensor.long_power_failure_count
    - sensor.gas_consumption
    - sensor.hourly_gas_consumption
```

## Update 1:

I've been playing around with my dashboard in Home Assistant this weekend. I now have the following view in my dashboard: ![Home Assistant Power Meter Readings](/images/2018/08/chrome_2018-08-06_10-55-14.png)

_Screenshot of Meter Readings view in Home Assistant_

## Update 2:

Something I forgot to mention in the blog post: if you use the ser2net package mentioned in the blog post, make sure you allow access to the port (e.g. 2001) from Home Assistant and deny access to any other device. This can be done by using a firewall like ufw on Linux. Otherwise your smart meter data is visible to anyone on the (local) network. Big thanks to everyone who made this possible in the Home Assistant Community! Cheers.
