---
title: 'Enable Hyper-V during Task Sequence in SCCM 2012 R2'
date: 2016-01-25T17:30:16+00:00
draft: false
tags: ['Deployment', 'Device Guard', 'Hyper-V', 'SCCM', 'System Center']
description: ""
cover:
  image: ""
  alt: ""
---

Because I wanted to configure Device Guard with Windows 10, I need the Hyper-V Hypervisor to be enabled on Windows 10. I tried to do this with DISM and an answer file, but it's not possible to enable Hyper-V during the Task Sequence Deployment because Hyper-V requires a couple of reboots.

## Solution

Create a new "Set Task Sequence Variable" task in your Task Sequence. This will run the PowerShell command after the Task Sequence ends. I've set this task before enabling the Driver Package, but it should be possible to place this task anywhere you like.

**Task Sequence Variable**: SMSTSPostAction **Value**: powershell -ExecutionPolicy ByPass -Command "Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V-Hypervisor -all -NoRestart;Disable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V-Tools-All,Microsoft-Hyper-V-Services -NoRestart" This will do the following:

1. Enable all the Hyper-V Features after the deployment
2. Remove the Hyper-V Tools and Services (Management Tools) afterwards. I found out that this is the best way to only add the Hyper-V Hypervisor.

You still need to reboot the system a few times to enable this feature. Because I enabled the BitLocker PIN, I can't reboot the machine because it will ask for a PIN a few times. **Screenshot:** ![Enable-HyperV](/images/2016/01/enable-hyperv1.png)
