---
title: wbadmin avviare il backup
description: 'Argomento dei comandi di Windows per * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 56f3e752-d99a-4c3d-8e97-10303c37dd78
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c8eb017e8bf49191c33cd2d9f0cf4a62b08ebb07
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362337"
---
# <a name="wbadmin-start-backup"></a>wbadmin avviare il backup



Crea un backup utilizzando i parametri specificati. Se viene specificato alcun parametro e aver creato un backup giornaliero pianificato, il sottocomando crea il backup utilizzando le impostazioni per il backup pianificato. Se vengono specificati parametri, viene creato un backup di copia del servizio Copia Shadow del Volume (VSS) e non aggiornerà la cronologia dei file che vengono sottoposti a backup.

Per creare un backup unico con questo sottocomando, è necessario essere un membro del **gruppo Backup Operators** gruppo o **amministratori** gruppo, oppure è necessario che siano state delegate le autorizzazioni appropriate. Inoltre, è necessario eseguire **wbadmin** da un prompt dei comandi con privilegi elevati. (Per aprire un prompt dei comandi con privilegi elevati di rapida **Command prompt** e quindi fare clic su **Esegui come amministratore**.)

Per esempi di come utilizzare questo sottocomando, vedere [esempi](#BKMK_examples).

## <a name="syntax"></a>Sintassi

Sintassi per Windows ° Vista e Windows Server 2008:
```
wbadmin start backup
[-backupTarget:{<BackupTargetLocation> | <TargetNetworkShare>}]
[-include:<VolumesToInclude>]
[-allCritical]
[-noVerify]
[-user:<UserName>]
[-password:<Password>]
[-noinheritAcl]
[-vssFull]
[-quiet]
```
Sintassi per Windows ° 7 e Windows Server 2008 R2 e versioni successive:
```
Wbadmin start backup
[-backupTarget:{<BackupTargetLocation> | <TargetNetworkShare>}]
[-include:<ItemsToInclude>]
[-nonRecurseInclude:<ItemsToInclude>]
[-exclude:<ItemsToExclude>]
[-nonRecurseExclude:<ItemsToExclude>]
[-allCritical]
[-systemState]
[-noVerify]
[-user:<UserName>]
[-password:<Password>]
[-noInheritAcl]
[-vssFull | -vssCopy] 
[-quiet]
```

## <a name="parameters"></a>Parametri

|Parametro|Descrizione|
|---------|-----------|
|-backupTarget|Specifica il percorso di archiviazione per il backup. Richiede una lettera di unità disco rigido (f:), un percorso basato su GUID volume nel formato \\ @ no__t-1? \\Volume {GUID} o un percorso Universal Naming Convention (UNC) a una cartella condivisa remota (\\ @ no__t-4 @ no__t-5servername > \\ @ no__ t-7sharename > \\). Per impostazione predefinita, il backup verrà salvato in: \\ @ no__t-1 @ no__t-2servername > \\ @ no__t-4sharename > \\**WindowsImageBackup**\\ @ No__t-8ComputerBackedUp > \\.</br>Importante: Se si salva un backup in una cartella condivisa remota, il backup verrà sovrascritto se si utilizza la stessa cartella per eseguire nuovamente il backup dello stesso computer. Inoltre, se l'operazione di backup non riesce, potrebbe avere alcun backup perché il backup precedente verrà sovrascritto, mentre il backup più recente non sarà utilizzabile. Per evitare questo problema creando sottocartelle nella cartella condivisa remota per organizzare i backup. In questo caso, le sottocartelle saranno necessario il doppio dello spazio della cartella padre.|
|-includere|Per Windows ° Vista e Windows Server 2008, specifica l'elenco delimitato da virgole di lettere di unità del volume, punti di montaggio del volume o nomi di volumi basati su GUID da includere nel backup. Questo parametro deve essere utilizzato solo quando il **- backupTarget** parametro viene utilizzato.</br>Per Windows 7 e Windows Server 2008 R2 e versioni successive, specifica l'elenco delimitato da virgole di elementi da includere nel backup. È possibile includere più file, cartelle o volumi. È possibile specificare i percorsi dei volumi utilizzando lettere di unità dei volumi, punti di montaggio dei volumi o nomi dei volumi basati su GUID. Se si utilizza un nome di volume basato su GUID, deve terminare con una barra rovesciata (\\). È possibile utilizzare il carattere jolly (\*) nel nome del file quando si specifica un percorso di un file. Deve essere utilizzato solo quando il **- backupTarget** parametro viene utilizzato.|
|-escludere|Per Windows 7 e Windows Server 2008 R2 e versioni successive, specifica l'elenco delimitato da virgole di elementi da escludere dal backup. È possibile escludere i file, cartelle o volumi. È possibile specificare i percorsi dei volumi utilizzando lettere di unità dei volumi, punti di montaggio dei volumi o nomi dei volumi basati su GUID. Se si utilizza un nome di volume basato su GUID, deve terminare con una barra rovesciata (\\). È possibile utilizzare il carattere jolly (\*) nel nome del file quando si specifica un percorso di un file. Deve essere utilizzato solo quando il **- backupTarget** parametro viene utilizzato.|
|-nonRecurseInclude|Per Windows 7 e Windows Server 2008 R2 e versioni successive, specifica l'elenco di elementi non ricorsivi, delimitati da virgole da includere nel backup. È possibile includere più file, cartelle o volumi. È possibile specificare i percorsi dei volumi utilizzando lettere di unità dei volumi, punti di montaggio dei volumi o nomi dei volumi basati su GUID. Se si utilizza un nome di volume basato su GUID, deve terminare con una barra rovesciata (\\). È possibile utilizzare il carattere jolly (\*) nel nome del file quando si specifica un percorso di un file. Deve essere utilizzato solo quando il **- backupTarget** parametro viene utilizzato.|
|-nonRecurseExclude|Per Windows 7 e Windows Server 2008 R2 e versioni successive, specifica l'elenco di elementi non ricorsivi, delimitati da virgole da escludere dal backup. È possibile escludere i file, cartelle o volumi. È possibile specificare i percorsi dei volumi utilizzando lettere di unità dei volumi, punti di montaggio dei volumi o nomi dei volumi basati su GUID. Se si utilizza un nome di volume basato su GUID, deve terminare con una barra rovesciata (\\). È possibile utilizzare il carattere jolly (\*) nel nome del file quando si specifica un percorso di un file. Deve essere utilizzato solo quando il **- backupTarget** parametro viene utilizzato.|
|-allCritical|Specifica che tutti i volumi critici (volumi che contengono lo stato del sistema operativo) vengono inclusi nei backup. Questo parametro è utile se si sta creando una copia di backup per ripristino bare metal. Deve essere utilizzato solo quando **- backupTarget** è specificato, in caso contrario il comando avrà esito negativo. Può essere utilizzato con il **-includono** (opzione).</br>Suggerimento: Il volume di destinazione per un backup del volume critico può essere un'unità locale, ma non può essere uno dei volumi inclusi nel backup.|
|-systemState|Per Windows 7 e Windows Server 2008 R2 e versioni successive, in viene creato un backup che include lo stato del sistema, oltre a qualsiasi altro elemento specificato con il parametro **-include** . Lo stato del sistema contiene i file di avvio (Boot. ini, NDTLDR, NTDetect.com), il Registro di sistema di Windows comprese le impostazioni di COM, la cartella SYSVOL (criteri di gruppo e script di accesso), Active Directory e NTDS. DIT sui controller di dominio e, se è installato il servizio certificati, il certificato nell'archivio. Se il server è installato il ruolo di server Web, IIS Metadirectory sarà inclusa. Se il server è parte di un cluster, informazioni sul servizio Cluster verranno inoltre incluse.|
|-noVerify|Specifica che i backup salvati su supporti rimovibili (ad esempio un DVD) non vengono verificati gli errori. Se non si utilizza questo parametro, salvati su supporti rimovibili vengono verificati gli errori.|
|-utente|Se il backup viene salvato in una cartella condivisa remota, specifica il nome utente con autorizzazione di scrittura nella cartella.|
|-password|Specifica la password per il nome utente fornito dal parametro **-utente**.|
|-noInheritAcl|Applica le autorizzazioni dell'elenco di controllo di accesso (ACL) che corrispondono alle credenziali fornite dai parametri **-User** e **-password** a \\ @ no__t-3 @ no__t-4servername > \\ @ no__t-6sharename > @no__ t-7WindowsImageBackup @ no__t-8 @ no__t-9ComputerBackedUp > 0 (la cartella che contiene il backup). Per accedere ai backup in un secondo momento, è necessario utilizzare le credenziali o essere un membro del gruppo Administrators o del gruppo Backup Operators nel computer con la cartella condivisa. Se **-noInheritAcl** non viene utilizzato, per impostazione predefinita le autorizzazioni ACL dalla cartella condivisa remota vengono applicate alla cartella \\ @ No__t-2ComputerBackedUp >, in modo che chiunque disponga dell'accesso alla cartella condivisa remota possa accedere al backup.|
|-vssFull|Esegue un backup completo mediante il servizio Copia Shadow del Volume (VSS). Tutti i file di backup, la cronologia di ogni file viene aggiornata per indicare che è stato eseguito il backup e i registri di backup precedente possono essere troncati. Se questo parametro non viene utilizzato **wbadmin start backup** consente a un backup di copia, ma la cronologia dei file non viene eseguito il backup viene aggiornato.</br>Attenzione: Non utilizzare questo parametro se si utilizza un prodotto diverso da Windows Server Backup per eseguire il backup di applicazioni che si trovano sui volumi inclusi nel backup corrente. In questo modo, è possibile che si interrompa la creazione di backup incrementali, differenziali o di altro tipo, perché la cronologia su cui si basano per determinare la quantità di dati di cui eseguire il backup potrebbe non essere presente e potrebbe eseguire un backup completo inutilmente.|
|-vssCopy|Per Windows 7 e Windows Server 2008 R2 e versioni successive, esegue un backup di copia con VSS. Tutti i file vengono sottoposti a backup, ma la cronologia dei file da eseguire il backup non viene aggiornata in modo da conservare tutte le informazioni su quali file modificati, eliminati e così via, nonché qualsiasi file di log dell'applicazione. L'utilizzo di questo tipo di backup non influisce sulla sequenza dei backup incrementali e differenziali che potrebbero verificarsi indipendentemente dal backup di copia. Rappresenta il valore predefinito.</br>Avviso: Non è possibile usare un backup di copia per i backup incrementali o differenziali o i ripristini.|
|-quiet|Esegue il sottocomando senza alcuna richiesta visualizzata all'utente.|

## <a name="BKMK_examples"></a>Esempi

Negli esempi seguenti viene illustrato il modo in cui il comando **Wbadmin start backup** può essere utilizzato in diversi scenari di backup:

Scenario #1
- Creare un backup dei volumi e:, d: \\mountpoint e \\ @ no__t-2? \\Volume {cc566d14-4410-11d9-9d93-806e6f6e6963}
- Salvare il backup del volume f:
  ```
  wbadmin start backup -backupTarget:f: -include:e:,d:\mountpoint,\\?\Volume{cc566d14-44a0-11d9-9d93-806e6f6e6963}\
  ```
  Scenario 2 #
- Eseguire un backup unico di *f: \\folder1* e *h: \\folder2* nel volume *d:* .
- Eseguire il backup dello stato del sistema
- Eseguire il backup di copia in modo che il backup differenziale in genere pianificato non è interessato.
  ```
  wbadmin start backup –backupTarget:d: -include:g\folder1,h:\folder2 –systemstate -vsscopy
  ```
  Scenario 3 #
- Eseguire un backup unico di *d: \\folder1* di cui eseguire il backup in modo non ricorsivo.
- Eseguire il backup della cartella nel percorso di rete *\\ @ no__t-2backupshare @ no__t-3backup1*
- Limitare l'accesso per il backup per i membri del **amministratori** o **gruppo Backup Operators** gruppo.
  ```
  wbadmin start backup –backupTarget: \\backupshare\backup1 -noinheritacl -nonrecurseinclude:d:\folder1
  ```

#### <a name="additional-references"></a>Altri riferimenti

-   [Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
