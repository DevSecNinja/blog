---
title: 'Windows AutoPilot - New Features'
date: 2018-03-31T07:00:18+00:00
draft: false
tags: ['Azure', 'Azure AD', 'Deployment', 'Intune', 'MDM', 'Windows', 'Windows AutoPilot']
description: ""
cover:
  image: ""
  alt: ""
---

**With the Windows 10 Creators Update, Microsoft introduced Windows AutoPilot. Windows AutoPilot is a service which allows users to enroll their device with the Intune/Azure AD tenant of the organization during the Out-of-the-Box (OOBE) experience of Windows 10.

By using Windows AutoPilot, organizations can dramatically decrease the time needed to configure a new device.

During Microsoft Tech Summit 2018 in Amsterdam, Michael Niehaus announced some exciting new features which I will discuss in this blog post too.**

## Deployment Scenario

First a very short introduction on the deployment scenario. With Windows AutoPilot, the following deployment scenario now becomes reality:

1. As a new employee, John joins the Contoso organization in 4 weeks.
2. Contoso creates a user account for John and will also order a new Surface Book 2 with their preferred OEM, Microsoft.
3. John will receive the Surface Book 2 notebook at home 1 week before his first day at Contoso.
4. John will boot up the device, is prompted to login with the Contoso organization and has access to all the necessary resources like applications and portals. This step enrolls John's device with Azure AD and Intune so that the device is managed by the organization.

This deployment scenario involves no IT personnel while the user can start using the device within 15 minutes!

### OEM Support

When you buy a device with one of the supported OEMs, the device are automatically added to the Windows AutoPilot service and ready for deployment. No manual registration needed! The following OEMs support Windows AutoPilot:

- Microsoft (Surface) - Now
- Lenovo (end of March)
- Hewlett Packard - HP (first half of CY2018)
- Dell (second half of CY2018)
- Panasonic (second half of CY2018)
- Fujitsu (second half of CY2018)
- Toshiba (second half of CY2018)

## Configuration

Windows AutoPilot can be configured from the Azure Portal [if you follow these steps](https://docs.microsoft.com/en-us/windows/deployment/windows-autopilot/windows-10-autopilot). One of the last steps is to create a Windows AutoPilot Deployment profile. Currently, the settings here are quite limited as you can see below:

![chrome_2018-03-31_07-19-27](/images/2018/03/chrome_2018-03-31_07-19-27.png)

_Windows AutoPilot Deployment Profile Settings in the Azure Portal_

## New features announced during Tech Summit

I see a lot of potential in Windows AutoPilot, especially because Microsoft released some new details during last Microsoft Tech Summit in Amsterdam. (Slide Deck not available yet - but found [his slide deck from Expert Live US](https://schd.ws/hosted_files/elus18/38/MNiehaus%20AutoPilot.pptx) on the web)

### Hybrid Azure AD Join

The slide below describes it all. In the near future, you can join devices to Active Directory as well, by using an Offline Domain Join connector and a VPN connection! In theory this means you can now manage those devices with Active Directory (GPOs etc.) and SCCM too! This is a brilliant idea and will allow a lot of organizations to use Windows AutoPilot now while migrating to a modern workplace.

![chrome_2018-03-31_08-01-33.png](/images/2018/03/chrome_2018-03-31_08-01-33.png)

_Hybrid Azure AD Join with Windows AutoPilot [(Source)](https://schd.ws/hosted_files/elus18/38/MNiehaus%20AutoPilot.pptx)_

### Captive Portal support

Some organizations have Guest WiFi with a captive portal where the user needs to agree on terms. This will be supported in the OOBE. I requested this years ago with Microsoft, so great to see it will be there soon.

### Plug and Forget

With Plug and Forget, Microsoft delivers a deployment solution for devices like scoring boards or information screens at airports. The technician can plug the device into ethernet/power and it automatically self-deploys itself into the Windows AutoPilot service. Cool stuff.

## Feature requests for Windows AutoPilot

### Pre-defined keyboard layout

As OEMs are already capturing the information to join a device into the Windows AutoPilot service, I would like to see that OEMs also forward keyboard layout information to Microsoft so users don't have to select a keyboard lay-out. In the Netherlands, most people are using the United States International instead of the Dutch keyboard lay-out. So if the OEM already knows which keyboard is on the device, why not pass that along to Microsoft?

![chrome_2018-03-31_08-06-50](/images/2018/03/chrome_2018-03-31_08-06-50-e1522476458201.png)

_Windows 10 Keyboard Layout selection in OOBE [(Source)](https://schd.ws/hosted_files/elus18/38/MNiehaus%20AutoPilot.pptx)_

### Install applications or needed binaries at the factory

In some scenarios, organizations are limited on network bandwidth. Shipping a device with the binaries of the applications already on the disk would increase both installation speed and adoption at low-bandwidth locations.

### Custom options during or at the end of OOBE

Think about showing a (web)page to a user with content on how a user can enroll with certain services or where they can find their applications. Or get rid of the install and configuration documentation by showing a manual from the organization. I'm really excited to see the new features for Windows AutoPilot! Let me know what you think in the comments! Cheers, Jean-Paul
