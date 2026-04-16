---
title: 'Windows 10 - Intel HDMI Audio doesn''t work'
date: 2015-07-27T14:00:39+00:00
draft: false
tags: ['Audio', 'HDMI', 'Insider', 'Intel', 'Receiver', 'Windows', 'Windows 10']
description: ""
cover:
  image: ""
  alt: ""
---

After installing Windows 10 on my production device (with a Windows 8.1 Hyper-V VM as back-up, of course), I had an issue with the HDMI Audio of my Dell Latitude E6540 notebook. I found some topics online about setting the default format of the Audio device, such as sample rate and bit depth, but that doesn't work for me. I had to reconfigure my Receiver + 5.1 Audio as "5.1 Surround", instead of the default "Stereo".

You can find this option when you right click the speaker-icon in your taskbar and then click "Sound".

The "Stereo" option worked for me before within Windows 8.1, but with Windows 10, I had to reconfigure this setting.

After Windows Update installed the latest Intel Display Audio driver (6.16.0.3179), I had to configure the "5.1 Surround" again.

Let me know if you had these issues too! [

![Windows 10 - Sound Menu](/images/2015/07/soundmenu.png)](/images/2015/07/soundmenu.png)
