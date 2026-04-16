---
title: 'Azure DevOps CI/CD Pipeline, PowerShell & PSScriptAnalyzer'
date: 2019-05-20T05:30:41+00:00
draft: false
tags: ['Azure DevOps', 'CI/CD', 'Git', 'PowerShell', 'PSScriptAnalyzer']
description: ""
cover:
  image: ""
  alt: ""
---

**In my [last blog post](http://DevSecNinja.com/2019/05/19/my-office-365-based-personal-secure-unique-email-system/), I introduced you to the solution I'm using on Office 365 to create personal e-mail addresses.

This solution is hosted on Azure DevOps and is automatically released to the PowerShell Gallery.

In this blog post, I will explain briefly how this works.** The [Azure DevOps project is hosted in a public repository](https://dev.azure.com/DevSecNinja/Office%20365%20Alias%20Module/).

This was introduced recently and enables other users of the module to contribute to the project. I started with an empty repository and created a new branch to upload the PowerShell module & manifest file to the repository.

## Build

Who doesn't like a neat PowerShell script? I do! So I always want to make sure that my scripts comply with the rules defined in the [PSScriptAnalyzer code checker](https://github.com/PowerShell/PSScriptAnalyzer).

The module must pass these rules before it gets uploaded to the [PowerShell Gallery](https://www.powershellgallery.com/packages/Office365MailAliases). I was able to do this by using an [Azure DevOps Build Pipeline](https://dev.azure.com/DevSecNinja/Office%20365%20Alias%20Module/_build/results?buildId=88).

The link redirects you to a successful build that shows you how this works. (Also notice how it grabs the Build ID and uses it as a release version of the module in the [PowerShell Gallery](https://www.powershellgallery.com/packages/Office365MailAliases)!)

## Release

After a successful build, it's time for the release to production! (OK, I might soon add a step or two before releasing to production. 😂) The release grabs the build artifact which contains the module and the manifest, and uploads it to the [PowerShell Gallery](https://www.powershellgallery.com/packages/Office365MailAliases).

## The result

A fully operational CI/CD pipeline that automatically builds, checks the code and releases it to the PowerShell Gallery! Great stuff! ✌
