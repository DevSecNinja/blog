---
title: 'User Policy not applied with Security Filtering and Loopback Processing'
date: 2015-12-22T17:15:58+00:00
draft: false
tags: ['GPMC', 'Group Policy', 'Loopback Processing', 'Microsoft', 'Security Filtering', 'Windows Server']
description: ""
cover:
  image: ""
  alt: ""
---

Today I created a user policy in an OU where Loopback Processing was applied and where Security Filtering was set to my account to test the policy. The policy didn't show up in the RSOP data (gpresult /h report1.html) and the policy was not getting applied.

**Solution:** Give the Domain Computers (or the group with the computer accounts from the OU) permission to read the GPO. Because of Loopback Processing, the computer account will be used to read the GPO, instead of the user account. You can still give the Domain Computers permission to read the GPO only, and add a user or group to the Security Filtering section to make sure that the GPO will be applied to that group or users. Cheers!
