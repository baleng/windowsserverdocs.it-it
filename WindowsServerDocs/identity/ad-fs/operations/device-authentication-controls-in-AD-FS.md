---
title: Device Authentication controls in AD FS
description: This document describes how to enable device authentication in AD FS for Windows Server 2016 and 2012 R2
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 11/09/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d66cfde20060229844c34abeea85dd83b802ddad
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/12/2017
---
# <a name="device-authentication-controls-in-ad-fs"></a>Device authentication controls in AD FS
The following document shows how to enable device authentication controls in Windows Server 2016 and 2012 R2.

## <a name="device-authentication-controls-in-ad-fs-2012-r2"></a>Device Authentication controls in AD FS 2012 R2
Originally in AD FS 2012 R2 there was one global authentication property called `DeviceAuthenticationEnabled` that controlled device authentication.

To configure the setting, the `Set-AdfsGlobalAuthenticationPolicy` cmdlet was used as shown below:


``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationEnabled $true
```



To disable device authentication, the same cmdlet was used to set the value to $false.

## <a name="device-authentication-controls-in-ad-fs-2016"></a>Device Authentication controls in AD FS 2016
The only type of device authentication supported in 2012 R2 was clientTLS.  In AD FS 2016, in addition to clientTLS there are two new types of device authentication for modern devices authentication.  These are:
- PKeyAuth
- PRT

To control the new behavior, the `DeviceAuthenticationEnabled` property is used in combination with a new property called `DeviceAuthenticationMethod`.  

The device authentication method determines the type of device authentication that will be done: PRT, PKeyAuth, clientTLS, or some combination.
It has the following values:
 - SignedToken: PRT only
 - PKeyAuth: PRT + PKeyAuth
 - ClientTLS: PRT + clientTLS 
 - All: All of the above

As you can see, PRT is part of all device authentication methods, making it in effect the default method that is always enabled when `DeviceAuthenticationEnabled` is set to `$true`.

Example: To configure the method(s), use the DeviceAuthenticationEnabled cmdlet as above, along with new property:

``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationEnabled $true
```
>[!NOTE]
> Enabling device authentication (setting `DeviceAuthenticationEnabled` to `$true`) means the `DeviceAuthenticationMethod` is implicitly set to `SignedToken`, which equates to **PRT**.


``` powershell
PS:\>Set-AdfsGlobalAuthenticationPolicy –DeviceAuthenticationMethod All
```
>[!NOTE]
>The default device authentication method is `SignedToken`.  Other values are **PKeyAuth,****ClientTLS,** and **All**.

The meanings of the `DeviceAuthenticationMethod` values have changed slightly since AD FS 2016 was released.  See the table below for the meaning of each value, depending on the update level:


|AD FS version|DeviceAuthenticationMethod value|Significa|
| ----- | ----- | ----- |
|2016 RTM|SignedToken|PRT + PkeyAuth|
||clientTLS|clientTLS|
||Tutti|PRT + PkeyAuth + clientTLS|
|2016 RTM + up to date with Windows Update|SignedToken (changed meaning)|PRT (only)|
||PkeyAuth (new)|PRT + PkeyAuth|
||clientTLS|PRT + clientTLS|
||Tutti|PRT + PkeyAuth + clientTLS|

## <a name="see-also"></a>Vedere anche
[Operazioni di ADFS](../../ad-fs/AD-FS-2016-Operations.md)
