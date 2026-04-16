---
title: 'Spotify - No sound after pausing in Windows 10'
date: 2016-01-02T15:30:47+00:00
draft: false
tags: ['Exclusive Mode', 'HDMI', 'Intel', 'Spotify', 'Windows', 'Windows 10']
description: ""
cover:
  image: ""
  alt: ""
---

I had a problem with Spotify on my notebook, connected with HDMI to my Pioneer receiver. I'm using Windows 10 with the 10586 Build. When I wanted to play music after I paused Spotify for a couple of minutes, the music doesn't play again. So I created a small PowerShell script that kills all the Spotify instances, but it's a workaround, not a solution:

```powershell
Get-Process *spotify | Stop-Process
```

## Solution

Right click the Speaker in your taskbar. Click on "Sounds". Go to the "Playback" tab and click on your audio device. Push the "Properties" button and go to the "Advanced" tab. Under "Exclusive Mode", untick "Allow applications to take exclusive control of this device".
