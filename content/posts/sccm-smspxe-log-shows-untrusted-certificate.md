---
title: 'SCCM - SMSPXE.log shows Untrusted certificate'
date: 2016-01-21T16:00:47+00:00
draft: false
tags: ['Certificates', 'IIS', 'SCCM', 'System Center']
aliases:
    - /2016/01/21/sccm-smspxe-log-shows-untrusted-certificate/
description: ""
cover:
  image: ""
  alt: ""
---

Recently I found the following error in the SMSPXE.log log file on my newly created distribution point: `CryptVerifySignature failed, 80090006 SMSPXE <REMOVED TIME> 2500 (0x09C4) untrusted certificate: <REMOVED CERTIFICATE> SMSPXE <REMOVED TIME> 2500 (0x09C4) Failed to get information for MP: https://SCCMPRIMARY.DOMAIN.TLD. 80090006. SMSPXE <REMOVED TIME> 2500 (0x09C4)` After recreating my certificate template for the IIS Service on the primary site server, it fixed the problem.

Check the online documentation of SCCM for the details of this certificate template.
