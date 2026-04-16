---
title: 'PowerShell Profiles - The profile.ps1 file'
date: 2015-08-30T10:00:52+00:00
draft: false
tags: ['Home Directory', 'Microsoft', 'PowerShell', 'Profile', 'Windows']
aliases:
    - /2015/08/30/powershell-profiles-the-profile-ps1-file/
description: ""
cover:
  image: ""
  alt: ""
---

Welcome to this blog series about PowerShell profiles. I'm using PowerShell profiles for a couple of months now to make life a lot easier.

To start this blog series, I would like to show you my Profile.ps1 file.

It's located in "C:\\Users\\<Your username>\\Documents\\WindowsPowerShell".

Because I use my PowerShell profiles at multiple locations such as my work notebook, home computer and sometimes at projects, I need to make sure that my PowerShell script home is always right so that the rest of the PowerShell profile is able to load successfully.

That's why I have these commands at the beginning of my profile:

```powershell
# Set the Home Directory for Powershell to start in
$ScriptHomeOneDrive = "$Home\OneDrive\Scripts"
$ScriptHomeDocuments = "$Home\Documents\Scripts"
$ScriptHomeMyDocuments = "$Home\My Documents\Scripts"

if ((Test-Path -Path $ScriptHomeOneDrive )) {
    $ENV:ScriptHome = $ScriptHomeOneDrive
}
Elseif ((Test-Path -Path $ScriptHomeDocuments )) {
    $ENV:ScriptHome = $ScriptHomeDocuments
}
Else {
    $ENV:ScriptHome = $ScriptHomeMyDocuments
}

Set-Location $ENV:ScriptHome
```

Because I'm using OneDrive as my script repository, I need to make sure that the script start in my OneDrive\\Scripts directory. When I have access to a computer or server without OneDrive, I need to use the Documents folder as my script home. On some servers, the "Documents" folder is named as "My Documents", so that's why I use that folder too.

```powershell
# Load the base functions
. .\Startup\_PSH_BASE.ps1
```

The above code will load my base file which is located in my OneDrive folder or in my Documents folder.

Now I can use my OneDrive folder to sync all my scripts between multiple computers and make changes to the profile from every device.

Make sure you sign those PowerShell Profile Scripts, so that you know that it's not changed! [In my next post, I'll show the structure of my \_PSH\_BASE.ps1 file and other files that are part of my PowerShell profile.](https://devsecninja.com/2015/08/30/powershell-profiles-the-structure-of-your-_psh_base-ps1-file/)
