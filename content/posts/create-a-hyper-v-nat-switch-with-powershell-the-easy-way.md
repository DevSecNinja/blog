---
title: 'Create a Hyper-V NAT Switch with PowerShell - the easy way'
date: 2017-09-24T12:00:54+00:00
draft: false
tags: ['Hyper-V', 'NAT', 'PowerShell', 'Virtual Switch', 'VNET']
description: ""
cover:
  image: ""
  alt: ""
---

You can follow the [original guide by Microsoft](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/user-guide/setup-nat-network) and manually edit all the details, or just use the variables from the script below and let PowerShell do the work for you.

```powershell
# Variables
$InternalSwitchName = "Internal Virtual Switch"
$NATGatewayPrefixLength = "24"
$NATGatewayNetwork = "192.168.0.0/$NATGatewayPrefixLength"
$NATGatewayIP = "192.168.0.1"
$NATNetworkName = "NAT Network"

# Create the VM Switch and NAT Gateway
New-VMSwitch -SwitchName $InternalSwitchName -SwitchType Internal
New-NetIPAddress -IPAddress $NATGatewayIP -PrefixLength $NATGatewayPrefixLength -InterfaceIndex (Get-NetAdapter -Name $("vEthernet ($InternalSwitchName)")).InterfaceIndex
New-NetNat -Name $NATNetworkName -InternalIPInterfaceAddressPrefix $NATGatewayNetwork
```
