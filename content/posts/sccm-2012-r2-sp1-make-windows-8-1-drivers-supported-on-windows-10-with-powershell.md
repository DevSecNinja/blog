---
title: 'SCCM 2012 R2 SP1 - Make Windows 8.1 drivers supported on Windows 10 with PowerShell'
date: 2015-07-23T15:25:56+00:00
draft: false
tags: ['Drivers', 'PowerShell', 'SCCM', 'System Center', 'Windows 10']
aliases:
    - /2015/07/23/sccm-2012-r2-sp1-make-windows-8-1-drivers-supported-on-windows-10-with-powershell/
description: ""
cover:
  image: ""
  alt: ""
---

I had an issue within my lab with deploying Windows 8.1 drivers to Windows 10 with SCCM 2012 R2 SP1. It isn't possible to make all Windows 8.1 drivers compatible with Windows 10 within the SCCM 2012 R2 SP1 console with just one click. Because I was running within a lab environment and I only had 2 driver packages for Windows 8.1 x64, I was able to make the drivers available for deployment to all platforms. You can do this with the magic of PowerShell:

## Solution

```powershell
Get-CMDriver | Set-CMDriver -RunOnAnyPlatform
```

_Note: make sure that all your drivers **are** compatible for all platforms. Make sure you have separate x64 and x86 Task Sequences and Driver Packages/Categories with drivers. Because I have separate Task Sequences/Driver Packages and categories for x64 and x86, it isn't a problem for me to have the drivers supported on all platforms._
