---
title: 'Cisco - Catalyst Express 500 PoE switch not working with Windows Vista/7/8/8.1'
date: 2013-10-17T18:59:12+00:00
draft: false
tags: ['bug', 'Catalyst 500', 'Cisco', 'General']
aliases:
    - /2013/10/17/cisco-catalyst-express-500-poe-switch-not-working-with-windows-vista/7/8/8-1/
description: ""
cover:
  image: ""
  alt: ""
---

**I was installing a Cisco Catalyst Express 500 switch, but I failed a couple of times to enter the setup menu.

When you try to restart the switch to factory default, you should get an IP address from the switch.

Mostly this is 10.1.1.2.

It works only with my old Windows XP laptop, not with my Windows 8.1 machines.** To fix this problem, set your IP address to: IP address: 10.1.1.2 Subnetmask: 255.255.255.0 Default gateway: 10.1.1.1 Try again to reset your switch to factory settings and you will now have access to the website of the switch.

Good luck!

If you have any questions, let me know!
