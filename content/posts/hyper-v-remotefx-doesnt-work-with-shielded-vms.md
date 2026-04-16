---
title: 'Hyper-V RemoteFX doesn''t work with Shielded VMs'
date: 2017-05-21T05:30:44+00:00
draft: false
tags: ['Hyper-V', 'RemoteFX', 'Windows']
description: ""
cover:
  image: ""
  alt: ""
---

## Cause

Recently I replaced my workstation and that was a perfect time to rebuild my home lab.

After I got green lights from my employer to install the all new Windows 10 Creators Update, I also installed Hyper-V and started to build servers in my lab. I was playing around with Shielding, Virtual TPM and SecureBoot until I found out that RemoteFX didn't work anymore. I added the RemoteFX adapter to a VM with shielding enabled, but saw in the Hyper-V Settings menu that "0 virtual machines are currently using this GPU". I first thought about updating my drivers, but I realized that I was playing around with some new features.

After disabling Shielding for this VM, RemoteFX started to work!

## Solution

When RemoteFX doesn't work, check if VM Shielding has been enabled. Disable VM Shielding and test your connection again with RDP.

[![](/images/2017/05/hyperv-physicalgpu.png)](/images/2017/05/hyperv-physicalgpu.png)

_0 virtual machines are currently using this GPU_
