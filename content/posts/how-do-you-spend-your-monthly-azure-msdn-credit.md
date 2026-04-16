---
title: 'How do you spend your monthly Azure MSDN credit?'
date: 2016-03-13T14:00:57+00:00
draft: false
tags: ['Azure', 'Azure Credits', 'MSDN', 'Subscription']
description: ""
cover:
  image: ""
  alt: ""
---

If you have an MSDN or Visual Studio subscription, you'll automatically [get Azure credits](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/).

Because I need to test System Center - Configuration Manager/Virtual Machine Manager/Operations Manager for my work, I have an Visual Studio Enterprise with MSDN subscription.

That gives me $150 credit on Azure automatically and makes it very easy to create a (big) home lab for dev/test or study purposes.

You can do a lot with 150 euro in Azure, if you turn your virtual machines off when you don't use them. I have a PowerShell script that runs at the end of the day to shutdown all my running virtual machines.

That saves me a lot of Azure credits.

My lab contains the following virtual machines:

- Windows 10 Test Machine - for testing new Windows 10 Builds
- Windows Server Containers - for testing the new Windows Server Container features
- Domain Controller - with Server 2012 R2
- Data Protection Manager - to demo the functionalities of DPM
- DSC Machines - for testing PowerShell DSC
- RDS - to show how easy it is to deploy an RDS farm
- Root CA - always turned off and is used when my Root CA has expired
- SCCM Server - to test the new SCCM Builds
- SCOM Server - to test SCOM management packs
- SQL Server - to host the System Center databases. (You can't host the SCCM or SCOM database on an Azure SQL database at the moment.)

Do you have an MSDN subscription? You can start testing, developing and training in [Azure right now](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/). Let me know how you spend your Azure credits in the comment section!
