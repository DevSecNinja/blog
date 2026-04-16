---
title: 'Installing the new Home Assistant Hass.IO 64-bit image on a Raspberry Pi 3 Model B+'
date: 2018-07-20T16:30:42+00:00
draft: false
tags: ['Automation', 'Domotica', 'Hass.IO', 'HassIO', 'Home Assistant', 'Install', 'Installation Guide', 'Manual', 'Raspberry Pi', 'Raspberry Pi 3 Model B+']
aliases:
    - /2018/07/20/installing-the-new-home-assistant-hass-io-64-bit-image-on-a-raspberry-pi-3-model-b-/
description: ""
cover:
  image: ""
  alt: ""
---

Home Assistant recently [announced a brand new image of Hass.IO running on HassOS](https://www.home-assistant.io/blog/2018/07/11/hassio-images/). I instantly ordered a new Raspberry Pi 3 Model B+ to replace my older Raspberry Pi Model B, which was running Raspbian and Home Assistant. The guide below helps you with installing your new Hass.IO instance!

## Prerequisites

- Raspberry Pi 3 Model B+
- 32 GB **Micro-**SD card (I ordered a SanDisk Micro-SDHC 32GB Extreme U3 100MB/s)
- Ethernet cable (if not using WiFi)
- Micro USB power supply **(2.1 A - very important! I'm using an iPad charger)**
- A Windows 10 machine (This guide might work on a MacBook Pro or a Linux distro too)

## Installation Guide - Step-by-Step

1. Download [the 64-bit version of Hass.IO from Hass.IO](https://www.home-assistant.io/hassio/installation/). (File was named hassos\_rpi3-64-1.7.img.gz)
2. Download and install [Etcher](https://etcher.io/). I've used the Win32DiskImager tool before, but just installed Etcher to ensure that I'm following the right process.
3. Open Etcher, open the image file you just downloaded and select the SD card.
4. Hit the Flash button! ![Shows the Etcher application with the image and SDHC card selected](/images/2018/07/etcher-1.png)
5. Wait until it's completed. It took me a couple of minutes.
6. Optional - If you want to setup WiFi or set a static IP: On a USB stick, create the `network/my-network` file and follow the [howto from ](https://github.com/home-assistant/hassos/blob/dev/Documentation/network.md) [HassOS](https://github.com/home-assistant/hassos/blob/dev/Documentation/network.md).
7. Safely remove the SD card (and optional USB stick) from the computer.
8. Insert the SD card (and optional USB stick) into the Raspberry Pi and turn it on. Make sure you connect the LAN cable if you don't use WiFi! On first boot, it downloads the latest version of Home Assistant which takes about 20 minutes.
9. This gives you enough time to remove Etcher from your PC if you don't need it anymore.
10. You can now check your router/DHCP server to find the IP address of the Raspberry Pi. You can also reach the Raspberry Pi at [http://hassio.local:8123](http://hassio.local:8123/).

In the next blog post, we will take about configuring Home Assistant in Hass.io with the new Raspberry Pi 3 Model B+. Cheers!
