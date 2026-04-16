---
title: 'Use PowerShell in Azure Functions [Preview]'
date: 2019-05-14T18:30:18+00:00
draft: false
tags: ['Azure', 'Azure Functions', 'Azure Logic Apps', 'Domotica', 'Microsoft', 'PowerShell']
description: ""
cover:
  image: ""
  alt: ""
---

**Microsoft [recently announced](https://devblogs.microsoft.com/powershell/public-preview-of-powershell-in-azure-functions-2-x/) the Public Preview of the ability to run PowerShell code in an Azure Function.

This means that the PowerShell code will run in a Platform-as-a-Service solution, completely serverless!

You pay only for the time that you use the solution and you don't have to manage the underlying infrastructure!

In this blog post, I will show a practical example of how to use an Azure Function in combination with an Azure Logic App.** After publishing a blog post, I always want to share the post as quickly as possible on Twitter & LinkedIn.

This happens automatically by using Twitter on WordPress, and after a day it gets tweeted again by [my Azure Logic App solution I created earlier](http://DevSecNinja.com/2019/01/20/use-azure-logic-apps-and-rss-to-create-a-simple-post-reminder-on-social-media/).

But this means a blog post is only mentioned two times on Twitter.

## Objective

To make sure that my blog posts are getting some more attention, I wanted to randomly publish a blog post once a week.

## Azure Logic App

As I like to keep things simple and as I do most of my automation in Azure Logic Apps, I started off with a blank Logic App to gather the RSS feed.

![msedge_2019-05-12_11-53-25](/images/2019/05/msedge_2019-05-12_11-53-25.png) Unfortunately, I quickly found out that's it's not that easy to get a random item from an array. So why not combine the power of Azure Logic Apps with the new and in preview version of PowerShell in Azure Functions?

## PowerShell in Azure Functions

After creating the Azure Function and selecting PowerShell, you start off by creating an HTTP Trigger function:

![msedge_2019-05-14_19-47-01](/images/2019/05/msedge_2019-05-14_19-47-01.png) This allows you to trigger the PowerShell Function by using an HTTP request. Opening the trigger shows you the function menu on the left, a PowerShell editor in the middle, a log/console window on the bottom and a test view on the right.

![14-05-2019_20-23-55--1L3l0H8i8c6r636i5w--3130x1540](/images/2019/05/14-05-2019_20-23-55-1l3l0h8i8c6r636i5w-3130x1540.png) I'm surprised to see how fast I was able to run a script in this new environment.

It works quickly as your script will run in about 5 seconds.

That is amazingly fast when compared to Azure Automation runbooks.

It feels like you have a shell open on your local machine with a little bit delay. I also like both the console and the output field to be able to see what the output will be if you call the HTTP trigger. I'm using the following PowerShell script in the Azure Function trigger:

```powershell
using namespace System.Net

# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)

# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."

# Get the feed
[xml]$Content = Invoke-WebRequest -Uri 'https://cloudenius.com/feed/'

$Object = ForEach ($msg in ($Content.rss.channel.Item | Get-Random)){
    [PSCustomObject]@{
        'Title' = $msg.title
        'pubDate' = [datetime]$msg.pubdate
        'Link' = $msg.link
    }
}

# Convert the object to JSON
$Body = $Object | ConvertTo-Json

# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
    StatusCode = [HttpStatusCode]::OK
    Body = $Body
})
```

## Using the data from the Azure Function in an Azure Logic App

Now that we have the data of the random blog post in the Azure Function, we can use it in the Azure Logic App to post the content on Twitter: ![msedge_2019-05-14_20-11-55](/images/2019/05/msedge_2019-05-14_20-11-55.png) You can use the following JSON schema to validate the content that comes from the Azure Function:

```json
{
    "properties": {
        "Link": {
            "type": "string"
        },
        "Title": {
            "type": "string"
        },
        "pubDate": {
            "type": "string"
        }
    },
    "type": "object"
}
```

## End result

Last weekend I've been working on this solution and on Monday I was happy to see that it worked, as you can see below: https://twitter.com/DevSecNinja/status/1127836495581200384?s=20 Cheers!
