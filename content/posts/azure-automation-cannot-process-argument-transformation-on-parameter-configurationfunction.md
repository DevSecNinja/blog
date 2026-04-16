---
title: 'Azure Automation - Cannot process argument transformation on parameter ''ConfigurationFunction'''
date: 2016-07-24T09:00:32+00:00
draft: false
tags: ['Azure', 'Azure Automation', 'PowerShell DSC']
description: ""
cover:
  image: ""
  alt: ""
---

Today I was working on an Azure project where the deployment of Azure resources needed to be automated.

## Problem

You'll see the following error message: `ERROR: New-AzureRmResourceGroupDeployment : 7:27:39 AM - Resource Microsoft.Compute/virtualMachines/extensions` `'test01/dscExtension' failed with message '{` `"status": "Failed",` `"error": {` `"code": "ResourceDeploymentFailure",` `"message": "The resource operation completed with terminal provisioning state 'Failed'.",` `"details": [` `{` `"code": "VMExtensionProvisioningError",` `"message": "VM has reported a failure when processing extension 'dscExtension'.

Error message: \"The DSC``Extension failed to execute: **Cannot process argument transformation on parameter 'ConfigurationFunction'**.

Cannot`convert value to type System.String..\r\nMore information about the failure can be found in the logs located under`'C:\\WindowsAzure\\Logs\\Plugins\\Microsoft.Powershell.DSC\\2.19.0.0' on the VM.\"."`}`]`}`}'`

## Solution

This issue probably occurs when the ZIP file with the DSC config cannot be found. When you use a program like 7-Zip to zip your PowerShell script, it will create a ZIP file named Yourfile.zip instead of Yourfile.**ps1**.zip. All of the scripts I've found in the Quickstart Repository need a .ps1.zip extension. So don't forget to check if your file with script has a .ps1.zip extension.
