---
title: 'Azure Bastion changes everything!'
date: 2019-06-16T07:00:46+00:00
draft: false
tags: ['Azure', 'Linux', 'RDP', 'RDS', 'Server Management', 'SSH', 'Windows']
description: ""
cover:
  image: ""
  alt: ""
---

**This week Microsoft quietly released some information about a new Azure solution called Azure Bastion.

Azure Bastion acts as a gateway between a Virtual Machine in Azure and your session in the Azure Portal.

This means that without assigning a Public IP address, you are able to connect to your Azure Virtual Machine through the Azure Portal.

No Remote Desktop environment or jumpbox needed.

Azure Bastion is currently in Private Preview.** Microsoft quietly released two YouTube video's.

The first one highlights the Azure Bastion solution in combination with Windows (Server) Virtual Machines over RDP.

{{< youtube eLjuWG-L57Q >}}

In this video, you see someone connecting to a Virtual Machine in Azure.

The Virtual Machine does not have a Public IP address assigned.

After the presenter clicks on the Connect button, the credentials to the Azure Bastion service must be provided.

The Azure Bastion service will now launch a Remote Desktop connection **in the browser** from the Azure Portal.

Looking for Azure Bastion in combination with SSH?

Microsoft also released a [new video on their website](https://azure.microsoft.com/en-us/resources/videos/introduction-to-bastion-ssh/) that shows Azure Bastion in action with SSH.

## Why you should use Azure Bastion when it's available

In a 'traditional' cloud scenario, you don't want to do your management of the VM over the Public IP address.

From a security perspective, it is recommended to use a machine in front of it.

This can be a Remote Desktop Services environment or one or more management VMs.

This is what we call a jumpbox or bastion environment.

As you can imagine, a jumpbox introduces extra costs such as Azure VM costs but also indirect costs such as server management.

Especially if you are leveraging multiple Azure regions and want to incorporate high availability of the jumpboxes.

Additionally you need to maintain a separate access list that defines who is allowed to login to the jumpbox.

As Azure Bastion is a cloud solution, you don't have to pay for the IaaS resources that you consume and Microsoft is managing the solution for you.

The feature is currently in private preview, so no pricing information is available yet.

But I assume Microsoft will follow the pay-per-use model, which mostly is significantly cheaper.

Additionally, I assume that Microsoft will allow this solution to run independently from an Azure region so you don't have to worry about High Availability and failover.

Azure Bastion should also simplify your access management, as all cloud solutions incorporate Azure RBAC which again simplifies the way you can assign access to cloud solutions.

## How Azure Bastion changes how you connect to servers

Microsoft is pushing paswordless scenarios as "76 % of breaches start with compromised passwords" according to Microsoft's Ann Johnson. ([SiliconRepublic.com](https://www.siliconrepublic.com/enterprise/microsoft-ann-johnson-identity-cybersecurity-skills)) Microsoft is internally on a paswordless mission and "have moved 80 % of internal users away from passwords and we are aggressively moving the other 20 %" according to Johnson.

Azure Bastion changes my vision on an optimal Privileged Identity Management strategy.

**User account**: uses Windows Hello biometric authentication to login passwordless.

**Server admin**: uses Azure Bastion to login to Azure VMs by using the local administrator password. This password can be managed by the Local Administrator Password Solution (LAPS) of Microsoft and will be changed every couple of hours. As Microsoft keeps track of everything in the Azure Portal, Audit Logs should provide clarification on who logged in to the machine.

**Domain admin**: uses a Privileged Access Workstation/Virtual Machine to work with Domain Controllers.

**Global admin**: uses Azure AD Privileged Identity Management to request permissions "Just-in-Time".

## It's (seems) fast!

The videos released by Microsoft reveals that it's working **fast**. Of course we have to wait for the public preview to find out in which situations it works fast and when it starts to lag, but it's promising.

## Conclusion

Azure Bastion seems to be a great addition to the Azure features currently available and will change how organizations are providing access to Virtual Machines in Azure.

Azure Bastion can be used for both Windows and Linux workloads as RDP and SSH sessions are supported.

As Azure Bastion is currently in Private Preview, I wasn't able to find any information of this new solution.

As soon there is documentation available from Microsoft, I will update this post. I'm really looking forward to the Public Preview of this feature.

How do you think that Azure Bastion will change the way you access servers on Azure?

Let me know in the comments section.
