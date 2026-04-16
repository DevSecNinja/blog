---
title: 'Windows 10 - SCCM 2012 R2 SP1 fails with error 0x80070032'
date: 2015-07-23T11:22:31+00:00
draft: false
tags: ['Deployment', 'MDT', 'OSD', 'SCCM', 'Windows']
description: ""
cover:
  image: ""
  alt: ""
---

I was deploying Windows 10 with SCCM 2012 R2 SP1 and the task sequence failed after "Installing device drivers" with error code 0x80070032 (or 80070032). The "Auto Apply Drivers" task works fine, but doesn't install a lot of drivers. **The smsts.log file:**

> Dism failed with return code 50 Failed to add driver to driver store. Code 0x80070032 Failed to provision driver. Code 0x80070032 Exiting with return code 0x80070032

**Solution:**

- Make sure you're using the latest MDT version, compatible with Windows 10.
- Make sure you're using at least ADK 10.
- Check if your boot image has OS Version 10 or higher. If not, create a new boot image with MDT or ADK.
