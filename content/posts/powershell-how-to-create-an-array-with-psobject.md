---
title: 'PowerShell - How to Create an Array with PSObject'
date: 2017-06-10T12:00:30+00:00
draft: false
tags: ['Array', 'PoSh', 'PowerShell', 'Report', 'Scripting']
description: ""
cover:
  image: ""
  alt: ""
---

As I told you before in my [previous blog post](http://cloudenius.com/2017/06/04/powershell-using-out-gridview-to-select-a-parameter/), I was asked to build an interactive PowerShell script for creating Virtual Machines in Azure. In this blog post, I want to show you how I've created a report (or array) within PowerShell that:

- Visualize the to-be-created objects to the user
- Allows PowerShell to get the data of that array to create Virtual Machines. This makes sure that you have a consistent view of what PowerShell will create for you. See it as an order overview before you buy something online.

Let's imagine I have all the Virtual Machines that I want to create in $VMs. This can be an import of a CSV, or maybe I've asked the user for details with "Read-Host" or [Out-GridView](http://devsecninja.com/2017/06/04/powershell-using-out-gridview-to-select-a-parameter/).

When you import a CSV, the content will already be organized in an array.

But with this code, you can easily add more content to it and combine both data from a CSV and from the script.

For example, a randomized password or the first available IP address in a subnet in Azure.

My end goal is to have a nice overview of all the needed Virtual Machines in $Report, which I can later use to make those VMs.

With the code below, you will create a PSObject for every VM in the $VMs variable.

After the PSObject has been created, it will append to the $Report variable.

With "$Report = @()" you ask PowerShell to create an empty array.

See it as an empty table that you could later use to add content to it.

After the deployment has succeeded or failed, you can add the status to $VM.DeploymentStatus.

```powershell
# Set report variable
$Report = @()

Foreach ($VM in $VMs) {
  $PSObject = New-Object PSObject -Property @{
    DeploymentName = $VM.resourceGroupName + "-" + (Get-Date -Format "yyyyMMdd-hh-mm-ss")
    VMName = $VM.vmName
    Location = $VM.resourceGroupLocation
    ResourceGroupName = $VM.resourceGroupName
    AdminPassword = $VM.adminPassword
    VMSize = $VM.vmSize
    VirtualNetwork = $VM.virtualNetwork
    VirtualNetworkRG = $VM.virtualNetwork.ResourceGroupName
    SubnetName = $VM.subnetName
    IPAddress = $VM.ipAddress
    OperatingSystem = $VM.operatingSystem
    DeploymentStatus = $Null
  }

  $Report += $PSObject
}

# Show the report
$Report

# Or show it in Table Format
# $Report | Format-Table
```

The above example is by far the easiest way to create a nice array for me. Thanks for reading. Hope you find it useful too.
