---
title: 'Install the Windows 10 Fall Creators Update on your GPO-enabled machine'
date: 2017-10-14T10:30:14+00:00
draft: false
tags: ['Windows']
description: ""
cover:
  image: ""
  alt: ""
---

So your Group Policy (GPO) settings do not allow you to upgrade to the Windows 10 Fall Creators Update and you have local administrative access on your machine?

The registry fix from below will change this!

Copy the registry fix from below and save it as fix.reg with Notepad. (Make sure you don't save it as fix.reg.txt!) Right click on the file and click "Merge".

You should now have access to Settings -> Update & Security -> Windows Insider Program.

Enroll your device in the program (with your Microsoft account!) and select "Just fixes, apps and drivers" from the dropdown - which will enroll you in the Release Preview Ring.

Go to Settings -> Update & Security -> Windows Updates and select "Check online for updates from Microsoft Update".

It will take some time before the Fall Creators Update pops up here.

When the Windows Insider Settings are greyed out again after several minutes, your GPO settings were re-applied and you need to rerun the fix.reg file.

Run the fix.reg file every hour or so and check again for Windows Updates.

After a couple of hours you should be able to enjoy the Fall Creators Update!

### Registry Fix:

`Windows Registry Editor Version 5.00` `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsSelfHost\Applicability]` `"EnablePreviewBuilds"=dword:00000002` `"IsBuildFlightingEnabled"=dword:00000001` `"IsConfigExpFlightingEnabled"=dword:00000001` `"IsConfigSettingsFlightingEnabled"=dword:00000001` `"SuspensionStartTime"=-` `"SuspensionEndTime"=-` `[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\PreviewBuilds]` `"AllowBuildPreview"=dword:00000001` `"EnableConfigFlighting"=dword:00000001` `[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\DataCollection]` `"CommercialId"=-`
