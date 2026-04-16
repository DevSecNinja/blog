---
title: 'Xbox One Achievements Not Working'
date: 2018-03-03T16:30:31+00:00
draft: false
tags: ['Xbox', 'Xbox Achievements', 'Xbox Live', 'Xbox One', 'Xbox One X']
description: ""
cover:
  image: ""
  alt: ""
---

Recently my Xbox Achievements stopped popping up for Forza Motorsport 7 [as described before in this post](http://cloudenius.com/2017/12/31/xbox-one-x-switching-from-ps4-pro/).

Achievements for other games where working fine but after a while also Battlefield 1 achievements where not popping up anymore.

After quitte some troubleshooting, I found out that the Pi-Hole Ad-Block DNS service installed on my Raspberry Pi was blocking the achievements traffic to the Xbox Servers.

The strange thing is that Microsoft is using the same server addresses for telemetry data!

So blocking telemetry data also blocks achievements, while all other Microsoft services are working fine.

Even the Network Tester on the Xbox told me that the connection was working fine.

After I changed the DNS server settings on the Xbox to the Google DNS Servers (8.8.8.8 and 8.8.4.4), the achievements started to pop-up slowly.

One achievement in Forza triggered all other achievements as well resulting in 9 achievement unlocks at the same time.

You can follow this guide on the Microsoft Support site to change the DNS Settings on your Xbox One X: [Network settings on Xbox One](https://support.xbox.com/en-US/xbox-one/networking/network-settings).

Let me know if this solved your issues too.

Cheers!
