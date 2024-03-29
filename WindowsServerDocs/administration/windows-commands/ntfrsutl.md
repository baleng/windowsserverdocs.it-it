---
title: ntfrsutl
description: 'Argomento dei comandi di Windows per * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d7721a19-5a87-4ab6-b816-65d2da2c811f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f1301b6876698e9eb552ae0ef9e70ed278319a7c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372618"
---
# <a name="ntfrsutl"></a>ntfrsutl

>Si applica a: Windows Server (canale semestrale), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Esegue il dump delle tabelle interne, thread e informazioni sulla memoria per il servizio Replica File NT \(NTFRS\). Viene eseguito su server locali e remoti. L'impostazione di ripristino per NTFRS in Gestione controllo servizi \(SCM @ no__t-1 può essere fondamentale per l'individuazione e la conservazione di importanti eventi di log nel computer. Questo strumento fornisce un metodo comodo per rivedere le impostazioni.   
  
## <a name="syntax"></a>Sintassi  
  
```  
ntfrsutl[idtable|configtable|inlog|outlog][<computer>]  
ntfrsutl[memory|threads|stage][<computer>]  
ntfrsutl ds[<computer>]  
ntfrsutl [sets][<computer>]  
ntfrsutl [version][<computer>]  
ntfrsutl poll[/quickly[=[<N>]]][/slowly[=[<N>]]][/now][<computer>]  
```  
  
### <a name="parameters"></a>Parametri  
  
|  Parametro  |                                                                                                                                                                                                                                                                                                                                        Descrizione                                                                                                                                                                                                                                                                                                                                         |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   IDTable   |                                                                                                                                                                                                                                                                                                                                          Tabella ID                                                                                                                                                                                                                                                                                                                                          |
| ConfigTable |                                                                                                                                                                                                                                                                                                                                  Tabella di configurazione del servizio Replica file                                                                                                                                                                                                                                                                                                                                   |
|    inlog    |                                                                                                                                                                                                                                                                                                                                        Log in ingresso                                                                                                                                                                                                                                                                                                                                         |
|   outlog    |                                                                                                                                                                                                                                                                                                                                        Registro in uscita                                                                                                                                                                                                                                                                                                                                        |
| <computer>  |                                                                                                                                                                                                                                                                                                                                  Specifica il computer.                                                                                                                                                                                                                                                                                                                                   |
|   memoria    |                                                                                                                                                                                                                                                                                                                                        Utilizzo della memoria                                                                                                                                                                                                                                                                                                                                        |
|   thread   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|    fase    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|     dominio Active Directory      |                                                                                                                                                                                                                                                                                                                         elenca la visualizzazione del servizio NTFRS del servizio di dominio Active Directory.                                                                                                                                                                                                                                                                                                                          |
|    Imposta     |                                                                                                                                                                                                                                                                                                                             Specifica il set di repliche attivi                                                                                                                                                                                                                                                                                                                              |
|   version   |                                                                                                                                                                                                                                                                                                                       Specifica le versioni del servizio NTFRS e API.                                                                                                                                                                                                                                                                                                                        |
|    polling     | Specifica gli intervalli di polling corrente.<br /><br />Parametri:<br /><br /><ul><li>**\/quickly**\[ **\=** \[ <N> @ no__t-7 @ no__t-8 @ no__t-9Polls rapidamente @ no__t-10<br /><br /><ul><li>\- **rapidamente** esegue il polling fino a quando la configurazione stabile non è rectrieved</li><li>il polling **rapido di @ no__t-1** \- viene eseguito rapidamente ogni minuti predefiniti.</li><li>**@ no__t-1**<N> \- esegue rapidamente il polling ogni *N* minuti</li></ul></li><li>**\/slowly**\[ **\=** \[ <N> @ no__t-7 @ no__t-8 \(Polls lentamente @ no__t-10<br /><br /><ul><li>**lentamente** \- esegue il polling lentamente fino a quando non viene recuperata la configurazione stabile</li><li>**slowly @ no__t-1** \- esegue il polling lentamente ogni minuti predefiniti</li><li>**slowly @ no__t-1**<N> \- esegue rapidamente il polling ogni *N* minuti</li></ul></li><li>**\/now** \(Polls Now @ no__t-3</li></ul> |
|     \/?     |                                                                                                                                                                                                                                                                                                                            Visualizza la guida al prompt dei comandi.                                                                                                                                                                                                                                                                                                                            |
  
## <a name="BKMK_Examples"></a>Esempi  
Per determinare l'intervallo di polling per la replica di file:  
  
```  
C:\Program Files\SupportTools>ntfrsutl poll wrkstn-1  
```  
  
Per determinare le interfacce NTFRS corrente \(API\) versione:  
  
```  
C:\Program Files\SupportTools>ntfrsutl version  
```  
  
## <a name="additional-references"></a>Riferimenti aggiuntivi  
  
-   [Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)  
  
  
  

