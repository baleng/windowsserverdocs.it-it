---
title: tasklist
description: Informazioni su come visualizzare un elenco dei processi in esecuzione nel computer locale o remoto.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8dbe30ee-1484-46be-917b-5ca3ff4fdc9c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f7ad61dfe8beb86c8299dd71bec1d862805e50e0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383676"
---
# <a name="tasklist"></a>tasklist

Visualizza un elenco dei processi attualmente in esecuzione nel computer locale o in un computer remoto. **TaskList** sostituisce lo strumento **Tlist** .

Per esempi di utilizzo di questo comando, vedere [Esempi](#BKMK_examples).

## <a name="syntax"></a>Sintassi

```
tasklist [/s <Computer> [/u [<Domain>\]<UserName> [/p <Password>]]] [{/m <Module> | /svc | /v}] [/fo {table | list | csv}] [/nh] [/fi <Filter> [/fi <Filter> [ ... ]]]
```

## <a name="parameters"></a>Parametri

|          Parametro           |                                                                                                                                            Descrizione                                                                                                                                             |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        /s \<Computer >        |                                                                                         Specifica il nome o l'indirizzo IP di un computer remoto (non utilizzare barre rovesciate). Il valore predefinito è il computer locale.                                                                                         |
| /u [\<Domain > \\ @ no__t-2 @ no__t-3UserName > | Esegue il comando con le autorizzazioni dell'account dell'utente specificato da *username* o *Domain*\*UserName. è possibile specificare<em>\* @ no__t-5/u</em>\* solo se è specificato **/s** . Il valore predefinito è le autorizzazioni dell'utente attualmente connesso al computer che sta eseguendo il comando. |
|        /p \<password >        |                                                                                                       Specifica la password dell'account utente specificato nella **/u** parametro.                                                                                                        |
|         /m \<Module >         |                                                               Elenca tutte le attività con i moduli DLL caricati che corrispondono al nome del modello specificato. Se il nome del modulo non è specificato, questa opzione consente di visualizzare tutti i moduli caricati da ogni attività.                                                                |
|             /SVC             |                                                                                    Elenca tutte le informazioni del servizio per ogni processo senza troncamento. Valido quando il parametro **/fo** è impostato su **Table**.                                                                                    |
|              /v              |                                                                                 Visualizza informazioni dettagliate sull'attività nell'output. Per un output dettagliato completo senza troncamento, usare **/v** e **/SVC** insieme.                                                                                 |
|  /fo {TABLE \| list \| CSV}  |                                                                             Specifica il formato da utilizzare per l'output. I valori validi sono **tabella**, **elenco**, e **csv**. Il formato predefinito per l'output è **Table**.                                                                             |
|             /NH              |                                                                                             Elimina le intestazioni di colonna nell'output. Valido quando il parametro **/fo** è impostato su **Table** o **CSV**.                                                                                              |
|        > \<filtro/Fi         |                                                                          Specifica i tipi di processi da includere o escludere dalla query. Vedere la tabella seguente per i nomi di filtro, gli operatori e i valori validi.                                                                          |
|              /?              |                                                                                                                                Visualizza la guida al prompt dei comandi.                                                                                                                                |

### <a name="filter-names-operators-and-values"></a>Filtrare nomi, operatori e valori

| Nome filtro |    Operatori validi     |                                                                 Valori validi                                                                 |
|-------------|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|   STATO    |         eq, ne         |                                                                   ESECUZIONE                                                                    |
|  IMAGENAME  |         eq, ne         |                                                                  Nome immagine                                                                  |
|     PID     | eq, ne, gt, lt, ge, le |                                                                  Valore PID                                                                   |
|   SESSIONE   | eq, ne, gt, lt, ge, le |                                                                Numero sessione                                                                |
| NOMESESSIONE |         eq, ne         |                                                                 Nome sessione                                                                 |
|   CPUTIME   | eq, ne, gt, lt, ge, le | Tempo CPU nel formato <em>HH</em> **:** <em>mm</em> **:** <em>SS</em>, dove *mm* e *SS* sono comprese tra 0 e 59 e *HH* è un numero senza segno |
|  MEMUSAGE   | eq, ne, gt, lt, ge, le |                                                              Utilizzo memoria in KB                                                              |
|  NOME UTENTE   |         eq, ne         |                                                             Qualsiasi nome utente valido                                                              |
|  SERVIZI   |         eq, ne         |                                                                 Nome del servizio                                                                 |
| WINDOWTITLE |         eq, ne         |                                                                 Titolo della finestra                                                                 |
|   MODULI   |         eq, ne         |                                                                   Nome DLL                                                                   |

## <a name="remarks"></a>Note

I filtri di stato e WINDOWTITLE non sono supportati quando si specifica un sistema remoto.

## <a name="BKMK_examples"></a>Esempi

Per elencare tutte le attività con un ID di processo superiore a 1000 e visualizzarle in formato CSV, digitare:
```
tasklist /v /fi "PID gt 1000" /fo csv
```
Per elencare i processi di sistema attualmente in esecuzione, digitare:
```
tasklist /fi "USERNAME ne NT AUTHORITY\SYSTEM" /fi "STATUS eq running"
```
Per elencare le informazioni dettagliate per tutti i processi attualmente in esecuzione, digitare:
```
tasklist /v /fi "STATUS eq running"
```
Per elencare tutte le informazioni sul servizio per i processi nel computer remoto "SRVPRINC" con un nome di DLL che inizia con "ntdll", digitare:
```
tasklist /s srvmain /svc /fi "MODULES eq ntdll*"
```
Per elencare i processi nel computer remoto "SRVPRINC", usando le credenziali dell'account utente attualmente connesso, digitare:
```
tasklist /s srvmain 
```
Per elencare i processi nel computer remoto "SRVPRINC", usando le credenziali dell'account utente hiropln, digitare:
```
tasklist /s srvmain /u maindom\hiropln /p p@ssW23
```

#### <a name="additional-references"></a>Altri riferimenti

[Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)