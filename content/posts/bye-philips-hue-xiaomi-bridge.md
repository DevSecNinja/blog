---
title: 'Bye Philips Hue & Xiaomi Bridge!'
date: 2019-08-03T12:30:06+00:00
draft: false
tags: ['ConBee', 'deCONZ', 'Domotica', 'Home Assistant', 'Home Automation', 'Reviews', 'Zigbee']
description: ""
cover:
  image: ""
  alt: ""
---

**My smart home journey started years ago with a simple Philips Hue configuration.

After integrating Home Assistant, I wanted to have some door/window sensors and temperature sensors. I bought the Xiaomi Aqara bridge and implemented all the sensors into Home Assistant. I quickly realized I now have two Zigbee bridges due to the fact that both Philips and Xiaomi want a 'customized' standard. ¯\\\_(ツ)\_/¯ I needed to do something...** I was using multiple bridges because I heard some stories about connection losses around some USB bridges.

As stability of the platform is crucial to me, I decided to hold back on the purchase until I saw this tweet from Franck: https://twitter.com/Frenck/status/1153634514402521088?s=20 Franck (or @Frenck) is a respected member of the Home Assistant community. I love his contributions to Hass.IO add-ons like the Spotify Connect and the Node-RED add-ons. A recommendation from him means a lot to me, so I decided to take the jump and order the Dresden Elektronic ConBee II stick.

This stick is able to integrate with products from Philips Hue, IKEA Trådfri, OSRAM SYLVANIA, Samsung SmartThings, Xiaomi Aqara and many more.

## Configure the deCONZ Add-on

The weekend after the arrival of the gateway, I started with the configuration in Home Assistant & Hass.IO. I installed the deCONZ Hass.IO plugin which was easy-peasy. The deCONZ add-on asks you to configure a device in the config. This is usually something like:

- /dev/ttyAMA0
- /dev/ttyUSB0
- /dev/ttyACM0

You can get this hardware ID if you go to Hass.IO => System => Hardware. In my case, only the following hardware IDs showed up:

1. /dev/ttyACM0
2. /dev/serial/by-id/usb-dresden\_elektronik\_ingenieurtechnik\_GmbH\_ConBee\_II\_DE<\*>

The first hardware ID didn't work in my case. As this hardware ID is mentioned in the documentation of deCONZ, I thought there must be something wrong. But the second hardware ID worked fine for me. This ID doesn't seem to work with ZHA, so I stick with deCONZ.

## Discover your devices

Now you have configured the add-on. You can click on the _Open Web UI_ button on the deCONZ Hass.IO add-on page.

This will show you the Web UI of deCONZ so you can start with the configuration of your devices. I was surprised to see that **all** my lights, switches and sensors are supported with deCONZ: \[gallery ids="2578,2579,2580" type="rectangular"\] So far this setup has been pretty reliable for me.

It works stable and the range of the Zigbee Gateway is pretty good.

Somehow the range is even better than the big Xiaomi Gateway.

## Troubleshooting

I did ran into an issue by doing a factory reset of my Philips Hue Light bulbs. You can find step-by-step instructions online about how you can reset your bulbs by using a Hue Dimmer switch, but it didn't work for me as most of the sites are missing one crucial step.

You need to follow the steps below very carefully: _First, **turn off the light bulb by disconnecting the bulb from power** by using a physical light switch on the wall (very important!).

Otherwise the factory reset might not work, which was driving me nuts as most online instructions don't provide this info._ _Second, turn on the bulb and ensure that all the other bulbs are turned off.

Hold the Hue Dimmer switch close to the bulb.

Press and hold the 1st (On / I in some countries) and the and 4th (Off / O in some countries) buttons simultaneously for about 10 seconds, until the bulb starts blinking on and off.

If the bulb stopped blinking (it will normally turn fully on again after reset) and the green LED on the remote (top left of the remote) blinked green - your bulb is reset.

You can now discover the bulb with deCONZ._

## Good bye

So long, Philips Hue and Xiaomi Aqara Bridge! ![Image](https://pbs.twimg.com/media/EAd-pqBX4AEoenp?format=jpg&name=4096x4096)
