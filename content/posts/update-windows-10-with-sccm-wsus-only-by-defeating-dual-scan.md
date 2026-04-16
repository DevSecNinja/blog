---
title: 'Update Windows 10 with SCCM/WSUS only by defeating Dual Scan'
date: 2018-04-21T10:00:56+00:00
draft: false
tags: ['Dual Scan', 'PowerShell', 'SCCM', 'Updates', 'Windows', 'Windows 10', 'WSUS']
description: ""
cover:
  image: ""
  alt: ""
---

**With Windows 10 1607, Microsoft introduced Dual Scan functionality, which allows the computer to connect with Microsoft Updates besides using WSUS or SCCM. [Steve Henry from Microsoft](https://blogs.technet.microsoft.com/wsus/2017/05/05/demystifying-dual-scan/): "It is for the enterprise that wants WU to be its primary update source while Windows Server Update Services (WSUS) provides all other content." I've seen various blog posts not covering all the steps I had to take to ensure Windows only looks to SCCM/WSUS.

Especially covering Windows 10 deployments with System Center - Configuration Manager.**

## Step 1: Answer File

During the Out of the Box Experience (OOBE) of Windows 10, Windows will look for updates.

![zdp-oobe](/images/2018/04/zdp-oobe.png) As Group Policies are not available at the OOBE stage, it will grab them from the Microsoft Update servers. To ensure this doesn't happen, set the ProtectYourPC setting in your answer file to 3. The update message will still pop-up during OOBE, but it will not download the updates:

> <ProtectYourPC>3</ProtectYourPC>

## Step 2: Registry

After the computer comes out of OOBE, the user is able to login to the system. Normally it can take around 10 minutes or longer before the SCCM Client receives its policies and populates the WSUS Server in the registry.

If a user opens Settings and clicks on "Updates & Security", followed by "Check for Updates", Windows will actually start looking for updates with Microsoft Updates.

At some organizations, a technician will finish OOBE for the user and login for the first time to check for updates.

If the technician does that accidentally by the "Check for Updates" button instead of using the SCCM Client, the machine will get it's updates from Microsoft.

Therefore, ensure that you run the PowerShell code below during your Task Sequence.

You can keep the WUServer and WUStatusServer registry keys empty as the SCCM Client will set them automatically after the SCCM policy gets applied on the system.

```powershell
# Add required registry keys for Windows Updates
try {
    $WURegistryKeyPath = "HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate"

    # Add registry value UseWUServer - 1 to enable WSUS, 0 for Microsoft Update
    Write-Output "Adding HKEY_LOCAL_MACHINE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer value as DWORD with data 1"
    New-ItemProperty -Path (Join-Path -Path $WURegistryKeyPath -ChildPath "AU") -Name UseWUServer -PropertyType DWORD -Value 1

    # Add registry value WUServer -  to allow the SCCM client to fill in the WSUS Server
    Write-Output "Adding HKEY_LOCAL_MACHINE\Policies\Microsoft\Windows\WindowsUpdate\WUServer value as String with data "
    New-ItemProperty -Path $WURegistryKeyPath -Name WUServer -PropertyType String -Value ""

    # Add registry value WUStatusServer -  to allow the SCCM client to fill in the WSUS Server
    Write-Output "Adding HKEY_LOCAL_MACHINE\Policies\Microsoft\Windows\WindowsUpdate\WUStatusServer value as String with data "
    New-ItemProperty -Path $WURegistryKeyPath -Name WUStatusServer -PropertyType String -Value ""
}
catch [System.Exception] {
    Write-Output "An error occured while configuring Windows Updates"
}
```

## Step 3: Group Policies

### Set policy "Do not connect to any Windows Update Internet locations" to Enabled in your Group Policy.

This will ensure that Windows will not use Windows Update Internet locations.

### Set policy "Do not allow update deferral policies to cause scans against Windows Update" to Enabled in your Group Policy.

This policy is new and might require an update of your ADMX templates. If you don't want to import the ADMX templates, you can also use the registry which you can find on this great [Group Policy Search site](http://gpsearch.azurewebsites.net/).

### Set policy "Select when Feature Updates are received" and  "Select when Quality Updates are received" to "Not configured" in your Group Policy.

If you use the Microsoft Security Baseline or CIS Benchmarks, remove this policy from your baseline. Even setting this policy to disabled in your baseline will enable Dual Scan.

### Set policy "Do not include drivers with Windows Updates" to Enabled in your Group Policy.

Occasionally Windows will include drivers in Windows Updates. If you want full control of your drivers, set this policy.

## Step 4: Validate!

On a Windows 10 machine, open Settings and click on "Updates & Security". Click on "View installed update history" and ensure this is empty after a fresh deployment. Browse back to the Updates & Security menu and check for updates. Again, ensure no updates are getting installed. I advise to keep an eye on the updates that are getting applied on your system as I found my findings at step 1 and 2 after my initial tests. Open PowerShell and run the following command:

```powershell
(New-Object -ComObject "Microsoft.Update.ServiceManager").Services | select Name, IsDefaultAUService
```

Ensure that the IsDefaultAUService parameter for the "Windows Server Update Service" has the value of True. Open PowerShell and run the following command:

```powershell
Get-WindowsUpdateLog
```

Examine the log to ensure Windows is not connecting with Microsoft Updates. Hope you find this useful. Cheers!
