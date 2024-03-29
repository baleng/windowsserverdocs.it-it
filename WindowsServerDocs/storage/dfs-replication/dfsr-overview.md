---
title: Panoramica di Replica DFS
ms.date: 03/08/2019
ms.prod: windows-server
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: eebce26eef6eceddc064e3bb179f268ccf47c93d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386065"
---
# <a name="dfs-replication-overview"></a>Panoramica di Replica DFS

> Si applica a: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows Server (canale semestrale)

Replica DFS è un servizio ruolo di Windows Server che consente di replicare in modo efficiente le cartelle (incluse quelle a cui fa riferimento un percorso dello spazio dei nomi DFS) in più server e siti. Replica DFS è un motore di replica multimaster efficace utilizzabile per mantenere sincronizzate le cartelle tra più server attraverso connessioni di rete con larghezza di banda limitata. Sostituisce il servizio Replica file (FRS) come motore di replica per gli spazi dei nomi DFS, nonché per la replica della cartella SYSVOL di Active Directory Domain Services (AD DS) in domini che utilizzano il livello di funzionalità del dominio Windows Server 2008 o versione successiva.

Replica DFS utilizza un algoritmo di compressione noto come RDC (Remote Differential Compression). La tecnologia RDC è in grado di rilevare le modifiche apportate ai dati di un file e consente a Replica DFS di replicare solo i blocchi di file modificati anziché l'intero file.

Per altre informazioni sulla replica di SYSVOL con Replica DFS, vedere [eseguire la migrazione della replica SYSVOL a replica DFS](migrate-sysvol-to-dfsr.md).

Per utilizzare Replica DFS, è necessario creare gruppi di replica e aggiungere cartelle replicate ai gruppi. I gruppi di replica, le cartelle replicate e i membri sono illustrati nella figura seguente.

![Gruppo di replica contenente una connessione tra due membri, ognuno con un paio di cartelle replicate](media/dfsr-overview.gif)

Questa figura mostra che un gruppo di replica è un set di server, noti come membri, che partecipa alla replica di una o più cartelle replicate. Una cartella replicata è una cartella che rimane sincronizzata in ogni membro. Nella figura sono presenti due cartelle replicate: Progetti e proposte. Quando i dati vengono modificati in ogni cartella replicata, le modifiche vengono replicate tra le connessioni tra i membri del gruppo di replica. Le connessioni tra tutti i membri formano la topologia di replica.
La creazione di più cartelle replicate in un singolo gruppo di replica semplifica il processo di distribuzione delle cartelle replicate, in quanto la limitazione della topologia, della pianificazione e della larghezza di banda per il gruppo di replica viene applicata a ogni cartella replicata. Per distribuire altre cartelle replicate, è possibile usare Dfsradmin. exe o seguire le istruzioni di una procedura guidata per definire il percorso locale e le autorizzazioni per la nuova cartella replicata.

Ogni cartella replicata dispone di impostazioni univoche, ad esempio filtri di file e sottocartelle, in modo che sia possibile filtrare file e sottocartelle diversi per ogni cartella replicata.

Le cartelle replicate archiviate in ogni membro possono trovarsi in volumi diversi del membro e le cartelle replicate non devono necessariamente essere cartelle condivise o parte di uno spazio dei nomi. Lo snap-in Gestione DFS, tuttavia, semplifica la condivisione delle cartelle replicate e, facoltativamente, la relativa pubblicazione in uno spazio dei nomi esistente.

È possibile amministrare Replica DFS tramite Gestione DFS, i comandi DfsrAdmin e Dfsrdiag o gli script che chiamano WMI.

## <a name="requirements"></a>Requisiti

Per poter distribuire Replica DFS, è prima necessario configurare i server nel modo seguente:

- Aggiornare lo schema di Active Directory Domain Services (AD DS) in modo da includere le aggiunte allo schema di Windows Server 2003 R2 o versioni successive. Non è possibile usare cartelle replicate di sola lettura con Windows Server 2003 R2 o aggiunte di schema obsolete.
- Verificare che tutti i server inclusi in un gruppo di replica si trovino nella stessa foresta. Non è possibile abilitare la replica tra server in foreste diverse.
- Installare Replica DFS in tutti i server che funzioneranno come membri di un gruppo di replica.
- Contattare il fornitore del software antivirus per verificare la compatibilità del software antivirus con Replica DFS.
- Individuare eventuali cartelle di cui si desidera eseguire la replica in volumi formattati con il file system NTFS. Replica DFS non supporta Resilient File System (ReFS) o il file system FAT. Replica DFS non supporta inoltre la replica di contenuto archiviato in volumi condivisi del cluster.

## <a name="interoperability-with-azure-virtual-machines"></a>Interoperabilità con macchine virtuali di Azure

L'uso di Replica DFS in una macchina virtuale in Azure è stato testato con Windows Server; Tuttavia, esistono alcune limitazioni e requisiti che è necessario seguire.

- Se si usano snapshot o stati salvati per ripristinare un server che esegue Replica DFS per la replica di qualsiasi elemento diverso dalla cartella SYSVOL, Replica DFS avrà esito negativo e saranno necessari passaggi speciali di ripristino del database. Allo stesso modo, non esportare, clonare o copiare le macchine virtuali. Per altre informazioni, vedere l'articolo [2517913](http://support.microsoft.com/kb/2517913) della Microsoft Knowledge Base e [Virtualizzazione sicura di DFSR](https://blogs.technet.microsoft.com/filecab/2013/04/05/safely-virtualizing-dfsr/).
- Quando si esegue il backup dei dati in una cartella replicata ospitata in una macchina virtuale, è necessario usare il software di backup della macchina virtuale guest.
- Replica DFS richiede l'accesso ai controller di dominio fisici o virtualizzati, non è in grado di comunicare direttamente con Azure AD.
- Replica DFS richiede una connessione VPN tra i membri del gruppo di replica locale e i membri ospitati nelle macchine virtuali di Azure. È anche necessario configurare il router locale (ad esempio, Forefront Threat Management Gateway) per consentire all'Agente mapping endpoint RPC (porta 135) e a una porta assegnata casualmente compresa tra 49152 e 65535 di saltare la connessione VPN. È possibile usare il cmdlet Set-DfsrMachineConfiguration o lo strumento da riga di comando Dfsrdiag per specificare una porta statica invece della porta casuale. Per altre informazioni su come specificare una porta statica per Replica DFS, vedere [Set-DfsrServiceConfiguration](https://docs.microsoft.com/powershell/module/dfsr/set-dfsrserviceconfiguration). Per informazioni sulle porte correlate da aprire per gestire Windows Server, vedere l'articolo [832017](http://support.microsoft.com/kb/832017) della Microsoft Knowledge Base.

Per altre informazioni introduttive sulle macchine virtuali di Azure, visitare il [sito Web di Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/).

## <a name="installing-dfs-replication"></a>Installazione di Replica DFS

Replica DFS fa parte del ruolo Servizi file e archiviazione. Gli strumenti di gestione per DFS (Gestione DFS, il modulo Replica DFS per Windows PowerShell e gli strumenti da riga di comando) vengono installati separatamente come parte del Strumenti di amministrazione remota del server.

Installare Replica DFS usando l'interfaccia di [amministrazione di Windows](../../manage/windows-admin-center/understand/windows-admin-center.md), Server Manager o PowerShell, come descritto nelle sezioni successive.

### <a name="to-install-dfs-by-using-server-manager"></a>Per installare il file system DFS tramite Server Manager

1. Aprire Server Manager, fare clic su **Gestione** e quindi su **Aggiungi ruoli e funzionalità**. Verrà visualizzata l'Aggiunta guidata ruoli e funzionalità.

2. Nella pagina **Selezione dei server** selezionare il server o il disco rigido virtuale (VHD) di una macchina virtuale offline in cui si desidera installare il file system DFS.

3. Selezionare i servizi ruolo e le funzionalità che si desidera installare.

    - Per installare il servizio Replica DFS, nella pagina **ruoli server** selezionare **replica DFS**.

    - Per installare solo gli Strumenti di gestione DFS, nella pagina **Funzionalità** espandere **Strumenti di amministrazione remota del server**, **Strumenti di amministrazione ruoli**, **Strumenti per Servizi file** e quindi selezionare **Strumenti di gestione DFS**.

         Con gli **strumenti di gestione DFS** vengono installati lo snap-in Gestione DFS, i moduli replica DFS e spazi dei nomi DFS per Windows PowerShell e gli strumenti da riga di comando, ma non viene installato alcun servizio DFS nel server.

### <a name="to-install-dfs-replication-by-using-windows-powershell"></a>Per installare Replica DFS tramite Windows PowerShell

Aprire una sessione di Windows PowerShell con diritti utente elevati, quindi digitare il comando seguente, dove < nome\> è il servizio ruolo o la funzionalità che si desidera installare (vedere la tabella seguente per un elenco di nomi di servizi ruolo o funzionalità rilevanti):

```PowerShell
Install-WindowsFeature <name>
```

|Servizio ruolo o funzionalità|Nome|
|---|---|
|Replica DFS|`FS-DFS-Replication`|
|Strumenti di gestione DFS|`RSAT-DFS-Mgmt-Con`|

Per installare, ad esempio, il componente Strumenti per File system distribuito (DFS) della funzionalità Strumenti di amministrazione remota del server, digitare:

```PowerShell
Install-WindowsFeature "RSAT-DFS-Mgmt-Con"
```

Per installare il Replica DFS e le parti degli strumenti file system distribuito della funzionalità Strumenti di amministrazione remota del server, digitare:

```PowerShell
Install-WindowsFeature "FS-DFS-Replication", "RSAT-DFS-Mgmt-Con"
```

## <a name="see-also"></a>Vedere anche

- [Panoramica di spazi dei nomi DFS e Replica DFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj127250(v%3dws.11))
- [Elenco di controllo: Distribuisci Replica DFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772201(v%3dws.11))
- [Elenco di controllo: Gestisci Replica DFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc755035(v%3dws.11))
- [Distribuzione di Replica DFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770925(v%3dws.11))
- [Gestione di Replica DFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770925(v%3dws.11))
- [Risoluzione dei problemi Replica DFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732802(v%3dws.11))
