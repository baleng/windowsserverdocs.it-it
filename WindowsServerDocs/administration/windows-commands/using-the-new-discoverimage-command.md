---
title: Utilizzando il comando nuovo DiscoverImage
description: 'Argomento dei comandi di Windows per * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ede9fbbb-0bba-4309-8c21-3cc13e1dc3cd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5b17777eb4d8541ce5669ee6becbd51e2b9da236
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362995"
---
# <a name="using-the-new-discoverimage-command"></a>Utilizzando il comando nuovo DiscoverImage



Crea una nuova immagine di individuazione da un'immagine di avvio esistente. Individuare le immagini sono immagini di avvio che impongono il programma Setup.exe di avvio in modalità servizi di distribuzione Windows e quindi individuare un server di servizi di distribuzione Windows. Queste immagini vengono generalmente utilizzate per distribuire le immagini ai computer che non sono in grado di consentire l'avvio di PXE. Per ulteriori informazioni, vedere Creazione di immagini ([https://go.microsoft.com/fwlink/?LinkId=115311](https://go.microsoft.com/fwlink/?LinkId=115311)).

## <a name="syntax"></a>Sintassi

```
WDSUTIL [Options] /New-DiscoverImage [/Server:<Server name>]
     /Image:<Image name>
     /Architecture:{x86 | ia64 | x64}
     [/Filename:<File name>]
     /DestinationImage
         /FilePath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
         [/WDSServer:<Server name>]
         [/Overwrite:{Yes | No | Append}]
```

## <a name="parameters"></a>Parametri

|        Parametro         |                                                                                                                                                                                                                                                                                                                                                                                                                       Descrizione                                                                                                                                                                                                                                                                                                                                                                                                                       |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server: nome \<Server >] |                                                                                                                                                                                                                                                                                                                                     Specifica il nome del server. Può essere il nome NetBIOS oppure il nome di dominio completo. Se viene specificato alcun nome di server, verrà utilizzato il server locale.                                                                                                                                                                                                                                                                                                                                     |
|   /Image: nome \<Image >   |                                                                                                                                                                                                                                                                                                                                                                                                      Specifica il nome dell'immagine di avvio di origine.                                                                                                                                                                                                                                                                                                                                                                                                       |
|    /Architettura: {x86    |                                                                                                                                                                                                                                                                                                                                                                                                                          ia64                                                                                                                                                                                                                                                                                                                                                                                                                           |
| [/Filename: \<File nome >] |                                                                                                                                                                                                                                                                                                                                                                         Se l'immagine non può essere identificata in modo univoco dal nome, è necessario utilizzare questa opzione per specificare il nome del file.                                                                                                                                                                                                                                                                                                                                                                          |
|    /DestinationImage     | Specifica le impostazioni per l'immagine di destinazione. È possibile specificare le impostazioni utilizzando le opzioni seguenti:</br>-/FilePath: < percorso e nome file > - Imposta percorso completo del file per la nuova immagine.</br>-[/Name: \<Name >]-imposta il nome visualizzato dell'immagine. Se non viene specificato alcun nome visualizzato, verrà utilizzato il nome visualizzato dell'immagine di origine.</br>-[/Description: \<Description >]-imposta la descrizione dell'immagine.</br>-[/WDSServer: \<Server nome >]-specifica il nome del server che tutti i client che eseguono l'avvio dall'immagine specificata devono contattare per scaricare l'immagine di installazione. Per impostazione predefinita, tutti i client che eseguono l'avvio di questa immagine individuerà un server di servizi di distribuzione Windows valido. Questa opzione Ignora la funzionalità di individuazione e forza il client avviato contattare il server specificato.</br>-[/Overwrite: {Yes |

## <a name="BKMK_examples"></a>Esempi

Per creare un'immagine di individuazione all'immagine di avvio esterno e denominarlo WinPEDiscover.wim, digitare:
```
WDSUTIL /New-DiscoverImage /Image:"WinPE boot image" /Architecture:x86 /DestinationImage /FilePath:"C:\Temp\WinPEDiscover.wim"
```
Per creare un'immagine di individuazione all'immagine di avvio esterno e denominarlo WinPEDiscover.wim con le impostazioni specificate, digitare:
```
WDSUTIL /Verbose /Progress /New-DiscoverImage /Server:MyWDSServer
/Image:"WinPE boot image" /Architecture:x64 /Filename:boot.wim /DestinationImage /FilePath:"\\Server\Share\WinPEDiscover.wim" 
/Name:"New WinPE image" /Description:"WinPE image for WDS Client discovery" /Overwrite:No
```

#### <a name="additional-references"></a>Altri riferimenti

[Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)