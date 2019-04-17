---
title: Azure AD UX Web Theme in AD FS
description: The following document describes how to change the AD FS forms sign-in so that it resembles the Azure AD user experience.
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/24/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e7bac1db17eb4facc7643fe0db0ccf00c119a45d
ms.sourcegitcommit: 9278435cbfa8dbeb30d0557ed0d27832b154edd2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/09/2018
---
# <a name="using-an-azure-ad-ux-web-theme-in-active-directory-federation-services"></a>Using an Azure AD UX Web Theme in Active Directory Federation Services
The AD FS forms sign in currently does not mirror the Azure/O365 sign-in experience.  To provide a more uniform and seamless experience for end-users, we have released the follow cascading style sheet web theme which can be applied to your AD FS servers.  Currently, the forms sign-in for AD FS on Windows Server 2016 looks like following:

![Current sign-in](media/Azure-UX-Web-Theme-in-AD-FS/one.png)


With the new style sheet, the user experience will look more like the Azure and Office 365 sign-in experiences.

## <a name="download-the-css-style-sheet"></a>Download the CSS style sheet
You can download the web theme from the following Github [location](https://github.com/Microsoft/adfsWebCustomization/tree/master/centeredUi).


## <a name="enabling-the-new-web-theme"></a>Enabling the new web theme
To enable the new web theme use the following procedure:

### <a name="to-enable-the-new-azure-ad-ux-web-theme-in-ad-fs"></a>To enable the new Azure AD UX web theme in AD FS
1.  Start PowerShell as an Administrator
2.  Create a new web theme using PowerShell:  `New-AdfsWebTheme –Name custom –StyleSheet @{path="c:\NewTheme.css"}`
3.  Set the new theme as the active theme using PowerShell:  `Set-AdfsWebConfig -ActiveThemeName custom`
![PowerShell](media/Azure-UX-Web-Theme-in-AD-FS/two.png)
4.  Test the sign-in by going to https://<AD FS name.domain>/adfs/ls/idpinitiatedsignon.htm ![Sign-on](media/Azure-UX-Web-Theme-in-AD-FS/three.png)

>![NOTE] You need to ensure that idpinitiatedsignon has been enabled.  It is not enabled by default.  To enable idpinitiatedsignon use the following PowerShell command:  `Set-AdfsProperties –EnableIdpInitiatedSignonPage $True`

## <a name="image-recommendations"></a>Image Recommendations
The following are the size recommendations for the background image and the logo image:

### <a name="logo"></a>Logo
- size 24px height, 256px max width
- Do not add any padding around the logo within the asset.  Ensure that the asset background is transparent.

### <a name="background"></a>Sfondo
- size 1024 x 1080 pixels with a file size of no greater than 200KB.  You should use the highest resolution possible with aspect ratio 16:9/16:10 that keeps the image size under the restriction.

## <a name="next-steps"></a>Passaggi successivi
- [Personalizzazione di AD FS in Windows Server 2016](AD-FS-Customization-in-Windows-Server-2016.md)
- [Personalizzazione avanzata](Advanced-Customization-of-AD-FS-Sign-in-Pages.md)
- [Temi web personalizzati](Custom-Web-Themes-in-AD-FS.md)
