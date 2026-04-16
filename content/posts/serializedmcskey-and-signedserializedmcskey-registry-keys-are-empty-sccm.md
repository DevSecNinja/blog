---
title: 'SerializedMCSKey and SignedSerializedMCSKey registry keys are empty - SCCM'
date: 2015-12-14T17:15:28+00:00
draft: false
tags: ['Multicast', 'Registry', 'SCCM', 'System Center']
description: ""
cover:
  image: ""
  alt: ""
---

**Problem:** Sometimes it's possible that the registry keys SerializedMCSKey and SignedSerializedMCSKey in the HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\SMS\\MCS location are empty after a fresh installation or after reinstalling multicast.

**Solution:** Patience... It took like 5 or 6 hours to get those values populated by SCCM / WDS. I've searched for a way to force this, but I couldn't find anything online. I've tried to reboot both machines, without any luck. If you know a way to force this, please let me know.
