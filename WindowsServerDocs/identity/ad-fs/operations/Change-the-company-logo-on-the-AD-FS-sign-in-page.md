---
ms.assetid: f7f6bac2-1100-4b00-a248-4ca3eb3cdbe9
title: Modifica del logo della società nella pagina di accesso AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 03/08/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b22c969e0113081e1ca8a662ae81a2ee24829835
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358301"
---
# <a name="changing-the-company-logo-on-the-ad-fs-sign-in-page"></a>Modifica del logo della società nella pagina di accesso AD FS

#### <a name="change-company-logo"></a>Cambiare il logo della società  
Per modificare il logo della società visualizzato nella pagina Sign @ no__t-0cm, usare la sintassi e il cmdlet di PowerShell per Windows PowerShell seguente.  

![cambia logo](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  
> [!IMPORTANT]  
> È consigliabile usare un logo con dimensioni di 260x35, 96 dpi, in un file con dimensioni massime di 10 KB.  
  
    
    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.png"}  

  
> [!NOTE]  
> Il parametro `TargetName` è obbligatorio. Il tema predefinito rilasciato con AD FS è denominato *default*.  

## <a name="additional-references"></a>Altri riferimenti 
[Personalizzazione dell'accesso utente AD FS](AD-FS-user-sign-in-customization.md)  
