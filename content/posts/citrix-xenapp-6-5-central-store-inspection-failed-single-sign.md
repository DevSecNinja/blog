---
title: 'Citrix XenApp 6.5: the central store inspection failed (Single Sign-On)'
date: 2014-08-09T08:14:02+00:00
draft: false
tags: ['AppCenter', 'Citrix', 'Discovery', 'XenApp']
aliases:
    - /2014/08/09/citrix-xenapp-6-5-the-central-store-inspection-failed-single-sign-on/
description: ""
cover:
  image: ""
  alt: ""
---

I was training for my Citrix XenApp 6.5 certification. When I was running the "Configure and discovery" wizard in the Citrix XenApp application, I received the error below.

I presume that SSO is already installed. Make sure you login as a Domain Admin on your domain controller. (Very important)

[![30-07-2014_07-41-47-8I9X5S9G8Q972P6r60-1025x695](https://cloudenius.com/images/2014/12/30-07-2014_07-41-47-8i9x5s9g8q972p6r60-1025x695.png)](https://cloudenius.com/images/2014/12/30-07-2014_07-41-47-8i9x5s9g8q972p6r60-1025x695.png)

Cancel the wizard and start the XenApp 6.5 CD on your domain controller. Browse to Manually install components -> Server Components -> Additional Features -> Single Sign-On -> Central Store -> Active Directory \-> Step 1: Extend Active Directory. After completing the first step, run Step 2: Create Central Store

Close and reopen the Citrix AppCenter on your XenApp server and try the discovery again.

Good luck!
