---
title: 'WTH Thermostat - Error Code A2.2'
date: 2017-06-01T05:00:15+00:00
draft: false
tags: ['Misc', 'Thermostaat', 'Thermostat', 'Winterverblijf', 'WTH', 'Zomerverblijf']
aliases:
    - /2017/06/01/wth-thermostat-error-code-a2-2/
description: ""
cover:
  image: ""
  alt: ""
---

The underfloor heating and cooling system of my apartment is managed by a WTH thermostat. Last week had temperatures of 30+ °C, which is why I wanted to switch from heating to cooling the floor of my apartment. Somehow the instructions in the manual didn't work for me and ended up with error code A2.2. Of course - an error code that's not described in the manual. Below is an image of the WTH D9380 rF-t thermostat I have.

![d938020wth20comfort20rf-t20ruimtethermostaat](/images/2017/06/d938020wth20comfort20rf-t20ruimtethermostaat.jpg) I was advised to call the company that implemented the underfloor heating and cooling system, but hey.. "I'm a tech guy!". I found out that there is another icon for winter and summer configuration:

![WTH-WinterSummer](/images/2017/06/wth-wintersummer.png) Both icons where not visible on my display, just like the example above. I had to dig into the configuration to change the P01 parameter from 0 to 1. You can do that with the following steps (Dutch):

![WTH-ChangeParameters](/images/2017/06/wth-changeparameters.png) I know this post was not about IT, but hopefully I can help some people struggling with the same issue. Cheers!
