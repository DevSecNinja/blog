---
title: 'Script for package failed with exit code 4 in SCCM 2012 R2'
date: 2015-12-10T16:00:36+00:00
draft: false
tags: ['BAT', 'Deployment', 'Package', 'SCCM', 'System Center']
description: ""
cover:
  image: ""
  alt: ""
---

**Problem:** In SCCM 2012 R2 SP1 CU2, I've created a package that deploys some files such as wallpapers with a .BAT file. When I check the execmgr.log, I see the following error:

> Script for Package:PR######, Program: Run Script failed with exit code 4.

**Solution:** Under the program in SCCM, change "Run" from "Hidden" to "Normal".
