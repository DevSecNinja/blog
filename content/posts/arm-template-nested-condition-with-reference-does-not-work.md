---
title: 'ARM Template - Nested condition with reference does not work'
date: 2020-06-10T12:00:00+00:00
draft: false
tags: ['Azure', 'Azure Resource Manager', 'ARM Template', 'Nested Template', 'Condition', 'Static IP address']
description: ""
cover:
  image: ""
  alt: ""
---

Recently I was facing an issue where a reference in a nested Azure Resource Manager template was still being executed, despite the condition being false. I have created an ARM template that first sets a dynamic IP address on the Network Interface and later on converts it to a static IP address. It uses the initially assigned IP address and converts it to static.

# The issue with a reference in a nested template with a condition

In the example below, you see a nested template that converts the dynamic IP address to a static IP address. If the `runTheNestedTemplate` variable is set to true, everything will work fine as the condition is met. If the `runTheNestedTemplate` condition is set to false, it **should** work too, but unfortunately Azure will still try to validate the reference mentioned in the `privateIPAddress` property, resulting in a failing ARM template deployment if NIC01 does not exists.

```json
{
  "apiVersion": "2019-10-01",
  "type": "Microsoft.Resources/deployments",
  "name": "[concat(variables('vmName'), '-UpdateNicToStaticIPAddress')]",
  "condition": "[or(equals(parameters('runTheNestedTemplate'), 'true'))]",
  "dependsOn": [
    "[resourceId('Microsoft.Network/networkInterfaces/', concat(variables('vmName'), '-NIC01'))]"
  ],
  "properties": {
    "mode": "Incremental",
    "parameters": {},
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {},
      "variables": {},
      "resources": [
        {
          "type": "Microsoft.Network/networkInterfaces",
          "name": "[concat(variables('vmName'), '-NIC01')]",
          "apiVersion": "2018-03-01",
          "location": "[parameters('region')]",
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Static",
                  "privateIPAddress": "[reference(concat(variables('vmName'), '-NIC01'), '2020-03-01').ipConfigurations[0].properties.privateIPAddress]",
                  "subnet": {
                    "id": "[concat(variables('vnetRef'),'/subnets/', parameters('vnetSubnetName'))]"
                  }
                }
              }
            ]
          }
        }
      ]
    }
  }
}
```

# Workaround

As a workaround to resolve this issue, you have to wrap the reference in another if statement:

```json
{
  "apiVersion": "2019-10-01",
  "type": "Microsoft.Resources/deployments",
  "name": "[concat(variables('vmName'), '-UpdateNicToStaticIPAddress')]",
  "condition": "[or(equals(parameters('runTheNestedTemplate'), 'true'))]",
  "dependsOn": [
    "[resourceId('Microsoft.Network/networkInterfaces/', concat(variables('vmName'), '-NIC01'))]"
  ],
  "properties": {
    "mode": "Incremental",
    "parameters": {},
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {},
      "variables": {},
      "resources": [
        {
          "type": "Microsoft.Network/networkInterfaces",
          "name": "[concat(variables('vmName'), '-NIC01')]",
          "apiVersion": "2018-03-01",
          "location": "[parameters('region')]",
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Static",
                  "privateIPAddress": "[if(equals(parameters('runTheNestedTemplate'),'true'), reference(concat(variables('vmName'), '-NIC01'), '2020-03-01').ipConfigurations[0].properties.privateIPAddress, 'Empty')]",
                  "subnet": {
                    "id": "[concat(variables('vnetRef'),'/subnets/', parameters('vnetSubnetName'))]"
                  }
                }
              }
            ]
          }
        }
      ]
    }
  }
}
```

I have reported this bug to Microsoft. In the meantime, feel free to use this workaround.
