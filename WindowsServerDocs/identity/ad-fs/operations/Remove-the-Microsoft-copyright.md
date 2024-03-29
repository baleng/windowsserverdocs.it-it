---
ms.assetid: c89a977c-b09f-44ec-be42-41e76a6cf3ad
title: Rimuovere il copyright Microsoft
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0c24173dd03e03f9e8a19ef5981a6dc1259d62d7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407510"
---
# <a name="remove-the-microsoft-copyright"></a>Rimuovere il copyright Microsoft 


 
Per impostazione predefinita, le pagine di ADFS includono il copyright Microsoft. Per rimuoverlo dalle pagine personalizzate, è possibile usare la procedura seguente. 

![rimuovere il copyright](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png) 
  
## <a name="to-remove-the-microsoft-copyright"></a>Per rimuovere il copyright Microsoft  
  
1. Creare un tema personalizzato basato su quello predefinito.

   ```powershell
   New-AdfsWebTheme –Name custom –SourceName default
   ```

2. Esportare il tema specificando la cartella di output.  

   ```powershell
   Export-AdfsWebTheme -Name custom -DirectoryPath C:\CustomWebTheme
   ```

3. Individuare il file `Style.css` che si trova nella cartella di output. Utilizzando l'esempio precedente, il percorso sarà `C:\CustomWebTheme\Css\Style.css.`
  
4. Aprire il file `Style.css` con un editor, ad esempio Blocco note.  
  
5. Trovare la parte `#copyright` e modificarla come segue:  

   ```css
   #copyright {color:#696969; display:none;}
   ```

6. Creare un tema personalizzato basato sul nuovo file `Style.css`.  

   ```powershell
   Set-AdfsWebTheme -TargetName custom -StyleSheet @{locale="";path="C:\customWebTheme\css\style.css"}
   ```

7. Attivare il nuovo tema.  

   ```powershell
   Set-AdfsWebConfig -ActiveThemeName custom
   ```

A questo punto, non dovrebbe essere il copyright nella parte inferiore della pagina di accesso.

![rimuovere il copyright](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1a.png) 

## <a name="additional-references"></a>Altri riferimenti 
[Personalizzazione dell'accesso utente AD FS](AD-FS-user-sign-in-customization.md) 
