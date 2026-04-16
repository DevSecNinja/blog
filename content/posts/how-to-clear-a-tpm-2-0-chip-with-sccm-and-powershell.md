---
title: 'How to Clear a TPM 2.0 chip with SCCM and PowerShell'
date: 2016-02-14T13:25:33+00:00
draft: false
tags: ['Physical Presence', 'PowerShell', 'SCCM 2012 R2 SP1', 'System Center', 'TPM 2.0', 'Windows', 'Windows 10']
aliases:
    - /2016/02/14/how-to-clear-a-tpm-2-0-chip-with-sccm-and-powershell/
description: ""
cover:
  image: ""
  alt: ""
---

With TPM 1.2, Microsoft was able to clear the TPM during the SCCM Task Sequence without asking for permission to clear the TPM.

With TPM 2.0, SCCM is unable to clear and activate the TPM chip during the deployment.

The first time you boot your computer, you need to provide a BitLocker Recovery Key, or the tpm.msc console will tell you that the TPM is ready for use, with reduced functionality. [I found a script online that I've added to my GitHub](https://github.com/jvravensberg/PowerShell/blob/master/Windows-General/BitLocker/Reset-TPMOwner.ps1) to clear the TPM 2.0 chip during the deployment.

You need to reboot the computer after running this script and it will give a UEFI pop-up during the deployment asking the user for permission to clear the TPM chip. (Physical Presence) I heart from a vendor that Microsoft is working on a workaround to disable the Physical Presence during the deployment.

You could experiment with the "NoPPIclear" TPM setting to disable this physical presence feature next time you deploy a computer.

Your Task Sequence should look like this: - Run the PowerShell script from the URL above - Restart Computer (You will see the Physical Clearance prompt after the reboot) - Enable BitLocker Task
