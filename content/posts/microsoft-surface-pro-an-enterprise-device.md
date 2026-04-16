---
title: 'Microsoft Surface Pro - An enterprise device?'
date: 2016-07-20T16:30:20+00:00
draft: false
tags: ['Enterprise', 'Hardware', 'Kensington', 'On-Screen Keyboard', 'Surface Pro 4', 'TPM']
description: ""
cover:
  image: ""
  alt: ""
---

Microsoft is pushing everything to an "As a Service" model. I think that's great because of - for example - staying in control of licenses and costs.

Microsoft recently announced the ["Windows 10 as a Service" and "Surface as a Service"](https://blogs.windows.com/windowsexperience/2016/07/12/announcing-new-subscription-options-for-windows-10-and-surface-for-businesses/) services.

The Surface Pro 4 is a fantastic device, but in my opinion lacks a couple of essential features to classify it as an Enterprise Device. I worked with large organizations and the first 2 check boxes on the acceptance list are:

- The device needs a Kensington lock
- The user needs to provide the BitLocker PIN to start the device

I think those points are really necessary for an enterprise device. Without a Kensington lock, a device can be easily stolen during a short break. (Or do you take your Surface with you when going to the toilet?!) Most organizations require that a BitLocker PIN is needed to unlock the device.

It's possible to [use an on screen keyboard](https://blogs.technet.microsoft.com/askpfeplat/2014/07/13/bitlocker-pin-on-surface-pro-3-and-other-tablets/) during the preboot screen, but I don't see any business using this. [Mark Morowczynski from Microsoft says](https://blogs.technet.microsoft.com/askpfeplat/2014/07/13/bitlocker-pin-on-surface-pro-3-and-other-tablets/) that this is because an attacker can connect to the machine using DMA or retrieve the secrets from memory.

The Surface Pro 4 DMA connector is soldered on the motherboard, but the memory can still be easily stolen without a Kensington lock!

So what do you think?

Should Microsoft add the Kensington lock to the Surface Pro 5?
