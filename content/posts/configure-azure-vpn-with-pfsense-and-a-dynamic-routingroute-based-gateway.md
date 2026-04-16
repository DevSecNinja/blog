---
title: 'Configure Azure VPN with PfSense and a Dynamic Routing/Route-based Gateway'
date: 2016-05-22T15:15:53+00:00
draft: false
tags: ['Azure', 'IPSec', 'S2S', 'Site to Site', 'VPN']
description: ""
cover:
  image: ""
  alt: ""
---

In this step-by-step, I'll show you how to configure PfSense with an Azure Site-to-Site VPN by using a Dynamic Routing Gateway/Route-based Gateway. This even works with a VPN **behind a NAT setup**. I was looking for a stable solution that could handle the new Route-based (IKE v2) Gateways. This tutorial is based on the new Azure Portal.

## Prerequisites

- A Hyper-V Host (Windows 10 is fine as well)
- 2 Hyper-V Virtual Networks. One called "External Virtual Network" and one called "Internal Virtual Network".
- A Hyper-V VM with PfSense installed with NAT configured between the internal and external virtual network. Just download the ISO from the [PfSense website](https://pfsense.org/) and create a Generation 1 VM with it. Give it 512 or 1024 MB RAM and 1 vCPU and follow online installation instructions.

## Configuration of your Azure Virtual Network & Gateway

1. Go to [Portal.Azure.com](https://portal.azure.com) and sign in to your Azure environment.
2. Create a Virtual Network and use the default settings. Make sure that the address space is not the same as your internal network.
3. Create a Subnet by opening the virtual network you just created and then click on the **Subnets** button under "General". Create a **Gateway Subnet** by clicking on the "+ Gatway Subnet" button. In this tutorial, I use:
   1. 10.0.0.0/19 address space
   2. VM subnet of 10.0.0.0/20 (10.0.0.0 - 10.0.15.255)
   3. Gateway subnet of 10.0.16.0/29 (10.0.16.0 - 10.0.16.7).
4. Create a Virtual Network gateway. Give it a name, select your Virtual Network and create a new Public IP address. Select **VPN** as gateway type and use the **Route-based** VPN type.
5. Azure will start the deployment of your gateway now. This could take up to an hour, so take a short break. :)
6. After the deployment has been completed, open the Virtual Network Gateway you just created. Click on **Settings** and **Connections**. Click on **Add** to create a connection. Give it a name, choose **Site-to-site (IPsec)** as the connection type, create a new local network with the Public IP address of the PfSense instance and use a strong 'password' as PSK. The Public IP adress could be an IPv4 Address of a router, which is the gateway of the PfSense VPN VM.
7. Open the PfSense Web Portal. Go to the **VPN** button in the top menu and open **IPsec**. Click on "**Add P1**".
8. Use the settings from the Phase 1 table below. Leave other settings as default.
9. You'll see a new entry in the IPsec Tunnels overview. Click on the **Show Phase 2 Entries** button and add a new P2 entry by clicking on the **Add P2** button.
10. Use the settings from the Phase 2 table below.
11. Go to **Status**, **IPsec** from the top menu. There you will see the new VPN connection. Click on **Connect VPN**. Click on F5. You'll see that the status is jumping between **ESTABLISHED** and **CONNECTING** or **ESTABLISHED X seconds** and **ESTABLISHED 0 seconds**. Give it some time here. It can take a couple of minutes to get this working. Check the logging under **Status,** **System Logs** and **IPsec**. Check if the status of the **Connection** in Azure is set to "Connected" as well.
12. (Optional) Don't forget to give your IPsec VM a static MAC Address and IP Address from your router of within the Web Interface.
13. (Optional) Give your PfSense VM a reboot to check if the VPN works after a reboot.
14. Try to RDP to an Azure VM from your Internal Hyper-V network or do a trace from your command line to a VM: **tracert 10.0.0.5**.

 

Phase 1

Name

Setting

Key Exchange Version

 V2

Remote Gateway

Enter public IP of VNet gateway

Pre-Shared Key

Enter the PSK of the connection

Phase 1 Lifetime

10800

 

Phase 2

Name

Setting

Local Network

Choose your LAN network here if you are using NAT

Remote Network

Use the whole Azure subnet. I use 10.0.0.0/19

Description

For example, Subnet-1

Protocol

ESP

Encryption Algorithms

Only select AES / 128 bits

Hash Algorithm

SHA1

PFS Key Group

2 (1024 bit)
