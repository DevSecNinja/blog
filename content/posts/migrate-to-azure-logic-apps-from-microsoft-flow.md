---
title: 'Migrate to Azure Logic Apps from Microsoft Flow'
date: 2019-04-06T09:00:43+00:00
draft: false
tags: ['Automation', 'Azure', 'Azure Logic Apps', 'Domotica', 'Flow', 'Flows', 'Microsoft', 'Microsoft Flow']
description: ""
cover:
  image: ""
  alt: ""
---

**People who follow me on Twitter might have noticed that I'm working more and more with Microsoft Flow.

Microsoft Flow allows me to create simple automations (like IFTTT) and to create a bridge between services like Office 365 and my home automation with Home Assistant.

Recent changes to the pricing model made me decide to move away from Microsoft Flow, back to Azure Logic Apps.

In this blog post, I'll explain how easy it is to move your flows to Azure Logic Apps.** In my flows I've been a heavy user of the HTTP Trigger and HTTP Request actions, because I'm relying mostly on REST API calls to perform the automation tasks.

Microsoft has suddenly decided that a premium account is needed to use these actions.

As I understand that Microsoft Flow uses compute power in the background and costs money to run, I think Microsoft should have done better by:

- Communicating that these triggers & request will require a premium account in X amount of months. Microsoft suddenly changed this in Microsoft Flow and forced me to migrate my Flows to Azure Logic Apps as quickly as possible to be able to create new flows or edit current flows. I do appreciate that Microsoft kept the already created flows running.
- Allowing a Microsoft account (MSA) to be registered as a premium account by somehow linking it to an Office 365 account. As I was using a Microsoft account and therefore not able to upgrade to a Microsoft Flow premium account, I was basically stuck.

https://twitter.com/DevSecNinja/status/1113068148171964416?s=20

## Migrate your Microsoft Flows to Azure Logic Apps

As Microsoft Flow is using the same back end as Azure Logic Apps, they made it very easy to migrate to Azure Logic Apps. Before you follow this guide, make sure you have an active Azure subscription that you can use for the Azure Logic Apps.

1. Browse to the [Microsoft Flow Portal](http://flow.microsoft.com/). Login with your Microsoft Flow account. On the left-hand side, click on _My Flows_.
2. On a flow that you want to migrate to Azure Logic Apps, click the _More Commands_ button, select _Export_ and click _Logic Apps Template (.json)_. ![More commands menu in Microsoft Flow](/images/2019/04/firefox_2019-04-06_10-19-28.png)
3. This will create a backup of the Microsoft Flow in JSON. Feel free to open up the file with Visual Studio Code or Notepad to see how the flows are structured. If you are in Visual Studio Code, you can make the JSON more human-readable by formatting the document. You can do this by using the SHIFT + ALT + F shortcut. You can also open the Command Palette (CTRL + SHIFT + P) and type Format Document.
4. Browse to the [Azure Portal](https://portal.azure.com) and search for _Deploy a custom template_ in the search bar. ![Search in Azure for Deploy a custom template](/images/2019/04/firefox_2019-04-06_10-23-31.png)
5. This will open up the **Custom deployment** blade. As we already have a JSON template, click on _Build your own template in the editor_. ![Azure Custom Deployment](/images/2019/04/firefox_2019-04-06_10-25-38.png)
6. On the right-hand side of the screen, paste the contents of the JSON file you've downloaded at step 2. This can be the same version as you've downloaded at this step or the formatted document. Click on the _Save_ button to load the template.
7. The next screen allows you to:
   1. Select the **subscription** where the Azure Logic App will be created.
   2. Select the **resource group** of the Azure Logic App.
   3. Select the Azure **region** of the Azure Logic App.
   4. Provide the **name** & **location** of the Azure Logic App. (You can keep the location as \[resourceGroup().location\] to add the Azure Logic App to the same Resource Group as the deployment.
   5. Provide values for additional parameters, like the name of the connectors if your export contains additional connectors like the Outlook connector.
8. Clicking on the _Purchase_ button after you agreed with the terms will start the deployment. In a couple of minutes, your Microsoft Flow flow is now running as an Azure Logic App! ![Azure Custom Deployment](/images/2019/04/firefox_2019-04-06_10-31-46.png)

Make sure to test the Azure Logic App by browsing to the Resource Group you've just created (CloudeniusApp in the example) and trigger the Logic App. If your Logic App is using connectors, you might need to add them to the Azure Logic App. After successful testing the Logic App, you can remove the flow from Microsoft Flows. That's it! You are now using Azure Logic Apps instead of Microsoft Flow!

## Want to learn more about Azure Logic Apps?

Check out the following blog post: [Use Azure Logic Apps and RSS to Create a Simple Post Reminder on Social Media](http://DevSecNinja.com/2019/01/20/use-azure-logic-apps-and-rss-to-create-a-simple-post-reminder-on-social-media/).
