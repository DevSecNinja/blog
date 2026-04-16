---
title: 'Azure - Windows Server Licensing Explained'
date: 2017-12-02T11:00:19+00:00
draft: false
tags: ['Azure', 'IaaS', 'KMS', 'Licensing', 'Windows', 'Windows Server']
description: ""
cover:
  image: ""
  alt: ""
---

**This article describes the licensing options you have when you want to deploy Windows Server Virtual Machines in Azure. It's getting complicated when you start using the Hybrid Use Benefit solution, so always contact Microsoft or your licensing supplier. ****Please note that I will not answer any licensing questions.**

## Built-in Licensing for Windows Server

This type of licensing is by-far the most easy to use but it can be an expensive solution. You deploy an Azure Virtual Machine from the Portal or PowerShell and the licensing costs are automatically included with the Virtual Machine costs. But what if you want to use your existing KMS licenses which you've bought with your Enterprise Agreement? Or you want to use Windows Server Standard licenses instead of Datacenter licenses?

## Hybrid Use Benefit

The Hybrid Use Benefit is a 'new' way of licensing. Microsoft will not activate your machine and you need to use your own activation method. That can be a KMS Server or a MAK-key. You also need to set the Hybrid Use Benefit flag from the Azure Portal or in your JSON template: "licenseType": "Windows\_Server". If you forget to set this configuration, you have to recreate the Virtual Machine. As of today, there is no way to change this value without recreating the Virtual Machine.

![HUB-configuration](/images/2017/11/hub-configuration.png)

### Using your own MAK-key, KMS Server or AD based activation

The best way to enforce the MAK-key or KMS Client key from the organization on a large scale is to use PowerShell DSC. PowerShell DSC will check every couple of minutes to see if the server is activated. If not, it will replace the key and try to reactivate. Use the script below as an example for your DSC Configuration.

### Need Windows Server Standard?

Most of the traditional Windows Server Standard licenses are bought with an Enterprise Agreement (EA) as a package deal with Microsoft. If you want to use those licenses in Azure, you have to create and maintain your own Windows Server image and upload it to Azure. As of today, you cannot grab a Windows Server Standard VM from the Azure Marketplace and deploy that.

## What Microsoft needs to improve:

- Please allow organizations to use Windows Server Standard images so there is no need to maintain own custom images
- Allow organizations to convert there current Windows Server licenses to Azure licenses more easily
- Activate Windows Server Standard licenses with Azure KMS which removes the need to host a KMS server

## DSC Configuration for Windows Server Activation in Azure

```powershell
Script ActivateWindows
{
    DependsOn = @("[xDSCDomainjoin]JoinDomain")
    SetScript =
    {
        # Get current OS version
        $OsVersion = (Get-WmiObject -class Win32_OperatingSystem).Caption

        # Add KMS client key for server version to variable $Key
        switch -Regex ($OsVersion) {
            'Windows Server 2012 R2 Standard' { $Key = 'D2N9P-3P6X9-2R39C-7RTCD-MDVJX'; break }
            'Windows Server 2016 Standard' { $Key = 'WC2BQ-8NRM3-FDDYY-2BFGV-KHKQY'; break }
            'Windows Server 2012 Server Standard' { $Key = 'XC9B7-NBPP2-83J2H-RHMBY-92BT4'; break }
            'Windows Server 2008 R2 Standard' { $Key = 'YC6KT-GKW9T-YTKYR-T4X34-R7VHC'; break }
        }

        # Gather KMS Service info
        $KmsService = Get-WMIObject -query "select * from SoftwareLicensingService"

        # Set KMS Server
        $null = $KmsService.SetKeyManagementServiceMachine('YourLicenseServer.contoso.com')

        # Install the KMS Client Key
        $null = $KmsService.InstallProductKey($Key)

        # Activate Windows
        $null = $KmsService.RefreshLicenseStatus()
    }

    TestScript =
    {
        function Get-ActivationStatus {
            [CmdletBinding()]
            param(
                [Parameter(ValueFromPipeline = $true, ValueFromPipelineByPropertyName = $true)]
                [string]$DNSHostName = $Env:COMPUTERNAME
            )
            process {
                try {
                    $wpa = Get-WmiObject SoftwareLicensingProduct -ComputerName $DNSHostName `
                        -Filter "ApplicationID = '55c92734-d682-4d71-983e-d6ec3f16059f'" `
                        -Property LicenseStatus -ErrorAction Stop
                }
                catch {
                    $status = New-Object ComponentModel.Win32Exception ($_.Exception.ErrorCode)
                    $wpa = $null
                }
                $out = New-Object psobject -Property @{
                    ComputerName = $DNSHostName;
                    Status       = [string]::Empty;
                }
                if ($wpa) {
                    :outer foreach ($item in $wpa) {
                        switch ($item.LicenseStatus) {
                            0 { $out.Status = "Unlicensed" }
                            1 { $out.Status = "Licensed"; break outer }
                            2 { $out.Status = "Out-Of-Box Grace Period"; break outer }
                            3 { $out.Status = "Out-Of-Tolerance Grace Period"; break outer }
                            4 { $out.Status = "Non-Genuine Grace Period"; break outer }
                            5 { $out.Status = "Notification"; break outer }
                            6 { $out.Status = "Extended Grace"; break outer }
                            default { $out.Status = "Unknown value" }
                        }
                    }
                }
                else { $out.Status = $status.Message }
                $out
            }
        }

        If ((Get-ActivationStatus).Status -eq "Licensed") {
            return $True
        }

        Else {
            return $False
        }
    }

    GetScript =
    {
        function Get-ActivationStatus {
            [CmdletBinding()]
            param(
                [Parameter(ValueFromPipeline = $true, ValueFromPipelineByPropertyName = $true)]
                [string]$DNSHostName = $Env:COMPUTERNAME
            )
            process {
                try {
                    $wpa = Get-WmiObject SoftwareLicensingProduct -ComputerName $DNSHostName `
                        -Filter "ApplicationID = '55c92734-d682-4d71-983e-d6ec3f16059f'" `
                        -Property LicenseStatus -ErrorAction Stop
                }
                catch {
                    $status = New-Object ComponentModel.Win32Exception ($_.Exception.ErrorCode)
                    $wpa = $null
                }
                $out = New-Object psobject -Property @{
                    ComputerName = $DNSHostName;
                    Status       = [string]::Empty;
                }
                if ($wpa) {
                    :outer foreach ($item in $wpa) {
                        switch ($item.LicenseStatus) {
                            0 { $out.Status = "Unlicensed" }
                            1 { $out.Status = "Licensed"; break outer }
                            2 { $out.Status = "Out-Of-Box Grace Period"; break outer }
                            3 { $out.Status = "Out-Of-Tolerance Grace Period"; break outer }
                            4 { $out.Status = "Non-Genuine Grace Period"; break outer }
                            5 { $out.Status = "Notification"; break outer }
                            6 { $out.Status = "Extended Grace"; break outer }
                            default { $out.Status = "Unknown value" }
                        }
                    }
                }
                else { $out.Status = $status.Message }
                $out
            }
        }
        @{ Result = ((Get-ActivationStatus).Status) }
    }
}
```
