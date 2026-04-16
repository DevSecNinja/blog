---
title: 'SCCM - IIS Error code 403 13 2148081683'
date: 2016-03-21T16:00:50+00:00
draft: false
tags: ['CRL', 'IIS', 'SCCM', 'SSL', 'Windows']
description: ""
cover:
  image: ""
  alt: ""
---

## Problem:

If you see the following error in your IIS Logs (C:\\inetpub\\logs\\LogFiles\\W3SVC1), it's possible that the CRL of your Certificate Authority isn't reachable or valid anymore: <IP Address> GET /SMS\_MP/.sms\_aut MPLIST 443 - <IP Address> SMS\_MP\_CONTROL\_MANAGER - 403 13 2148081683 5701 18

## Solution:

Export a certificate from your personal certificate store, for example, an SCCM Client Certificate to your C: drive. Open a command prompt with elevated rights and type:

> certutil -url "C:\\Certificate.cer"

Check if the CRL can be verified. Open the CRL manually and check that the BASE and DELTA CRL's aren't expired. In this case, the AD CS service wasn't started and the Delta CRL's were not up-to-date. The service may have been crashed because the startup type was set to "Automatic".
