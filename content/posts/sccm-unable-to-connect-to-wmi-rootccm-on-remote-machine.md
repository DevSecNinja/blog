---
title: 'SCCM - Unable to connect to WMI (root\ccm) on remote machine'
date: 2014-12-28T18:13:09+00:00
draft: false
tags: ['Agent install', 'CCM', 'Client install', 'Configuration Manager', 'SCCM', 'System Center']
description: ""
cover:
  image: ""
  alt: ""
---

### Problem

The following error occurs in the ccm.log when doing a remote client install:

> Unable to connect to WMI (root\\ccm) on remote machine "COMPUTER"

### Solution

Allow the following rules in Windows Firewall: **Outbound and inbound: File and Printer Sharing** **Inbound: Windows Management Instrumentation (WMI)**
