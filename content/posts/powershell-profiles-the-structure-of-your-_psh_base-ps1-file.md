---
title: 'PowerShell Profiles - The structure of your _PSH_BASE.ps1 file'
date: 2015-08-30T12:00:18+00:00
draft: false
tags: ['Console', 'ISE', 'Microsoft', 'PowerShell', 'PowerShell Profiles', 'Windows PowerShell']
aliases:
    - /2015/08/30/powershell-profiles-the-structure-of-your-_psh_base-ps1-file/
description: ""
cover:
  image: ""
  alt: ""
---

In my previous post [PowerShell Profiles - The profile.ps1 file](https://devsecninja.com/2015/08/30/powershell-profiles-the-profile-ps1-file/) I showed you my profile.ps1 file.

In this post, I'll show you a way to structure your base file, so that you can use it for your functions and aliases.

Make sure that you always use max 2 files.

The first file is your profile.ps1 file and the other file is this \_PSH\_BASE.ps1 file.

If you use like 3 or 4 files, it can take a couple of seconds to load your PowerShell session.

Start with the header:

```powershell
#########################################################################################
# File Name is: _PSH_BASE.ps1
#########################################################################################
# Powershell Profile Base - Updated:30/08/2015 @ 14:00
#########################################################################################
```

It contains some basic stuff, but it's not necessary.

```powershell
# Set the Home Directory for Powershell to start in
Set-Location $env:ScriptHome
```

This part will start your PowerShell session in your script home. More information about this environment variable in my previous blog post.

```powershell
## Profile Functions ###################################
#region Functions
# PLACE FUNCTIONS HERE
#endregion
```

Because I have a lot of functions in my PowerShell Profile, it's great to use a region so that you can hide your code with the + sign in PowerShell ISE like this: [![PowerShell Regions](/images/2015/08/psregions.png)](/images/2015/08/psregions.png)

```powershell
## Profile Aliases ###################################
Set-Alias -Name list -Value dir/w | Out-Null
```

This is the place where you can define your profile aliases. For example, if you type "list" in the console, it will do the "dir/w" command in the background.

```powershell
## Only PowerShell ISE ###################################
if ($host.name -eq 'Windows PowerShell ISE Host')
{
    Enable-ScriptBrowser
}
```

I've downloaded the [ScriptBrowser plugin for ISE](http://blogs.technet.com/b/poshchap/archive/2014/05/02/powershell-ise-script-browser-add-on.aspx) and I want it to run only in the PowerShell ISE console. Here you can place functions or commands that should only run in PowerShell ISE. Use "ConsoleHost" instead of "Windows PowerShell ISE Host" to define commands and functions to run only in the console.

```powershell
## Only PowerShell Console ###################################
if ($host.name -eq 'ConsoleHost')
{
    $a = (Get-Host).PrivateData
    $a.ErrorForegroundColor = "RED"
    $a.ErrorBackgroundColor = "WHITE"
    $a.WarningForegroundColor = "YELLOW"
    $a.WarningBackgroundColor = "BLACK"
    $a.DebugForegroundColor = "YELLOW"
    $a.DebugBackgroundColor = "BLACK"
    $a.VerboseForegroundColor = "YELLOW"
    $a.VerboseBackgroundColor = "BLACK"
    $a.ProgressForegroundColor = "YELLOW"
    $a.ProgressBackgroundColor = "DARKBLUE"

    $Shell = $Host.UI.RawUI
     $size = $Shell.BufferSize
     $size.width=150
     $size.height=500
     $Shell.BufferSize = $size
     $size = $Shell.WindowSize
     $size.width=150
     $size.height=50
     $Shell.WindowSize = $size
}
```

I use the above code to change the error colors in the PowerShell Console. This doesn't work in PowerShell ISE, that's why I used the if ($host.name) command.

```powershell
# Let the user know your done
$ConsoleType = $Host.Name
Write-Host -ForegroundColor "Green" "Base profile for $ConsoleType loaded."
```

Last but not least, let the user know that the Base profile is loaded for the ISE or Console. In the next blog post, I'll show you some great functions I use with my PowerShell Profile. Cheers!
