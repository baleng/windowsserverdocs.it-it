---
title: Utilizzando il comando get-MulticastTransmission
description: 'Argomento dei comandi di Windows per * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b733737b-1e81-43d4-a058-d6985a613bef
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 54c503abda871d1f2a4fd8a30d7f12317eee6a48
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392130"
---
# <a name="using-the-get-multicasttransmission-command"></a>Utilizzando il comando get-MulticastTransmission

>Si applica a: Windows Server (canale semestrale), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Visualizza le informazioni sulla trasmissione multicast per un'immagine specificata.
## <a name="syntax"></a>Sintassi
**Windows Server 2008**
```
wdsutil [Options] /Get-MulticastTransmissiomedia:<Image name> [/Server:<Server name>mediatype:InstallmediaGroup:<Image group name>] 
[/Filename:<File name>] [/Show:Clients]
```
**Windows Server 2008 R2** per le trasmissioni di immagini di avvio:
```
wdsutil [Options] /Get-MulticastTransmissiomedia:<Image name>
    [/Server:<Server name>]
    [/details:Clients]
  mediatype:Boot
    /Architecture:{x86 | ia64 | x64}
        [/Filename:<File name>]
```
per le trasmissioni di immagini di installazione:
```
wdsutil [Options] /Get-MulticastTransmissiomedia:<Image name>
         [/Server:<Server name>]
         [/details:Clients]
       mediatype:Install
    mediaGroup:<Image Group>]
     [/Filename:<File name>]
```
## <a name="parameters"></a>Parametri
|Parametro|Descrizione|
|-------|--------|
supporto: <Image name>|Visualizza la trasmissione multicast associata a questa immagine.|
|[/Server:<Server name>]|Specifica il nome del server. Questo può essere il nome NetBIOS o il nome di dominio completo (FQDN). Se viene specificato alcun nome di server, viene utilizzato il server locale.|
MediaType: installazione|Specifica il tipo di immagine. Si noti che questa opzione deve essere impostata su **Installa**.|
|\mediaGroup:<Image group name>]|Specifica il gruppo di immagini che contiene l'immagine. Se viene specificato alcun nome di gruppo di immagini e il gruppo solo un'immagine esistente sul server, viene utilizzato il gruppo di immagini. Se nel server è presente più di un gruppo di immagini, è necessario utilizzare questa opzione per specificare un gruppo di immagini.|
|/ Architettura: {x86 &#124; ia64 &#124; x64}|Specifica l'architettura dell'immagine di avvio associata alla trasmissione. Poiché è possibile avere lo stesso nome di immagine per le immagini di avvio in architetture diverse, è necessario specificare l'architettura per garantire che venga utilizzata l'immagine corretta.|
|[/Filename:<File name>]|Specifica il file che contiene l'immagine. Se l'immagine non può essere identificata in modo univoco dal nome, è necessario utilizzare questa opzione per specificare il nome del file.|
|[/ Show: client]<br /><br />oppure<br /><br />[/Details: client]|Visualizza informazioni sui computer client connessi alla trasmissione multicast.|
## <a name="BKMK_examples"></a>Esempi
**Windows Server 2008** Per visualizzare le informazioni sulla trasmissione per un'immagine denominata vista con Office, digitare uno dei seguenti:
```
wdsutil /Get-MulticastTransmissiomedia:"Vista with Officemediatype:Install
wdsutil /Get-MulticastTransmission /Server:MyWDSServemedia:"Vista with Officemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim /Show:Clients
```
**Windows Server 2008 R2** Per visualizzare le informazioni sulla trasmissione per un'immagine denominata vista con Office, digitare uno dei seguenti:
```
wdsutil /Get-MulticastTransmissiomedia:"Vista with Office"
 /Imagetype:Install
```
```
wdsutil /Get-MulticastTransmission /Server:MyWDSServemedia:"Vista with Officemediatype:InstalmediaGroup:ImageGroup1 /Filename:install.wim /details:Clients
```
```
wdsutil /Get-MulticastTransmission /Server:MyWDSServemedia:"X64 Boot Imagemediatype:Boot /Architecture:x64 /Filename:boot.wim /details:Clients
```
#### <a name="additional-references"></a>Riferimenti aggiuntivi
[Chiave della sintassi della riga di comando](command-line-syntax-key.md)
[usando il comando get-AllMulticastTransmissions](using-the-get-allmulticasttransmissions-command.md)
 usando il comando[New-MulticastTransmission](using-the-new-multicasttransmission-command.md)
[usando il comando Remove-MulticastTransmission](using-the-remove-multicasttransmission-command.md)
[ Sottocomando: Start-MulticastTransmission](subcommand-start-multicasttransmission.md)
