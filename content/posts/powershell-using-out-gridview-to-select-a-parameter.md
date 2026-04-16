---
title: 'PowerShell - Using Out-GridView to Select a Parameter'
date: 2017-06-04T09:30:38+00:00
draft: false
tags: ['Azure', 'PowerShell']
description: ""
cover:
  image: ""
  alt: ""
---

Last week I was asked to build an interactive PowerShell script for creating Virtual Machines in Azure. In this blog post, I want to share an easy way to prompt a user for a selection.

```powershell
# Select Azure subscription
$AzureSubscription = (Get-AzureRmSubscription | Out-GridView -Title "Choose your Azure subscription and click OK." -PassThru)

Write-Output "Switching to Azure subscription: $($AzureSubscription.Name)"

$AzureSubscriptionInfo = Select-AzureRmSubscription -SubscriptionId $AzureSubscription.Id
```

This uses Out-GridView to display the contents of the "Get-AzureRmSubscription" Cmdlet and asks the user to make a selection. The user is able to sort and filter the contents within the grid and the user will be informed of the decision by using "Write-Output".

![Out-GridView](/images/2017/06/out-gridview.png) Let's say it's not the most elegant way to ask a user to select a value because it's a pop-up and because of the small "OK" and "Cancel" buttons, but this PowerShell script was developed for IT Administrators. The benefit is that it's easy to use with out-of-the-box code, instead of using custom modules. That's it for now, hope you find it useful. Cheers!
