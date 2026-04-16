---
title: 'Unknown Devices when installing Hyper-V on Windows 10'
date: 2017-09-11T15:00:06+00:00
draft: false
tags: ['Credential Guard', 'Device Guard', 'Hyper-V', 'Windows', 'Windows 10']
description: ""
cover:
  image: ""
  alt: ""
---

The following unknown device IDs will pop-up when you run the script or when you open Device Manager:

> ROOT\\VMBUS\\0000 ROOT\\VID\\0000 ROOT\\VPCIVSP\\0000 ROOT\\STORVSP\\0000 ROOT\\SYNTH3DVSP\\0000

If you want to find all Unknown Devices, open PowerShell as an Administrator and run:

```powershell
Get-WmiObject Win32_PNPEntity | Where-Object { $_.ConfigManagerErrorCode -ne 0} | Select DeviceID
```

On my work notebook, all drivers were correctly populated so it had to be something with my test laptop. It's a fresh Windows 10 machine deployed by a Task Sequence - enabled with Device Guard and Credential Guard.

**Solution**: During the installation I've installed the **Microsoft-Hyper-V-Hypervisor** feature on Windows 10. You also need to install the **Microsoft-Hyper-V-Services** if you want to have those drivers installed as well.
