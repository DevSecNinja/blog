---
title: 'Exchange 2013 - Service FMS failed to reach status ''Running'' on this server.'
date: 2014-01-05T09:51:46+00:00
draft: false
tags: ['Exchange', 'installation', 'Windows Server 2012']
aliases:
    - /2014/01/05/exchange-2013-service-fms-failed-to-reach-status-running-on-this-server-/
description: ""
cover:
  image: ""
  alt: ""
---

When I was installing Exchange 2013 in my home lab, I received an error message on 98 %. You will see the screen below for 15-20 minutes. [

![Exchange-2013-Service-FMS-failed-to-reach-status-Running-error-702x576](https://cloudenius.com/images/2014/12/exchange-2013-service-fms-failed-to-reach-status-running-error-702x576.jpg)](https://cloudenius.com/images/2014/12/exchange-2013-service-fms-failed-to-reach-status-running-error-702x576.jpg) After a moment your installation ends up in an error:

**Error:** **The following error was generated when "$error.Clear();** **if ($RoleStartTransportService)** **{** **start-SetupService -ServiceName FMS** **}** **" was run: "Service 'FMS' failed to reach status 'Running' on this server.".**

When I was searching on Google I found some topics who say that FMS stands for Filtering Management Service. Some people say it's because you've enabled IPv6 or it's about your write permissions on the harddisk. I tried a couple of things without luck. Because I'm using the Exchange server is running in my home lab, I don't need to install the malware protection.

## The solution

Everytime I started the installation, Exchange restarts the incomplete installation. You first need to uninstall the incomplete installation from your machine. Go to "Programs and Features" and delete Exchange from there. Then restart your machine and try install Exchange again but **untick** the box which installs the malware protection. (Of course, only recommended in a testing environment.)
