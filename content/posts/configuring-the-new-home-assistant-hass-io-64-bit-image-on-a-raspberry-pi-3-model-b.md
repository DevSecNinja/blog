---
title: 'Configuring the new Home Assistant Hass.io 64-bit image on a Raspberry Pi 3 Model B+'
date: 2018-08-04T06:00:53+00:00
draft: false
tags: ['Domotica', 'Hass.IO', 'HassIO', 'Home Assistant', 'Raspberry Pi']
aliases:
    - /2018/08/04/configuring-the-new-home-assistant-hass-io-64-bit-image-on-a-raspberry-pi-3-model-b-/
description: ""
cover:
  image: ""
  alt: ""
---

My [last blog post](http://DevSecNinja.com/2018/07/20/installing-the-new-home-assistant-hass-io-64-bit-image-on-a-raspberry-pi-3-model-b/) was all about getting Hass.io (or HassIO) installed on the new Raspberry Pi 3 Model B+.

This guide starts [right where we left](http://DevSecNinja.com/2018/07/20/installing-the-new-home-assistant-hass-io-64-bit-image-on-a-raspberry-pi-3-model-b/) off: configuring Home Assistant to work with the configuration files we already have from Home Assistant running on Raspbian.

Below are the steps I took in a nutshell.

- Install and open the Configurator Add-on on Hass.io to make sure you can always open the web UI to change your configurations.
- Create a snapshot so you can always go back to this point in time.
- Cut/paste the BaseURL and SSL settings from the configuration.yaml on your old Pi to the new configuration.yaml on your new Pi by using the Configurator add-on. Make sure that you have an SSH session open to the old Pi on the IP address of the old Pi, so you can still copy/paste the contents of various configurations. Also stop the Home Assistant service on your old Raspberry Pi and change any port forwarding rules in your firewall or DNS settings. (Depending on your old setup)
- Got your Home Assistant ready under the original URL? Create a new snapshot, just to be sure.
- Start copying the contents of your configuration.yaml and other relevant YAML configurations by grabbing it from SSH and pasting it in the Configurator Add-on. I was surprised to see that all the modules I've used before on Raspbian are working fine on Hass.io! So don't worry too much about that.
- Go to your Hass.io URL and confirm the dashboard is back to where it was before.

Let me know if this guide helped you out! Cheers!
