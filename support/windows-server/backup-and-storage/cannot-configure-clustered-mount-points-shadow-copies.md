---
title: 0x80042306 error occurs when configuring shadow copies for clustered mount points on another drive in Windows Server 2012
description: Fixes the error 0x80042306 that occurs when you configure Previous Versions in Windows Server 2012 for the clustered disks that are mounted as folders on a different volume.
ms.date: 09/14/2020
author: Deland-Han
ms.author: delhan
manager: dscontentpm
audience: itpro
ms.topic: troubleshooting
ms.prod: windows-server
localization_priority: medium
ms.reviewer: eldenc, kaushika
ms.prod-support-area-path: Configuring and using Backup software
ms.technology: BackupStorage
---
# 0x80042306 error occurs when configuring shadow copies for clustered mount points on another drive in Windows Server 2012

This article helps fix the error 0x80042306 that occurs when you configure Previous Versions in Windows Server 2012 for the clustered disks that are mounted as folders on a different volume.

_Original product version:_ &nbsp;Windows Server 2012 R2  
_Original KB number:_ &nbsp;2828270

## Symptoms

When trying to configure Previous Versions in Windows Server 2012 for the clustered disks that are mounted as folders on a different volume, it may fail. Additionally, you may receive the following error message:
> Failed to create the storage area association.  
Error 0x80042306: The shadow copy provider had an error.  

Other symptoms you might observe when trying to configure previous versions for a mount point on another volume:

- Cluster Disk goes offline
- You may receive the following event logged for VSS:

## Cause

The error occurs because of mismatch in cluster online and offline timeouts. There's a premature exit after calling resource online/offline.

## Workaround

To work around this problem, consider modifying the registry values by following the steps mentioned below.

> [!IMPORTANT]
> This section, method, or task contains steps that tell you how to modify the registry. However, serious problems might occur if you modify the registry incorrectly. Therefore, make sure that you follow these steps carefully. For added protection, back up the registry before you modify it. Then, you can restore the registry if a problem occurs. For more information about how to back up and restore the registry, click the following article number to view the article in the Microsoft Knowledge Base:

[322756](https://support.microsoft.com/help/322756) How to back up and restore the registry in Windows


1. On the **Start** screen, click the **Search** tile.
2. Type regedit in the Search window and then double-click **regedit.exe**.
3. Locate the following registry entry:
    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\VSS\Settings` 

4. Right-click **ClusterOfflineTimeout**, and then click **Modify**.
5. Select Decimal and then type 2000000000 in the **Value data** box, and then click **OK**.
6. Right-click ClusterOnlineTimeout, and then click Modify.
7. Select Decimal and then type 2000000000 in the Value data box, and then click OK.
8. Exit Registry Editor, and then restart the computer.

Note: The Decimal value can be increased as per requirement.