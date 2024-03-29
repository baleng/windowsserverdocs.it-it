---
title: relog
description: Informazioni su come estrarre le informazioni sui contatori delle prestazioni dai file di log delle prestazioni di Coutner.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7480f6c0-9953-4d70-9b1c-b27e09d8db13
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: daedd85f1557c191a690e7eb750559cfd268d3a0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371619"
---
# <a name="relog"></a>relog

>Si applica a: Windows Server (canale semestrale), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Estrae i contatori delle prestazioni da registri contatori delle prestazioni in altri formati, ad esempio testo-TSV (per il testo delimitato da tabulazione), CSV (da testo delimitato da virgole), BIN binario o SQL.   

## <a name="syntax"></a>Sintassi  
```  
relog [<FileName> [<FileName> ...]] [/a] [/c <path> [<path> ...]] [/cf <FileName>] [/f  {bin|csv|tsv|SQL}] [/t <Value>] [/o {OutputFile|DSN!CounterLog}] [/b <M/D/YYYY> [[<HH>:] <MM>:] <SS>] [/e <M/D/YYYY> [[<HH>:] <MM>:] <SS>] [/config {<FileName>|i}] [/q]  
```  

### <a name="parameters"></a>Parametri  

|                                         Parametro                                          |                                                                                                                                                                  Descrizione                                                                                                                                                                   |
|--------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                *Nome del file* [ *... FileName*]                                 |                                                                                                                      Specifica il percorso di un log dei contatori delle prestazioni esistente. È possibile specificare più file di input.                                                                                                                      |
|                                             -a                                             |                                                                                                          Accoda output file anziché sovrascrivere. Questa opzione non è applicabile al formato SQL in cui il valore predefinito è sempre da accodare.                                                                                                           |
|                                   -c *percorso* [*percorso...* ]                                   |                                                       Specifica il percorso del contatore delle prestazioni da registrare. Per specificare più percorsi dei contatori, separarli con uno spazio e racchiuderli tra virgolette (ad esempio, **"** <em>Counterpath1</em> <em>Counterpath2</em> **"** )                                                       |
|                                       -CF *nomefile*                                       |                                            Specifica il percorso del file di testo in cui sono elencati i contatori delle prestazioni da includere in un file di relog. Utilizzare questa opzione per elencare i percorsi dei contatori in un file di input, uno per riga. Impostazione predefinita è che tutti i contatori nel file di registro originale vengano nuovamente registrati.                                            |
|                                  -f {bin @ no__t-0 CSV @ no__t-1tsv @ no__t-2Il programma}                                  |                                       Specifica il percorso del formato di file di output. Il formato predefinito è **bin**. Per un database SQL, specifica il file di output di *DSN! CounterLog*. È possibile specificare il percorso del database utilizzando la gestione di ODBC per configurare il DSN (Database System Name).                                        |
|                                         *valore* -t                                         |                                                                                                           Specifica gli intervalli di campionamento in "*N*" record. Include ogni punto dati ennesima nel file di relog. Valore predefinito è ogni punto dati.                                                                                                           |
| -o {*OutputFile* \| *"SQL: DSN! Counter_Log*} dove DSN è un DSN ODMC definito nel sistema. |                                                   Specifica il percorso del file di output o database SQL in cui verranno scritti i contatori. <br>Nota: Per le versioni a 64 bit e a 32 bit di relog. exe, è necessario definire un DSN nell'origine dati ODBC (rispettivamente 64-bit e 32-bit)                                                   |
|                          -b \<*M*/*D*/*aaaa*> [[*HH*:]*mm*:]*SS*                           |                                                                          Specifica ora di inizio della copia del primo record dal file di input. la data e l'ora devono essere in questo formato <em>M</em> **/** <em>D</em> **/** <em>YYYYHH</em> **:** <em>mm</em> **:** <em>ss</em>.                                                                          |
|                          -e \<*M*/*D*/*aaaa*> [[*HH*:]*mm*:]*SS*                           |                                                                           Specifica l'ora di fine per la copia dell'ultimo record dal file di input. la data e l'ora devono essere in questo formato <em>M</em> **/** <em>D</em> **/** <em>YYYYHH</em> **:** <em>mm</em> **:** <em>ss</em>.                                                                            |
|                                -config {*FileName* \| *i*}                                 | Specifica il percorso del file di impostazioni che contiene i parametri della riga di comando. Utilizzare *-i* nel file di configurazione come segnaposto per un elenco dei file di input che può essere inserito nella riga di comando. Nella riga di comando, tuttavia, non devi usare *è*. È anche possibile usare caratteri jolly, ad esempio \*. grosso, per specificare molti nomi di file di input. |
|                                             -q                                             |                                                                                                                          Consente di visualizzare i contatori delle prestazioni e gli intervalli di tempo dei file di log specificati nel file di input.                                                                                                                           |
|                                             -y                                             |                                                                                                                                            Ignora la richiesta rispondendo a "Sì" a tutte le domande.                                                                                                                                             |
|                                             /?                                             |                                                                                                                                                      Visualizza la guida al prompt dei comandi.                                                                                                                                                      |

## <a name="remarks"></a>Note  
Formato del percorso del contatore:  
- Il formato generale per i percorsi dei contatori è il seguente: [\\ @ no__t-1Computer >] \\ @ no__t-3Object > [\<Parent > \\ < Instance # index >] \\ @ no__t-7Counter >] in cui l'elemento padre, instance, index e Counter i componenti del formato possono contenere un nome valido o un carattere jolly. Il computer, padre, istanza e i componenti dell'indice non sono necessari per tutti i contatori.  
- Determinare i percorsi dei contatori da utilizzare in base al contatore stesso. Ad esempio, l'oggetto disco logico ha un'istanza <Index>, pertanto è necessario fornire < #index > o un carattere jolly. Pertanto, è possibile utilizzare il formato seguente: **\LogicalDisk (\* @ no__t-2 @ no__t-3 @ no__t-4 @ no__t-5) \\ @ no__t-7***  
- In confronto, l'oggetto processo non richiede un'istanza \<Index >. Pertanto, è possibile utilizzare il seguente formato: **\Processo (\*) \ID processo**  
- Se viene specificato un carattere jolly nel nome del padre, verranno restituite tutte le istanze dell'oggetto specificato che corrispondono ai campi del contatore e istanza specificata.  
- Se viene specificato un carattere jolly nel nome dell'istanza, tutte le istanze dell'oggetto specificato e oggetto padre verranno restituite se il carattere jolly corrispondano a tutti i nomi di istanza corrispondente all'indice specificato.  
- Se viene specificato un carattere jolly nel nome del contatore, vengono restituiti tutti i contatori dell'oggetto specificato.  
- Percorso stringa le corrispondenze parziali contatori (ad esempio, pro *) non sono supportate.  

File dei contatori:  
-   I file dei contatori sono file di testo in cui sono elencati uno o più dei contatori delle prestazioni nel registro esistente. Copiare il nome completo del contatore dal log o l'output **/q** in \<computer > \\ @ No__t-3Object > \\ @ No__t-5Instance > \\ @ No__t-7Counter > formato. elenca un percorso del contatore in ogni riga.  

Copia di contatori:  
-   Quando viene eseguito, **relog** Copia i contatori specificati da ogni record nel file di input, la conversione del formato, se necessario. Percorsi con caratteri jolly sono consentiti nel file del contatore.  
Salvataggio dei sottoinsiemi di file di input:  
-   Utilizzare il **/t** parametro per specificare i file di input vengono inseriti in file a intervalli di output ogni <n>record th. Per impostazione predefinita, sono registrati di nuovo dati da ogni record.  
Utilizzando **/b** e **/e** parametri con i file di log  
-   È possibile specificare che i log di output includono record da prima dell'ora di inizio (vale a dire **/b**) che fornisce dati per i contatori che richiedono valori di calcolo del valore formattato. Il file di output avrà gli ultimi record dai file di input con timestamp minore di **/e** (vale a dire, ora di fine) parametro.  
Utilizzo di **/config** opzione:  
-   Il contenuto del file di impostazioni utilizzato con il **/config** opzione deve essere nel formato seguente:  
    -   \<CommandOption > \\ @ no__t-2Value >, dove \<CommandOption > è un'opzione della riga di comando e \<Value > ne specifica il valore.

Per ulteriori informazioni sull'incorporamento di **relog** negli script Strumentazione gestione Windows (WMI), vedere l'argomento relativo alla creazione di script WMI nel [sito Web Microsoft Windows Resource Kit](https://go.microsoft.com/fwlink/?LinkId=4665).  

## <a name="BKMK_Examples"></a>Esempi  
Per ricampionare i registri di traccia esistenti a intervalli fissi di 30, elencare i percorsi dei contatori, file e formati di output:  
```  
relog c:\perflogs\daily_trace_log.blg /cf counter_file.txt /o c:\perflogs\reduced_log.csv /t 30 /f csv  
```  
Per ricampionare i registri di traccia esistenti a intervalli fissi di 30, elencare i percorsi dei contatori e i file di output:  
```  
relog c:\perflogs\daily_trace_log.blg /cf counter_file.txt /o c:\perflogs\reduced_log.blg /t 30  
```
Per ricampionare i log di traccia esistenti in un database, utilizzare:
```
relog "c:\perflogs\daily_trace_log.blg" -f sql -o "SQL:sql2016x64odbc!counter_log"
```

## <a name="additional-references"></a>Altri riferimenti  
-   [Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)  
