---
title: 'SCCM - Multicast on client fails with error "Failed to get MCS key (Code 0x80004005)"'
date: 2016-04-15T18:05:21+00:00
draft: false
tags: ['1511', 'Multicast', 'SCCM', 'System Center', 'Troubleshooting', 'Windows', 'Windows 10']
description: ""
cover:
  image: ""
  alt: ""
---

### Problem:

Multicast during an SCCM 2012 R2 SP1 (1511 release) Task Sequence fails with error "Failed to get MCS key (Code 0x80004005)". This error is found in the smsts.log log file on the (Windows 10 Enterprise x64 1511) client machine.

### SMSTS.log file contents

`CLibSMSMessageWinHttpTransport::Send: URL: SCCM01.CORP.DOMAIN.COM:443 CCM_POST /SMS_MCS_AltAuth/.sms_mcs?op=keyinfo ApplyOperatingSystem 15-4-2016 9:02:57 656 (0x0290)` `In SSL, but with no client cert ApplyOperatingSystem 15-4-2016 9:02:57 656 (0x0290)` `Request was successful.

ApplyOperatingSystem 15-4-2016 9:02:57 656 (0x0290)`pNext != NULL, HRESULT=80004005 (e:\nts_sccm_release\sms\framework\osdmessaging\libsmsmessaging.cpp,2054) ApplyOperatingSystem 15-4-2016 9:02:57 656 (0x0290)`reply has no message header marker ApplyOperatingSystem 15-4-2016 9:02:57 656 (0x0290)`DoRequest (sReply, true), HRESULT=80004005 (e:\nts_sccm_release\sms\framework\osdmessaging\libsmsmessaging.cpp,10358) ApplyOperatingSystem 15-4-2016 9:02:57 656 (0x0290)`oMcsRequest.GetMCSKey(mcsKeyInfoResponse), HRESULT=80004005 (e:\nts_sccm_release\sms\server\mcs\consumer\mcsisapiclient.cpp,429) ApplyOperatingSystem 15-4-2016 9:02:57 656 (0x0290)`Failed to get MCS key (Code 0x80004005) ApplyOperatingSystem 15-4-2016 9:02:57 656 (0x0290)`ClientRequestToMCS::DoRequest failed. error = (0x80004005).

ApplyOperatingSystem 15-4-2016 9:02:57 656 (0x0290)``Request to MCS 'SCCM01.CORP.DOMAIN.COM' failed with error (Code 0x80004005).

ApplyOperatingSystem 15-4-2016 9:02:57 656 (0x0290)``Multicast OpenSessionRequest failed (0x80004005).

ApplyOperatingSystem 15-4-2016 9:02:57 656 (0x0290)``Sending status message: SMS_OSDeployment_PackageDownloadMulticastStatusFail ApplyOperatingSystem 15-4-2016 9:02:57 656 (0x0290)`

### Solution

#### Fix 1: could fix your problem but didn't work for me:

1. Uncheck "Allow this package to transfered via multicast" at packages and your install image properties.
2. Remove the "SerializedMCSKey" and "SignedSerializedMCSKey" keys in registry at HKLM\\Software\\SMS\\MCS.
3. Uncheck "Enable multicast" at the properties of the Distribution Point.
4. Wait for 30 to 60 minutes until multicast is fully removed from the Distribution Point. Check this in the SCCM console under the site roles status view and check the log files on the distribution point.
5. Check "Enable multicast" at the properties of the Distribution Point.
6. Check if the "SerializedMCSKey" and "SignedSerializedMCSKey" keys in registry at HKLM\\Software\\SMS\\MCS are populated again. This could take a couple of minutes or a couple of hours. I couldn't find how to force this. If you know a way, let me know in the comments section.
7. Check "Allow this package to transfered via multicast" at packages and your install image properties.
8. Wait again for 15 to 30 minutes until the packages are multicast enabled. A background process runs to do this. Microsoft recommended to wait around 15 to 30 minutes.

#### Fix 2:

Rebuild your distribution point server by removing the server and installing Windows Server again. This was the only thing that fixed it for me after spending a lot of hours with the Microsoft Support. We enabled multicast during the installation of the environment and disabled it a couple of weeks later. After we wanted to enable it again, this problem started to occur. Let me know in the comments section if this blog post has fixed your issue too! Cheers!
