---
title: 'BSOD when capturing image with SCCM 2012 R2 SP1'
date: 2015-12-08T09:35:44+00:00
draft: false
tags: ['BSOD', 'OSD', 'SCCM', 'System Center', 'Windows 10']
description: ""
cover:
  image: ""
  alt: ""
---

I was capturing a new Windows 10 TH2 (1511) image with SCCM 2012 R2 SP1 CU2 when suddenly the capturing process stops and ends with a Blue Screen of Death: "SYSTEM\_THREAD\_EXCEPTION\_NOT\_HANDLED".

**Current environment:** SCCM 2012 R2 SP1 CU2 Primary Site Local Distribution Point Windows Server 2012 R2 OS Based on Hyper-V 2008 R2 and 2012 R2.

Windows 10 Template on Hyper-V Server 2008 R2 Cluster with VM Version 1.

Firstly I thought that the boot image was corrupt or not working, so I tried to recreate the image using [the following post](http://blogs.technet.com/b/brandonlinton/archive/2015/07/30/windows-10-adk-boot-image-updates-for-configuration-manager.aspx).

Unfortunately, the BSOD comes up with both boot images.

**Solution:** Use a Generation 2 VM instead of a Generation 1 VM.
