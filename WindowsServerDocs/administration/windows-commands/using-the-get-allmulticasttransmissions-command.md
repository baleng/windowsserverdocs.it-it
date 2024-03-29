---
title: Utilizzando il comando get-AllMulticastTransmissions
description: 'Argomento dei comandi di Windows per * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95b8fb79-7a8a-4f0c-88f4-92bc1111c67f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 644684ffb356ef07120bc391e3d3da2daf768eaf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363338"
---
# <a name="using-the-get-allmulticasttransmissions-command"></a>Utilizzando il comando get-AllMulticastTransmissions

>Si applica a: Windows Server (canale semestrale), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Visualizza informazioni su tutte le trasmissioni multicast in un server.
## <a name="syntax"></a>Sintassi
per Windows Server 2008:
```
wdsutil /Get-AllMulticastTransmissions [/Server:<Server name>] [/Show:Clients] [/ExcludedeletePending]
```
per Windows Server 2008 R2:
```
wdsutil /Get-AllMulticastTransmissions [/Server:<Server name>] [/Show:{Boot | Install | All}] [/details:Clients]  [/ExcludedeletePending]
```
## <a name="parameters"></a>Parametri

|        Parametro        |                                                                                                                                                                                                                                                                   Spiegazione                                                                                                                                                                                                                                                                    |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server:<Server name>] |                                                                                                                                                                                 Specifica il nome del server. Può essere il nome NetBIOS oppure il nome di dominio completo. Se viene specificato alcun nome di server, verrà utilizzato il server locale.                                                                                                                                                                                  |
|         [/Show]         | **Windows Server 2008**<br /><br />/Show:Clients - Visualizza informazioni sui computer client connessi a trasmissioni multicast.<br /><br />**Windows Server 2008 R2**<br /><br />Mostra: {Avvio &#124; Installa &#124; All} - il tipo di immagine da restituire.                                **Avvio** restituisce solo le trasmissioni di immagini di avvio.                                  **Installare** restituisce installare solo le trasmissioni di immagine. **Tutti** restituisce entrambi i tipi di immagine. |
|                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|    /details:clients     |                                                                                                                                                                                              Supportato solo per Windows Server 2008 R2. Se presente, verranno visualizzati ai client connessi alla trasmissione.                                                                                                                                                                                               |
| [/ExcludedeletePending] |                                                                                                                                                                                                                                              Esclude tutte le trasmissioni disattivate dall'elenco.                                                                                                                                                                                                                                               |

## <a name="BKMK_examples"></a>Esempi
Per visualizzare informazioni su tutte le trasmissioni, digitare:
- Windows Server 2008: `wdsutil /Get-AllMulticastTransmissions`
- Windows Server 2008 R2: `wdsutil /Get-AllMulticastTransmissions /Show:All` per visualizzare informazioni su tutte le trasmissioni eccetto le trasmissioni disattivate, digitare:
- Windows Server 2008: `wdsutil /Get-AllMulticastTransmissions /Server:MyWDSServer /Show:Clients /ExcludedeletePending`
- Windows Server 2008 R2: `wdsutil /Get-AllMulticastTransmissions /Server:MyWDSServer /Show:All /details:Clients /ExcludedeletePending`
  #### <a name="additional-references"></a>Riferimenti aggiuntivi
  [Chiave di sintassi della riga di comando](command-line-syntax-key.md)
  [utilizzando il comando get-MulticastTransmission](using-the-get-multicasttransmission-command.md)
  [utilizzando il comando /New-multicasttransmission](using-the-new-multicasttransmission-command.md)
  [utilizzando il comando remove-MulticastTransmission](using-the-remove-multicasttransmission-command.md)
  [sottocomando: inizio MulticastTransmission](subcommand-start-multicasttransmission.md)
