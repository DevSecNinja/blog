---
title: 'Microsoft Teams notifications without message preview in Python'
date: 2019-03-15T14:00:19+00:00
draft: false
tags: ['Microsoft Teams', 'Notification', 'Python', 'Teams', 'Toast Message', 'Windows 10']
description: ""
cover:
  image: ""
  alt: ""
---

**Since a couple of months I've been using Microsoft Teams as my daily driver. This means that I'm fully migrated from Skype for Business to Microsoft Teams.

One of the things I'm missing is notifications without the content of the message. (also called message preview) Especially when I'm presenting my screen during a meeting, I don't want the meeting participants to read my Teams messages.

Disabling notifications and relying on the taskbar icon didn't work for me, as I've missed several messages per week.

In this post, I'll show you how I used Python to create a toast message when I get a new message from Teams.**

## Python?! Why not use PowerShell?!

You can definitely do this with PowerShell. I think it would've saved me some time to create it in PowerShell. As I'm on a journey to learn new languages, I like to keep challenging myself to do things in other languages.

## How the Python script works

As I couldn't find something a Teams client API that I could use with Python, I'm using the log files of the Teams client to discover the state of the client.

It's not something I would recommend for a mass roll-out, but it does the job for me until Microsoft fixes this. ([Vote for this UserVoice please](https://microsoftteams.uservoice.com/forums/555103-public/suggestions/32624690-turn-off-message-preview-in-notification-toast)!) Also please be aware that this is my second Python script and it might require improvement. :) It loops through the _logs.txt_ file and searches for the "Available -> NewActivity" string.

If it finds that string, it means that the Teams client is receiving a message. (E.g. a private message or a message in a channel).

The next action that the script takes is to create a toast message by using the ToastNotifier module.

## Script contents & usage

[View the repository of the script on GitHub](https://github.com/DevSecNinja/MSTeamsPrivateNotifications) and feel free to contribute by opening a Pull Request!
