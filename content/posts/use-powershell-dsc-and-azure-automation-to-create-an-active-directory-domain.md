---
title: 'Use PowerShell DSC and Azure Automation to Create an Active Directory Domain'
date: 2018-07-22T13:00:45+00:00
draft: false
tags: ['Azure', 'Azure Automation', 'Desired State Configuration', 'DSC', 'IaaS', 'PowerShell', 'Virtual Machines']
description: ""
cover:
  image: ""
  alt: ""
---

Because of the recent [domain change of my blog](http://DevSecNinja.com/2018/07/19/welcome-to-cloudenius-com/), I decided to completely start over again with my lab in Azure. I've been working with Desired State Configuration Configs in Azure for quite a few years, but never used them for my own lab environment.

It felt a bit overkill to do that, but now I wanted to start over and do everything right.

This step-by-step installation guide explains how to create a DSC Configuration in Azure Automation and how to apply this on your domain controller in Azure.

## Prerequisites

- **Azure Automation Account**
  - Including these credentials:
    - DomainAdminCredential
    - SafeModePassword (Pick a random username)
  - Including these variables:
    - DomainName - Contains the domain name for Active Directory (e.g. mylab.DevSecNinja.com)
  - Including these modules from the Modules Gallery:
    - xActiveDirectory
    - xStorage
    - xPendingReboot
- **An Azure Virtual Machine that will be the domain controller, with:**
  - A data disk
  - Ensure you disable caching on both disks as that's required for domain controllers running in Azure

## Installation Guide - Step-by-Step

### Configuring Azure DSC

1. Ensure you've followed the prerequisites steps above, as we depend on it during the installation guide.
2. Create the following folder structure on your machine:
   - DSC
     - DSC_AD_Domain
3. Copy/Paste _Script 1 - DSC_AD_Domain.ps1_ from below and save it in the DSC\_AD\_Domain folder.
4. Open the Azure Portal, open _Automation Accounts_ and click on the _Automation Account_ you've created based on the prerequisites. Open _DSC Configurations_, click the _Add Configuration_ button and upload the DSC_AD_Domain.ps1 script.
5. After importing the script, you should now see it in your DSC Configurations. Click on the script and click on the _Compile_ button: ![chrome_2018-07-22_13-50-36](/images/2018/07/chrome_2018-07-22_13-50-36.png)
6. Wait for a couple of minutes for the compilation to complete. Go back to the Azure Portal and ensure that the last compilation has completed successfully: ![chrome_2018-07-22_13-52-41](/images/2018/07/chrome_2018-07-22_13-52-41.png)
7. Good job! You've compiled the DSC Configuration. We can now apply this configuration to a Virtual Machine in Azure.

### Apply the DSC Configuration to your Virtual Machine

1. Browse and open your Automation Account in the Azure Portal.
2. Click the _DSC Nodes_ tab.
3. Click the _Add Azure VM_ button.
4. Select the Virtual Machine you want to manage with DSC and click the _Connect_ button: ![chrome_2018-07-22_13-58-17](/images/2018/07/chrome_2018-07-22_13-58-17.png)
5. The Registration Blade will open. Make sure you select the new DSC Configuration you've recently uploaded.

Also ensure you select "ApplyAndAutoCorrect" as the Configuration Mode. DSC will now take care of the configuration and ensure it will stay compliant.

It's very important to select "Reboot Node if Needed", otherwise the domain creation process cannot proceed as it will need a reboot there.

Be careful with this setting in production though.

Click the _OK_ button so Azure can do it's magic.

![chrome_2018-07-22_13-59-41](/images/2018/07/chrome_2018-07-22_13-59-41.png)
6. Go back to the DSC Nodes tab and wait for the system to show up there. Also keep an eye on the status of the machine there. ![chrome_2018-07-22_14-11-39](/images/2018/07/chrome_2018-07-22_14-11-39.png)

It's a wrap! Thanks for reading this blog post. Let me know if you have any questions in the comments section. Cheers!

## Script 1 - DSC_AD_Domain.ps1

This script was originally [written by Michael Green](https://www.powershellgallery.com/packages/DomainControllerConfig/0.3.1/DisplayScript) and modified by me.

```powershell
configuration DSC_AD_Domain
{
    # Import the modules needed to run the DSC script
    Import-DscResource -ModuleName 'xActiveDirectory'
    Import-DscResource -ModuleName 'xStorage'
    Import-DscResource -ModuleName 'xPendingReboot'
    Import-DscResource -ModuleName 'PSDesiredStateConfiguration'

    # When using with Azure Automation, modify these values to match your stored credential names
    $DomainAdminCredential = Get-AutomationPSCredential -Name 'DomainAdminCredential'
    $SafeModePassword = Get-AutomationPSCredential -Name 'SafeModePassword'
    $DomainName = Get-AutomationVariable -Name 'DomainName'

    # Configuration
    node localhost
    {
        WindowsFeature ADDSInstall
        {
            Ensure = 'Present'
            Name = 'AD-Domain-Services'
        }

        xWaitforDisk Disk2
        {
            DiskId = 2
            RetryIntervalSec = 10
            RetryCount = 30
        }

        xDisk DiskF
        {
            DiskId = 2
            DriveLetter = 'F'
            DependsOn = '[xWaitforDisk]Disk2'
        }

        xPendingReboot BeforeDC
        {
            Name = 'BeforeDC'
            SkipCcmClientSDK = $true
            DependsOn = '[WindowsFeature]ADDSInstall','[xDisk]DiskF'
        }

        xADDomain Domain
        {
            DomainName = $DomainName
            DomainAdministratorCredential = $DomainAdminCredential
            SafemodeAdministratorPassword = $SafeModePassword
            DatabasePath = 'F:\NTDS'
            LogPath = 'F:\NTDS'
            SysvolPath = 'F:\SYSVOL'
            DependsOn = '[WindowsFeature]ADDSInstall','[xDisk]DiskF','[xPendingReboot]BeforeDC'
        }

        Registry DisableRDPNLA
        {
            Key = 'HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp'
            ValueName = 'UserAuthentication'
            ValueData = 0
            ValueType = 'Dword'
            Ensure = 'Present'
            DependsOn = '[xADDomain]Domain'
        }
    }
}
```
