---
title: 'Azure - Automatically deploy a VM in Azure (Runbook)'
date: 2015-02-18T19:00:06+00:00
draft: false
tags: ['Automation', 'Azure', 'Deployment', 'PowerShell', 'Runbook', 'VM']
description: ""
cover:
  image: ""
  alt: ""
---

I was looking for a way to automatically deploy a VM in Azure. The solution was quite simple: Azure Automation. I found [the blog post of DexterPOSH](http://www.dexterposh.com/2014/10/azure-automation-deploy-domain-join-vm.html "Deploy a Windows 10 VM (Server Tech Preview) & domain join") very useful, but the script doesn't work for me. Follow the steps on his blog and use this script below. I'll update this post if I find some improvements.

To-Do list:

- Custom static IP as variable.
- Custom domain as variable.

```powershell
workflow Deploy-NonJoined-VM {
    param(
        [parameter(Mandatory)]
        [String]
        $VMName,

        [parameter(Mandatory)]
        [String]
        $ServiceName = "contoso<Insert name>",

        [parameter(Mandatory)]
        [String]
        $InstanceSize = "Small",

        [parameter(Mandatory)]
        [String]
        $VMImageName = "Specify custom or default image name",

        [parameter(Mandatory)]
        [String]
        $AzureSubscriptionName = "Subscription-1",

        [parameter(Mandatory)]
        [String]
        $StorageAccountName = "contoso",

        [parameter(Mandatory)]
        [String]
        $VMSubnetName = "subnet-1",

        [parameter(Mandatory)]
        [String]
        $VMVnetName = "CORP.contoso.com",

        [parameter(Mandatory)]
        [String]
        $VMAffinityGroup = "West-Europe"
    )
    $verbosepreference = 'continue'

    #Change this to your needs
    $DomainJoinAccount = "Domain Join Account"
    $LocalAccount = "LocalAdmin"
    $AutomationAccount = "Azure Automation Account"

    #Get the Credentials to authenticate agains Azure
    Write-Verbose -Message "Getting the Credentials"
    $Cred = Get-AutomationPSCredential -Name $AutomationAccount
    $LocalCred = Get-AutomationPSCredential -Name $LocalAccount
    $DomainCred = Get-AutomationPSCredential -Name $DomainJoinAccount

    #Add the Account to the Workflow
    Write-Verbose -Message "Adding the Azure Automation Account to Authenticate"
    Add-AzureAccount -Credential $Cred

    #select the Subscription
    Write-Verbose -Message "Selecting the $AzureSubscriptionName Subscription"
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    #Set the Storage for the Subscrption
    Write-Verbose -Message "Setting the Storage Account for the Subscription"
    Set-AzureSubscription -SubscriptionName $AzureSubscriptionName -CurrentStorageAccountName $StorageAccountName

    #Select the most recent Server 2012 R2 Image
    Write-Verbose -Message  "Getting the Image details"
    $imagename = Get-AzureVMImage |
    where-object -filterscript { $_.ImageName -eq $VMImageName } |
    Sort-Object -Descending -Property PublishedDate |
    Select-Object -First 1 |
    select -ExpandProperty ImageName

    #use the above Image selected to build a new VM and wait for it to Boot
    $Username = $LocalCred.UserName
    $Password = $LocalCred.GetNetworkCredential().Password
    New-AzureQuickVM -Windows -ServiceName $ServiceName -Name $VMName -ImageName $imagename -Password $Password -AdminUsername $Username -SubnetNames $VMSubnetName -VNetName $VMVnetName -InstanceSize $InstanceSize -AffinityGroup $VMAffinityGroup -WaitForBoot
    Write-Verbose -Message "The VM is created and booted up now.. Deployment done."

} #Workflow end
```
