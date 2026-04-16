---
title: 'Lock screen image not showing - Windows 10 1703'
date: 2017-09-10T14:00:08+00:00
draft: false
tags: ['Configuration Manager', 'Deployment', 'SCCM', 'Windows', 'Windows 10']
description: ""
cover:
  image: ""
  alt: ""
---

Recently I was trying to apply a lock screen image with a GPO. I distributed the image to the C:/Windows/Web/Wallpaper directory and configured the Windows 10 GPO to that location.

After running the Windows 10 Task Sequence successfully, the default lock screen image came up. I was using a large image from the client so that it still looks good on bigger screens. I've found out that after resizing the image back to 1080P, the image was applied successfully after locking the machine.

Looks like a strange bug if you would ask me.

Cheers!
