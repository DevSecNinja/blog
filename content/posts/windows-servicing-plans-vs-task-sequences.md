---
title: 'Windows Servicing Plans vs Task Sequences'
date: 2018-08-04T04:30:19+00:00
draft: false
tags: ['ConfigMgr', 'Configuration Manager', 'SCCM', 'System Center', 'Task Sequence', 'Windows', 'Windows Servicing']
description: ""
cover:
  image: ""
  alt: ""
---

On Twitter I asked the following to David James (Director of Engineering, ConfigMgr, Microsoft) and Johan Arwidmark (CTO @ TrueSec): https://twitter.com/DevSecNinja/status/1024927840138145793 For example, I have 3 device collections in SCCM that I call: "Windows 10 Feature Updates - Test" "Windows 10 Feature Updates - Pre-Production" "Windows 10 Feature Updates - Production" With ADRs, that's quite simple.

Just add the deployment to the Software Update Group in SCCM and you're done.

But I was wondering if that is supported in the Servicing Plan scenario too, as with a Servicing Plan you define the amount of days it will take after a build release, before SCCM will deploy the feature update to the collection.

## Option 1: Multiple Servicing Plans, one Software Update Group (Automated)

Rob York (Program Manager for Configuration Manager at Microsoft) joined the discussion and he pointed out that you can create multiple Servicing Plans and select an existing update package. Once the update package has been downloaded, it will not be re-downloaded. Proof is in the image below. https://twitter.com/robdotyork/status/1025049053699235840

## Option 2: One Servicing Plan, multiple deployments (Manual)

Chris Roberts pointed out that you can also use the console to quickly deploy the Servicing Plan to a new collection. Using this method, you have more control over the timing when a feature update gets pushed to a new device collection. https://twitter.com/young\_robbo/status/1025084944291385345?s=21

## That escalated quickly...

If you open the first tweet of this blog post, you see we had some interesting discussions about when to use a Servicing Plan and a Task Sequence.

Johan is not a big fan of the Servicing Plan model: https://twitter.com/jarwidmark/status/1025078067981688836 While David James explains what we will see with 1810: https://twitter.com/djammmer/status/1025137270934757376 Nick Wiley has a valid point here: https://twitter.com/npwiley/status/1025167790980980738?s=21 There are some more great tweets in there!

## Conclusion

According to me, Windows Servicing gives the best user experience, is easy/quick to setup and is the next step towards Windows as a Service. If you need perform various tasks before or directly after the upgrade, Task Sequences are still required. Let me know what you prefer: Task Sequences or Windows Servicing in the comments section. Cheers!
