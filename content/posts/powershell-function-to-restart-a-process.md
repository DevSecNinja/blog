---
title: 'PowerShell Function to Restart a Process'
date: 2016-06-19T08:30:51+00:00
draft: false
tags: ['PowerShell', 'Windows']
description: ""
cover:
  image: ""
  alt: ""
---

My notebook connects to a Docking Station with access to my receiver with speakerset, 2 screens, power and a KVM switch for my mouse and keyboard.

When I lock my laptop, the sounds switches from the receiver to my internal speakers.

When I unlock my laptop, the sound switches back but the Spotify application doesn't play any sound.

Closing the application doesn't solve this problem, because the application will crash and I have to use the Task Manager to force the application to close. I made a PowerShell function that I've added to my PowerShell profile. https://gist.github.com/jvravensberg/302a3de8dbc92b54812afc408f5c43ec The Restart-Spotify function looks for any process that ends with "spotify" and stops the process.

When all the processes are killed, a new instance of Spotify will be opened and the PowerShell console will close itself.

Even a reinstall of Spotify doesn't help solving this issue I'm facing for months now.

So the above script is a great workaround for me.
