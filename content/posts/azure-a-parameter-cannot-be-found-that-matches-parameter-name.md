---
title: 'Azure - A parameter cannot be found that matches parameter name'
date: 2016-12-14T11:30:29+00:00
draft: false
tags: ['Azure', 'AzureRM', 'JSON', 'PowerShell', 'Templates']
description: ""
cover:
  image: ""
  alt: ""
---

Some error outputs are not always useful. Especially when they make no sense for the issue you have. **Error message:** New-AzureRmResourceGroupDeployment : A parameter cannot be found that matches parameter name 'YOURPARAMETER' **Solution:** This error occurs because of at least the 2 following issues:

- You didn't specify a parameter for 'YOURPARAMETER' in your JSON template. That's what the error says. If you forget to specify a parameter with the New-AzureRmResourceGroupDeployment cmdlet, you'll see a prompt to insert a value for that parameter. But if you add a paremeter like -Name "VM01" to the command while it's not specified in the JSON template, you'll see this error.
- The JSON code you provided isn't valid. Always validate your JSON code. You can use http://www.jsoneditoronline.org/, paste your code and look for the red "X" buttons after a line number.

Did you find another issue where this error occurs? Please let me know in the comments section. Cheers!
