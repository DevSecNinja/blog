---
title: 'My Office 365 based personal, secure & unique email system'
date: 2019-05-19T18:00:00+00:00
draft: false
tags: ['Email', 'Exchange', 'Exchange Online', 'Microsoft', 'Office 365', 'PowerShell', 'Privacy', 'Secure']
description: ""
cover:
  image: ""
  alt: ""
---

**A secure email system is important to protect yourself from the increasing phishing and spam attacks, where hackers try to steal money on a large scale. More and more organizations hosting personal data are getting hacked, where hackers misuse this personal data to launch attacks. In this blog post I will introduce you to a solution I've created based on Office 365 and PowerShell to prevent that my email address is spread more widely on the internet.**

## Requirements

As I always like to start with requirements before building a solution...

1. E-mail addresses/aliases must be revoked when spam or phishing is delivered to the alias. I also want to prevent using aliases like amazon2@domain.com after revoking an alias.
2. Email addresses/aliases must have a unique identifier to make sure that hackers cannot guess the email address for another service. For example, if you use amazon@domain.com a hacker could guess bestbuy@domain.com as well. Also wildcards like John+amazon@domain.com are easy to manipulate with a regex.
3. All email delivered to the email addresses/aliases should be forwarded to one address. I prefer to be able to deliver emails to other addresses as well. For example, if you have an address for your Amazon account, you might want to send emails about delivery to the rest of the family as well.
4. An e-mail address or alias should be active within seconds.
5. The solution must be able to track how much aliases and which aliases are already created.
6. The solution must be easy to use and straightforward. (e.g. prevent the use of a database to keep track of aliases)
7. The e-mail solution must be hosted on a secure email system like Office 365 (preferred) with powerful spam filtering capabilities.
8. The email solution must be fully managed. I don't want to spend time on keeping the system working.

These requirements forced me to look into a solution similar to how an API key works. If you want to have access to an API, you can request an API key which is unique to you. The organization that provides the API key stays in full control of the key. When the API is misused by the user, the organization can revoke the API key preventing further access to the API. But how can we achieve this with a secure e-mail provider preventing you from creating less than 150 aliases?

## Options that crossed my mind

My initial thought was to create aliases for my Office 365 account, but after doing some testing I found two major issues:

- It takes at least 15-20 minutes for an alias to get active and you don't know when it's active. This is really frustrating if you want to register a new e-mail address for a new company or website.
- Office 365 limits the amount of aliases to <400. Depending on which documentation you read, users are telling that there is a limit on 150 or 200 proxy addresses. Other large email providers do this as well.

## Solution

The solution is focused around Distribution Groups in Office 365. To support the solution, I've developed a PowerShell module and made it available on the PowerShell Gallery.

This resulted in the following scenario I'm now actively using.

The solution creates email address in the following format: <Prefix><Random number>@<subdomain>.<domain>.<tld> The **prefix** is used to easily identify email addresses created with this solution.

The **random number** makes it hard for attackers to identify other email addresses in the domain.

The **subdomain** is useful for other _Doe_ family members, so they can also create these aliases if required.

An e-mail address for John Doe for Amazon.com looks like: JD30485@j.doe.com

### Prerequisite

As a prerequisite I've created 100 'claimable' distribution groups which I rename before use. I also installed my PowerShell module on Azure Cloud Shell to make sure I can easily create new email addresses and aliases from any browser or the Azure app. See the last chapter for the module download.

### When I create a new account at a website like Amazon.com

Let's say I want to register an account with Amazon.com.

1. I open the Azure Cloud Shell by browsing to [shell.azure.com/powershell](https://shell.azure.com/powershell).
2. As I already provisioned claimable distribution groups, I can just run the following command: **Select-MailAlias -Verbose -DomainName amazon.com** This command will change the display name of a claimable distribution group to match the domain name.
3. I provide the personalized email address to Amazon. All emails will be forwarded to my primary mail account. _Optionally_, I can also include other family members in the distribution group to make sure they will also receive emails from Amazon.

## Download the module

The module is available on the [PowerShell Gallery](https://www.powershellgallery.com/packages/Office365MailAliases), which can be installed by running the following PowerShell command:

> Install-Module -Name Office365MailAliases

The module contains various cmdlets you can use. Have a look! Want to contribute?

Feel free to open up a Pull Request!

The project is hosted on a [public GitHub repository](https://github.com/DevSecNinja/Office365AliasModule).

This project is integrated with a complete CI/CD pipeline that automatically tests, builds and releases to the PowerShell Gallery!

More on that in a later blog post.

Let me know if this is something you will use too! I really like it for my personal email as I already have 20+ e-mail addresses registered.
