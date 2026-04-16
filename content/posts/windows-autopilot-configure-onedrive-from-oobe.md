---
title: 'Windows Autopilot - Configure OneDrive from OOBE?!'
date: 2017-07-04T17:30:12+00:00
draft: false
tags: ['Autopilot', 'DEP', 'Enrollment', 'Intune', 'MDM', 'Windows', 'Windows 10']
description: ""
cover:
  image: ""
  alt: ""
---

![Windows AutoPilot OneDrive](/images/2017/07/windowsautopilotonedrive1.png)Recently Microsoft introduced Windows Autopilot.

This is a feature where you can register your corporate devices and where users can use their internet connection to sign in with their Azure AD credentials.

The device is automatically enrolled with MDM like Intune and will receive apps and policies from there.

According to [Microsoft's recent blog post](https://blogs.technet.microsoft.com/ausoemteam/2017/07/04/coming-soon-to-a-pc-near-you-windows-autopilot/) and instruction video, a user needs to insert their WiFi password as the device will get the configuration from MDM and is already enrolled, without having the option to change the MDM provider or enroll the device as a personal device.

**The device really becomes a corporate-owned device**. This looks a bit like the [Apple Device Enrollment Program](https://www.apple.com/business/dep/). One of the interesting parts of that instruction video, is that it looks like OneDrive can be pre-configured from OOBE as well:

![WindowsAutoPilotOneDrive.PNG](/images/2017/07/windowsautopilotonedrive.png) I hope that Microsoft will further expand the possibilities of this service. What I would like to see is that the device can cache/download applications and settings from Intune during the factory imaging process. This ensures that applications, policies and settings are pre-loaded on a device and don't need to be downloaded anymore. This will dramatically decrease network bandwidth and deployment time.
