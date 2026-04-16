---
title: 'Troubleshoot BSOD after deploying driver package in SCCM 2012 R2'
date: 2015-12-01T11:00:21+00:00
draft: false
tags: ['0x0000007e', 'BSOD', 'ConfigMgr', 'Driver Package', 'SCCM', 'System Center', 'Troubleshooting', 'Windows']
description: ""
cover:
  image: ""
  alt: ""
---

During an Operating System Deployment in SCCM 2012 R2, new notebook models crashed after installing the driver package. I couldn't see the BSOD code because I wasn't able to boot the computer in safe mode, but after taking some pictures with my phone of the BSOD screen, I found out that the error code was **0x0000007e**.

The next step: how are you going to troubleshoot 160 drivers that you deployed to those models with your new driver package?

You could delete the original driver package and create a new one and insert the drivers one by one.

That could be very time consuming.

**Installing multiple drivers with dpinst.exe** Our driver package was nicely ordered by the manufacturer. So I had like 15 folders per driver set. For example: - Audio - Bluetooth - LAN - WLAN I want to troubleshoot all the drivers in those folders because it's easier to tell the manufacturer that they need to fix there "Audio" drivers rather than telling that the task sequence crashes on the driver package because of a faulty driver.

1. Download and install [the Windows Driver Kit](http://msdn.microsoft.com/en-US/windows/hardware/gg454513). The Windows 8.1 kit is for this purpose compatible with Windows 7. Don't forget to check the installation directory of the kit during the installation.
2. We need to copy **dpinst.exe** from the <InstallDir>\\redist\\DIFx subdirectory. Copy it to a share that is easy to map with the "net use" command later. For example: \\\\Server\\Share\\dpinst.exe
3. Create a **DPInst.xml** file with UTF-8 encoding. UTF-8 encoding is an option in the Save As screen in Notepad.
4. Add the following code to the DPInst.xml file to troubleshoot the Audio driver folder:

```xml
<?xml version="1.0" ?> <dpinst> <!-- The following search and subDirectory elements direct DPInst to search all subdirectories (under the DPInst working directory) to locate driver packages. --> <search> <subDirectory><strong>Audio</strong></subDirectory> </search> </dpinst>
```

5. Copy the contents of your driver package to your share, for example \\Server\Share. Make sure you have a structure like \\Server\Share\Audio, to troubleshoot the audio drivers.
6. Change the task sequence to "Auto Apply Drivers" so that your device will miss some drivers, but your deployment should finish. You have a test device after the deployment that can be used for further troubleshooting. On your test device, open a PowerShell prompt and run the following code. or create a small script:

```powershell
net use L: \\Server\Share L:\dpinst.exe /F
```

7. After running the code above, you'll see a screen where the drivers are being installed. After installing the drivers, reboot your test device.
8. **Do this again for the next driver folder:** Change the subdirectory in the **DPInst.xml** file from Audio to for example Bluetooth to test the Bluetooth drivers. Repeat the PowerShell code, install the drivers and reboot the test device again to find out which driver folder is causing the Blue Screen of Death.

Cheers!
