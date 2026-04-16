---
title: 'NAT Switch now built into Hyper-V! - Windows 10 Fall Creators Update'
date: 2017-10-20T10:00:31+00:00
draft: false
tags: ['Microsoft', 'Windows']
description: ""
cover:
  image: ""
  alt: ""
---

**With the new Windows 10 Fall Creators Update, Microsoft finally added a built-in NAT Switch into Hyper-V!

This gives Hyper-V Virtual Machines access to the computer's network. ****The new switch automatically assigns IP address to your Virtual Machines, so no need to run your own DHCP server anymore!** In older versions of Windows 10, [it was still required to create the Virtual Switch yourself](http://cloudenius.com/2017/09/24/create-a-hyper-v-nat-switch-with-powershell-the-easy-way/), but this required static IP address assignment in the OS or the installation of a DHCP server.

Not the most elegant option.

The switch is named "Default Switch" and cannot be changed in the Hyper-V Virtual Switch Manager:

![The Default Switch Virtual Network in the Hyper-V Virtual Switch Manager](/images/2017/10/hyperv-defaultswitch.png)

_The Default Switch Virtual Network in the Hyper-V Virtual Switch Manager_ According to the info message: "The Default Network switch automatically gives virtual machines access to the computer's network using NAT (network address translation)." I'm happy that Microsoft finally introduced this as it was already available in other 3rd Party solutions and a good argument why some people didn't want to migrate to Hyper-V.

Now they can! I wasn't able to find an official statement of Microsoft on this new feature, but I'm sure it will be published soon.

What do you think of this new feature?

Are you going to migrate from VMware or other solutions to Hyper-V?

Let me know in the comments section!

Cheers, Jean-Paul
