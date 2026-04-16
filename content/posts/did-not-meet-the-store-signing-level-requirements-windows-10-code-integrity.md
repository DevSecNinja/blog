---
title: '*driver* did not meet the Store signing level requirements - Windows 10 Code Integrity'
date: 2018-04-21T09:00:20+00:00
draft: false
tags: ['Code Integrity', 'Device Guard', 'Endpoint Protection', 'Microsoft', 'Security', 'Store signing level requirements', 'Symantec', 'Windows', 'Windows 10']
description: ""
cover:
  image: ""
  alt: ""
---

**This error message is related to Device Guard Code Integrity in Windows 10 and shows up in the Event Viewer under the Code Integrity folder.

As of writing this article, the error message is not described in online documentation of Microsoft.** In the current scenario, the built-in Windows 10 apps like the Calculator, Alarms & Clock or the Photos app will instantly crash after opening it.

This error message tells that the sysfer.dll is not trusted by Microsoft and therefore cannot interfere with the Alarms & Clock app.

Sysfer.dll is the driver that Symantec Endpoint Protection uses with their Application & Device Control feature to control which processes are allowed to run.

> Code Integrity determined that a process (\\Device\\HarddiskVolume3\\Program Files\\WindowsApps\\Microsoft.WindowsAlarms\_10.1709.2621.1000\_x64\_\_8wekyb3d8bbwe\\Time.exe) attempted to load \\Device\\HarddiskVolume3\\Windows\\System32\\sysfer.dll that **did not meet the Store signing level requirements.**

There are a couple of workarounds to 'solve' the issue:

1. **Use Device Guard Code Integrity**: exclude the C:\\Program Files\\WindowsApps\\\* location from the Application & Device Control feature. If that doesn't work (which I'm currently looking into), remove the Application & Device Control feature from the Symantec installation.
2. **Use Symantec Application & Device Control**: disable User Mode Code Integrity by removing the "Enabled:UMCI" part in the CI Policy.

Even though Symantec [states that they are fully supporting Code Integrity](https://support.symantec.com/en_US/article.TECH235458.html), I don't see how that's going to work out because Device Guard doesn't trust the Symantec driver. I also tried to remove the "Required:Enforce Store Applications" option from the CI Policy which didn't fix the issue.

Even if you add the driver to your Code Integrity Policy which runs in Audit mode, it will not work.

Otherwise it would show the following error message:

![Afbeeldingsresultaat voor Windows 10 code integrity policy not trusted](https://docs.microsoft.com/en-us/windows/security/threat-protection/device-guard/images/dg-fig23-exceptionstocode.png)

_Source: [Microsoft Docs](https://docs.microsoft.com/en-us/windows/security/threat-protection/device-guard/steps-to-deploy-windows-defender-application-control)_ ".. or violated code integrity policy. However, due to code integrity **auditing** policy, the image was allowed to load." Hope this explains the error message and the options you have. Cheers!
