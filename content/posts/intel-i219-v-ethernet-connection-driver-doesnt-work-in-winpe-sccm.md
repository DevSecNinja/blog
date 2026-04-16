---
title: 'Intel I219-V Ethernet Connection driver doesn''t work in WinPE (SCCM)'
date: 2015-11-25T21:00:59+00:00
draft: false
tags: ['ConfigMgr', 'Driver', 'I219-V', 'Intel', 'SCCM', 'System Center', 'WinPE']
description: ""
cover:
  image: ""
  alt: ""
---

Today I had an issue with one of our new notebook models at a client.

**Problem:** After you PXE-boot the device, the device doesn't get his advertisement from SCCM and goes in a reboot to the original OS.

If you open the command prompt with F8 during the boot image startup process, no IP address is shown after you type in the command "ipconfig".

The driver package from the manufacturer we used included a Windows 7 NIC driver, which was good for the install image.

In our System Center - Configuration Manager 2012 R2 (SCCM / ConfigMgr) environment, we used a WinPE version of 6.3.9600.16384 which is equal to Windows 8.1.

The "Intel(R) Ethernet Connection I217-LM" Windows 7 driver (NDIS62) doesn't work with the Windows 8.1 Boot Image (WinPE) we used.

This worked fine for older models like the "Intel(R) Ethernet Connection I217-LM" and the "Intel(R) Ethernet Connection I218-LM".

**Solution:** Add the NDIS64 as well as the NDIS62 version of the driver to your SCCM boot image (WinPE). After updating the boot image, your deployment will work again.

**Update:** Check the comments below as well for some tips! Cheers!
