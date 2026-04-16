---
title: 'SCCM - PXE stopped working after configuring Update Server in VMM'
date: 2016-01-21T16:30:31+00:00
draft: false
tags: ['Certificates', 'PXE', 'SCCM', 'System Center']
description: ""
cover:
  image: ""
  alt: ""
---

Recently I connected System Center - Virtual Machine Manager with WSUS. The WSUS server is installed on the primary site server of my SCCM 2012 R2 SP1 CU2 installation.

After I configured my SCCM WSUS server as an update server for VMM, the distribution point in the office stopped working.

You will see HTTP ERROR "12030" in your logs and the PXE request on a client will fail.

Browsing to the website of the SCCM Primary Site server will fail too. I found out that the certificate of IIS on my primary site was gone.

There was no certificate selected for the Default Website.

After adding the certificate again and restarting IIS, PXE started to work again.
