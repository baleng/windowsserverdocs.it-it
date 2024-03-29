---
title: Logman creare api
description: 'Argomento dei comandi di Windows per * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2ecc0a75-2613-464a-8616-c5dc404bb736
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 512602213fcfd95770af0e27b721a589ed489771
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374604"
---
# <a name="logman-create-api"></a>Logman creare api

>Si applica a: Windows Server (canale semestrale), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

creare un agente di raccolta dati di traccia API.  

## <a name="syntax"></a>Sintassi  
```  
logman create api <[-n] <name>> [options]  
```  
## <a name="parameters"></a>Parametri  

|                    Parametro                     |                                                                               Descrizione                                                                               |
|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                        /?                        |                                                                    Vengono visualizzate sensibile al contesto della Guida.                                                                     |
|                -s <computer name>                |                                                          Eseguire il comando nel computer remoto specificato.                                                          |
|                 -config <value>                  |                                                         Specifica il file di impostazioni che contiene le opzioni di comando.                                                         |
|                   [-n] <name>                    |                                                                       Nome dell'oggetto di destinazione.                                                                        |
| -f < bin &#124; bincirc &#124; csv &#124; tsv &#124; sql > |                                                            Specifica il formato di log per l'agente di raccolta dati.                                                             |
|             -u [-] < utente [password] >              | Specifica l'utente di Esegui come. L'immissione di un \* per la password genera una richiesta per la password. La password non viene visualizzata quando si digita. |
|    -m < [avvio] [stop] [[start] [stop] [...]] >    |                                                modificare l'avvio o l'arresto manuale anziché un'ora di inizio o di fine pianificata.                                                 |
|                -rf < [[hh:] mm:] ss >                |                                                        Eseguire l'agente di raccolta dati per il periodo di tempo specificato.                                                         |
|        -b < g/aaaa h:mm: ss [AM &#124; PM] >         |                                                              Avviare la raccolta dei dati all'ora specificata.                                                               |
|        -e < g/aaaa h:mm: ss [AM &#124; PM] >         |                                                               Terminare la raccolta dei dati all'ora specificata.                                                                |
|                -si < [[hh:] mm:] ss >                |                                                 Specifica l'intervallo di campionamento per raccolta dati dei contatori delle prestazioni.                                                  |
|              -o < percorso &#124; dsn! log >              |                                              Specifica che il file di log di output o DSN e di log impostare il nome in un database SQL.                                               |
|                      -[-]r                       |                                                  Ripetere l'agente di raccolta dati ogni giorno alle ore di inizio specificato e di fine.                                                  |
|                      -[-]a                       |                                                                     Accoda a un file di log esistente.                                                                     |
|                      -[-] Mostra                      |                                                                     Sovrascrivere un file di log esistente.                                                                     |
|           -v [-] < nnnnnn &#124; mmgghhmm >           |                                                   alleghi le informazioni sul controllo delle versioni dei file alla fine del nome del file di log.                                                   |
|                  -[-] RC <task>                   |                                                         Eseguire il comando specificato ogni volta che il log viene chiuso.                                                          |
|                 -max [-] <value>                  |                                                 Dimensioni massime in MB o numero massimo di record di log di SQL.                                                  |
|              -cnf [-] < [[hh:] mm:] ss >              |     Quando viene specificata l'ora, creare un nuovo file quando è trascorso il tempo specificato. Quando non viene specificata l'ora, creare un nuovo file quando viene superata la dimensione massima.     |
|                        -y                        |                                                             Rispondere Sì a tutte le domande senza chiedere conferma.                                                              |
|            -modifiche < percorso [[...]] >             |                                                          Specifica l'elenco dei moduli per registrare le chiamate API da.                                                           |
|     -inapis < module! api [module! api [...]] >      |                                                         Specifica l'elenco di chiamate API da includere nella registrazione.                                                          |
|     -exapis < module! api [module! api [...]] >      |                                                        Specifica l'elenco di chiamate API da escludere dalla registrazione.                                                         |
|                     -ano [-]                      |                                                     Log (-ano) solo nomi di API o non registrare solo i nomi delle API (-ano).                                                     |
|                  -ricorsive [-]                   |                                          Log (-ricorsivo) o non registrare (-ricorsive) le API in modo ricorsivo oltre il primo livello.                                           |
|                   -exe <value>                   |                                                        Specifica il percorso completo di un file eseguibile per la traccia API.                                                        |

## <a name="remarks"></a>Note  
Dove [-] è elencato, un ulteriore - Nega l'opzione.  
## <a name="BKMK_examples"></a>Esempi  
Il comando seguente crea una traccia API contatore chiamata trace_notepad per il file eseguibile c:\Windows\Notepad.exe. e restituisce i risultati in c:\notepad.etl il file.  
```  
logman create api trace_notepad -exe c:\windows\notepad.exe -o c:\notepad.etl  
```  
Il comando seguente crea una traccia API contatore chiamata trace_notepad per c:\Windows\Notepad.exe. il file eseguibile la raccolta di valori prodotti da c:\windows\system32\advapi32.dll il modulo.  
```  
logman create api trace_notepad -exe c:\windows\notepad.exe -mods c:\windows\system32\advapi32.dll  
```  
Il comando seguente crea una traccia API contatore chiamata trace_notepad per c:\Windows\Notepad.exe. il file eseguibile escludendo la chiamata all'API TlsGetValue generati dal modulo Kernel32. dll.  
```  
logman create api trace_notepad -exe c:\windows\notepad.exe -exapis kernel32.dll!TlsGetValue  
```  
#### <a name="additional-references"></a>Riferimenti aggiuntivi  
[logman](logman.md)  
