---
title: 'Use Azure Logic Apps and RSS to Create a Simple Post Reminder on Social Media'
date: 2019-01-20T13:00:08+00:00
draft: false
tags: ['Automation', 'Azure', 'How-to', 'Logic Apps', 'LogicApps', 'Microsoft', 'RSS', 'Step-by-Step', 'Tutorial']
description: ""
cover:
  image: ""
  alt: ""
---

**In this blog post, I will show you how to create an RSS** **Feed/WordPress Post Reminder with Azure Logic Apps, which you can use to post to various Social Media platforms like Twitter or Facebook.** If you've been following me on Twitter, you've probable seen a post like this with a reminder to check out my yesterday's blog post: https://twitter.com/DevSecNinja/status/1084815812232388613?s=20 This is all works automatically by using Azure and Azure Logic Apps.

Azure Logic Apps is just pulling the RSS Feed of my blog, waiting for 24 hours and publishing a tweet on Twitter.

It's really easy to set up as most blog sites and Content Management Systems (CMS) have a built-in RSS-feed.

Let me show you how to set this up.

## Requirements

- **An Azure Subscription**
  - I'm using a Visual Studio Enterprise license, but a trial or Pay-As-You-Go Subscription will do just fine.
  - Based on the cost history, this Azure Logic App construction seems to cost around € 0,00 and € 0,08.
- **An RSS Feed from a site like WordPress**
  - To get the URL to your RSS feed, try yourdomain.com/feed or feed.xml. My WordPress.com blog is hosting an RSS feed on https://DevSecNinja.com/feed/.
- **A Social Media account like Twitter**
  - You need to setup a connection between Azure Logic Apps and Twitter. Just follow the instructions in the blog post to get you started.

## Quick Start Tutorial

1. Login on the [Azure Portal](https://portal.azure.com).
2. Click on _Create a resource_ and search the Marketplace for _Logic App._ Click on _Logic App_. A new blade will open. Click the _Create_ button.
3. Specify:
   1. **Name** - e.g. RSSFeedPostReminder or WordPressPostReminder
   2. **Subscription** - select your Azure subscription
   3. **Resource Group** - create a new one called "LogicApps" or use an existing.
   4. **Location** - specify the region near you. E.g. West Europe
   5. Keep the Log Analytics switch to Off
4. Click _Create_. The Logic App will be provisioned for you which can take a couple of minutes.
5. Click on the bell icon to see the status of the deployment in the Notifications section: ![azure-notifications](/images/2019/01/azure-notifications-1.png)
6. When the Logic App has been provisioned successfully, click on it. This will open the Logic App.
7. Click the _Edit_ button. This will open the Logic Apps Designer. ![azure-logicapp-edit](/images/2019/01/azure-logicapp-edit-e1547987492675.png)
8. You can now add new steps to your Logic App. In my case, I have the following steps defined:
   1. "When a feed item is published" - When a new post is available on my blog
   2. "Delay" - Wait for 1 day
   3. "Post a tweet" - Post a tweet on Twitter and use the featured image of my blog post.
9. This should look something like this: ![Azure-LogicApp-Designer.PNG](/images/2019/01/azure-logicapp-designer-1.png)
10. Be creative! Think about also posting to Facebook or Microsoft Teams. Or maybe you want to send your blog posts to newsletter subscribers. It's all possible.

## Enhance your Azure Logic Apps skills?

Check out the [Azure Logic Apps website](https://azure.microsoft.com/en-us/services/logic-apps/) and [documentation on Microsoft Docs](https://docs.microsoft.com/en-us/azure/logic-apps/). Thanks for reading my blog post. I hope that this post helped you by creating a new Logic App. Let me know if you have other cool steps to share! ![logic apps_color](/images/2019/01/logic-apps_color.png)
