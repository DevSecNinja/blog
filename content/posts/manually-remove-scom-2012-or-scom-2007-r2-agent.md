---
title: 'Manually remove SCOM 2012 or SCOM 2007 R2 Agent'
date: 2015-05-01T15:00:13+00:00
draft: false
tags: ['2007', '2012', 'Agent install', 'Operations Manager', 'System Center']
description: ""
cover:
  image: ""
  alt: ""
---

I was doing a migration project from System Center - Operations Manager 2007 to System Center - Operations Manager 2012 R2.

Some computers had troubles with the upgrade of the agent. I first tried to do a client push deployment. 80 % of the installations succeeded, but I had a couple of computers with failed installations/upgrades. 1.

Start the agent installation manually on the failed computer.

Run the MOMAgent.msi installer. 2.

Click "Next".

Accept the terms and click "I agree". **3\.

Notice the "Upgrade" button instead of the "Install" button.** 4.

Close the setup and check the solution below.

**Solution:** I was able to fix this to remove the product registry key of the SCOM 2007 Agent. You can find it at HKEY\_CLASSES\_ROOT\\Installer\\Products\\. Search for a key with ProductName "System Center Operations Manager 2007 R2 Agent".

**Back-up your registry** and remove the key. Try the setup again and notice the "Next" button instead of the "Upgrade" button. The agent push will work now.
