---
title: 'Windows Storage Spaces - Remove physical disk from storage pool with PowerShell'
date: 2015-01-02T15:08:48+00:00
draft: false
tags: ['Microsoft', 'PowerShell', 'Storage Pool', 'Storage Spaces', 'Windows 8', 'Windows Server 2012']
description: ""
cover:
  image: ""
  alt: ""
---

I have an Intel NUC with 8 GB as media center and Hyper-V host for a test domain controller. I attached 2 physical external disks (1x 2,5" USB 3, 1x 3,5" USB 2) and created a storage pool. A couple of weeks later, I bought a new 2,5" USB 3 disk with 1 TB to replace the older USB 2.0 disk.

That disk is a lot quieter than the older one.

First, attach the new disk and make sure it's added to your storage pool.

You can't remove the physical disk from the console when it's in use.

The only option is to rename a disk:[

![Remove-PhysicalDisk-1](/images/2015/01/remove-physicaldisk-1.png)](/images/2015/01/remove-physicaldisk-1.png)

## Remove physical disk from the storage pool with PowerShell

Open PowerShell (as Administrator) and paste the following code:

> Get-PhysicalDisk

[![Remove-PhysicalDisk-2](/images/2015/01/remove-physicaldisk-2.png)](/images/2015/01/remove-physicaldisk-2.png) As you can see, my drives are in a healthy state and operational. We need the FriendlyName of the device. You can use -AutoSize after ft or just use FriendlyName:

> Get-PhysicalDisk | ft FriendlyName

[![Remove-PhysicalDisk-3](/images/2015/01/remove-physicaldisk-3.png)](/images/2015/01/remove-physicaldisk-3.png) Copy the FriendlyName of the Physical Drive you want to remove from the storage pool and use the following code:

> Set-PhysicalDisk -FriendlyName "<DeviceName>" -Usage Retired

[![Remove-PhysicalDisk-4](/images/2015/01/remove-physicaldisk-4.png)](/images/2015/01/remove-physicaldisk-4.png) We have to repair the Virtual Disks on the drives, because some Virtual Disks are maybe located on the retired drive. Firstly, make sure you know the name of the Virtual Disk:

> Get-VirtualDisk

[![Remove-PhysicalDisk-5](/images/2015/01/remove-physicaldisk-5.png)](/images/2015/01/remove-physicaldisk-5.png) If your Virtual Disk names are too long for the output, you can use

> Get-VirtualDisk | ft -AutoSize

Copy the FriendlyName of the first Virtual Disk and type:

> Repair-VirtualDisk -FriendlyName "YourVirtualDisk"

Do this for every Virtual Disk in the storage pool. Some repairs are quick, because the Virtual Disk was not located on the drive or was very small. Open a new PowerShell window to monitor the repairs with

> Get-StorageJob

[![Remove-PhysicalDisk-6](/images/2015/01/remove-physicaldisk-6.png)](/images/2015/01/remove-physicaldisk-6.png) Last but not least: remove the PhysicalDisk if all repairs are successfully done. Make sure that your drive is in the output of the following command:

> Get-PhysicalDisk | Where-Object { $\_.Usage -eq 'Retired'}

[![Remove-PhysicalDisk-7](/images/2015/01/remove-physicaldisk-7.png)](/images/2015/01/remove-physicaldisk-7.png) Assign the disk to a variable:

> $DiskToRemove = Get-PhysicalDisk | Where-Object { $\_.Usage -eq 'Retired'}

Find the name of the storage pool:

> Get-StoragePool

[![Remove-PhysicalDisk-8](/images/2015/01/remove-physicaldisk-8.png)](/images/2015/01/remove-physicaldisk-8.png) Delete the physical disk from the storage pool:

> Remove-PhysicalDisk -PhysicalDisks $DiskToRemove -StoragePoolFriendlyName "Storage pool"

This should work! Your drive should now be deleted.

## Troubleshooting

> Remove-PhysicalDisk: One of the physical disks specified could not be removed because it is still in use.

[

![Remove-PhysicalDisk-12](/images/2015/01/remove-physicaldisk-12.png)](/images/2015/01/remove-physicaldisk-12.png) If the Remove-PhysicalDisk command doesn't work, try to remove the disk when the device is turned off, so you can see which virtual disk is using the physical drive. Turn the device off and attach the drive. I had a simple storage space on the old hard disk. I had to delete that storage space manually before the command above worked.
