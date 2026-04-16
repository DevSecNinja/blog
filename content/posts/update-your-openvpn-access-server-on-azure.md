---
title: 'Update your OpenVPN Access Server on Azure'
date: 2020-02-02T10:00:00+00:00
draft: false
tags: ['Azure', 'Linux', 'OpenVPN', 'Patching', 'Virtual Private Network']
description: ""
cover:
  image: ""
  alt: ""
---

**The OpenVPN Access Server appliance in Azure allows you to quickly setup an Azure Virtual Machine that you can use for VPN purposes. I've been using an OpenVPN Access Server myself for a couple of months now and I'm happy with the performance and features.

Even on a very small VM size like the _Standard B1ms_ with 1 vCPUs and 2 GiB of memory.

At the time of writing this blog post, the documentation of OpenVPN is a bit vague about updating your Azure OpenVPN Access Server, so I wanted to share with you what is needed to keep your OpenVPN Access Server up-to-date.**

## Prerequisites

Before we start updating the OpenVPN Access Server, it's important that you have an active SSH connection with _root_ privileges. You can either get these by running _sudo -i_ or by prefixing every command below with _sudo_. Additionally, I would recommend to create a snapshot of the Azure VM Disk to ensure that we can always go back to an earlier point in time when the update fails.

## What we know about the OpenVPN appliance

The virtual appliance is based on Ubuntu. In my case, it's based on Ubuntu 18.04 LTS. You can find this by running the command below.

```
root@server:~# cat /etc/*-release

DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=18.04
DISTRIB_CODENAME=bionic
DISTRIB_DESCRIPTION="Ubuntu 18.04.4 LTS"
NAME="Ubuntu"
VERSION="18.04.4 LTS (Bionic Beaver)"
```

Now that we know that the virtual appliance uses Ubuntu, we can check if the OpenVPN software is available on the sources list of _apt_:

```
root@server:~# cat /etc/apt/sources.list.d/openvpn-as-repo.list

deb http://as-repository.openvpn.net/as/debian bionic main
```

Great! So now we can check if the packages are actually visible in _apt_:

```
root@server:~# apt list | grep 'openvpn'

gadmin-openvpn-client/bionic 0.1.9-1 amd64
gadmin-openvpn-server/bionic 0.1.5-3.1build1 amd64
gadmin-openvpn-server-dbg/bionic 0.1.5-3.1build1 amd64
network-manager-openvpn/bionic 1.8.2-1 amd64
network-manager-openvpn-gnome/bionic 1.8.2-1 amd64
openvpn/bionic-updates 2.4.4-2ubuntu1.3 amd64
openvpn-as/bionic,now 2.7.5-932a08a3-Ubuntu18 amd64 [installed]
openvpn-as-bundled-clients/bionic,now 3 all [installed,automatic]
openvpn-auth-ldap/bionic 2.0.3-6.1ubuntu2 amd64
openvpn-auth-radius/bionic 2.1-6build1 amd64
openvpn-auth-radius-dbg/bionic 2.1-6build1 amd64
openvpn-systemd-resolved/bionic 1.2.7-1 amd64
```

## Updating the OpenVPN Access Server on Azure

Now that we know that the OpenVPN software is managed by _apt_, we can easily apply OpenVPN updates:

```
root@server:~# apt update && apt upgrade

Hit:1 http://azure.archive.ubuntu.com/ubuntu bionic InRelease
Hit:2 http://azure.archive.ubuntu.com/ubuntu bionic-updates InRelease
Hit:3 http://azure.archive.ubuntu.com/ubuntu bionic-backports InRelease
Hit:4 http://as-repository.openvpn.net/as/debian bionic InRelease
Get:5 http://security.ubuntu.com/ubuntu bionic-security InRelease [88.7 kB]
Fetched 88.7 kB in 0s (181 kB/s)
Reading package lists... Done
Building dependency tree
Reading state information... Done
All packages are up to date.
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```

As you can see at Hit:4, _apt_ contacts the OpenVPN update service to see if there is a new version available. Luckily I'm already fully up-to-date.
