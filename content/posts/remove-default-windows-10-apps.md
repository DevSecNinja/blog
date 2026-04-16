---
title: 'Remove default Windows 10 Apps'
date: 2016-05-15T07:00:44+00:00
draft: false
tags: ['Applications', 'Apps', 'Appx', 'Windows', 'Windows 10']
description: ""
cover:
  image: ""
  alt: ""
---

**WARNING:** **Removing Windows 10 Apps can make your system unstable.** I had issues with my NUC after removing some default applications. Don't do this in your master Enterprise image! Block apps with AppLocker instead. Use the following PowerShell command to check which Windows 10 Apps are installed:

```powershell
Get-AppxPackage | Select Name
```

Make sure that you get all the packages that you want to delete in one view. For example:

```powershell
Get-AppxPackage | Where {$_.Name -ilike "Microsoft.ZuneVideo" -or $_.Name -ilike "Microsoft.WindowsCamera"}
```

To remove those packages, pipe it to Remove-AppxPackage.

```powershell
Get-AppxPackage | Where {$_.Name -ilike "Microsoft.ZuneVideo" -or $_.Name -ilike "Microsoft.WindowsCamera"} | Remove-AppxPackage
```
