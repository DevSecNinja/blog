---
title: 'Windows 10 - Intel Bluetooth can''t connect to devices after reboot in TH2'
date: 2015-12-02T16:15:24+00:00
draft: false
tags: ['Bluetooth', 'Driver', 'Intel', 'TH2', 'Threshold 2', 'Windows', 'Windows 10']
description: ""
cover:
  image: ""
  alt: ""
---

Recently I had an issue with my work notebook, a Dell Latitude E6540. After upgrading to the new Windows 10 TH2 version, my Bluetooth keyboard and headset started couldn't connect after a shutdown. I had to reconnect the Bluetooth devices again to temporarily fix it. I was looking for a recent driver for my Intel Centrino Advanced-N 6235 network card, but it was already up-to-date because of a manual Windows Updates action I did after the upgrade to TH2. I realized that my "Intel(R) Wireless Bluetooth(R)" wasn't up-to-date.

The driver date was from 2013. I don't know why Microsoft or Intel didn't update that driver during the installation of the Windows Updates.

This was an easy fix:

1. Open Device Manager.
2. Find the "Intel(R) Wireless Bluetooth(R)" under the Bluetooth section.
3. Right click on the on the "Intel(R) Wireless Bluetooth(R)" item and click on "Update driver software".
4. Voila, Microsoft installed the 2015 driver for me which fixes the problem.

Cheers!
