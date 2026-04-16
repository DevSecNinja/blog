---
title: 'AMD drivers are not functioning properly after updating Dell Latitude E6540 BIOS to A8/A10'
date: 2014-07-21T09:43:56+00:00
draft: false
tags: ['AMD', 'BIOS', 'Dell', 'Drivers', 'General', 'Intel', 'Latitude', 'Microsoft']
description: ""
cover:
  image: ""
  alt: ""
---

I updated my Dell Latitude E6540 BIOS to A10 today. After updating, the screen stays black after rebooting. If you reboot your PC, your resolution has changed and the drivers are not working anymore. Opening the AMD Catalyst Control Center gives the error “AMD drivers are not functioning properly”.

**Solution:** go to the Dell website. Click the Support page and type your Service Tag. Download the newest AMD and Intel graphics drivers. I installed the AMD driver after installing the Intel driver. You don’t have to delete the old driver. Reboot after installing the 2 drivers. Your notebook should work as before.
