---
title: 'PowerShell - Signed scripts "cannot be loaded because running scripts is disabled"'
date: 2017-12-06T18:00:48+00:00
draft: false
tags: ['ExecutionPolicy', 'PowerShell', 'SCCM', 'Script', 'Task Sequence']
description: ""
cover:
  image: ""
  alt: ""
---

So you are signing your PowerShell scripts as a Best Practice from Microsoft. Good job! You've configured the PowerShell Execution Policy as AllSigned and you've created an application in SCCM where you run the signed script as:

> PowerShell.exe -File .\\Script.ps1

The application installs just fine on your machine from the Software Center. During the Task Sequence, the application cannot be installed and in the Event Viewer. You'll find the following error message:

> PowerShell.exe: File <Filename> cannot be loaded because running scripts is disabled on this system. For more information, see about\_execution\_policies at..."

You open up PowerShell to see the current ExecutionPolicy. "Get-ExecutionPolicy -List" shows that all scopes have undefined execution policies. With "Get-Help about\_Execution\_Policies" you find out that Undefined policy is equal to a restricted policy and that "Permits individual commands, but will not run scripts".

## The solution

Go back to your application in SCCM and make sure you set the ExecutionPolicy to AllSigned so it will work both during a Task Sequence and while working in OS.

> PowerShell.exe **\-ExecutionPolicy AllSigned** -File .\\Script.ps1

Cheers!
