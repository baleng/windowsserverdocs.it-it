---
title: Replica di archiviazione da cluster a cluster
ms.prod: windows-server-threshold
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
ms.assetid: 834e8542-a67a-4ba0-9841-8a57727ef876
author: nedpyle
ms.date: 04/26/2019
description: Come usare la Replica di archiviazione per replicare i volumi in un unico cluster a un altro cluster che esegue Windows Server.
ms.openlocfilehash: 9d4b7eb05576095abd5d8c905211b2a5e88555bd
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447628"
---
# <a name="cluster-to-cluster-storage-replication"></a>Replica di archiviazione da cluster a cluster

> Si applica a: Windows Server 2019, Windows Server 2016, Windows Server (canale semestrale)

Replica archiviazione consente di replicare volumi tra i cluster, inclusa la replica di cluster con spazi di archiviazione diretta. La gestione e la configurazione sono simili alla replica da server a server.  

I computer e l'archiviazione vengono configurati in una configurazione da cluster a cluster, in cui un cluster replica il proprio set di risorse di archiviazione con un altro cluster e la relativa serie di risorse di archiviazione. Questi nodi e la relativa archiviazione devono trovarsi in siti fisici separati, anche se non è obbligatorio.  

> [!IMPORTANT]
> In questo test, i quattro server sono un esempio. È possibile usare qualsiasi numero di server supportato da Microsoft in ogni cluster, che attualmente corrisponde a 8 per un cluster di spazi di archiviazione diretta e 64 per un cluster di archiviazione condivisa.  
>   
> Questa Guida non illustra la configurazione di Spazi di archiviazione diretta. Per informazioni sulla configurazione di spazi di archiviazione diretta, vedere [Panoramica di spazi di archiviazione diretta](../storage-spaces/storage-spaces-direct-overview.md).  

Questa procedura dettagliata usa l'ambiente seguente come esempio:  

-   Due server membri, denominati **SR-SRV01** e **SR-SRV02** successivamente trasformati in un cluster denominato **SR-SRVCLUSA**.  

-   Due server membri, denominati **SR-SRV03** e **SR-SRV04** successivamente trasformati in un cluster denominato **SR-SRVCLUSB**.  

-   Una coppia di "siti" logici che rappresentano due centri dati diversi, uno chiamato **Redmond** e l'altro **Bellevue**.  

![Diagramma che mostra un ambiente di esempio con un cluster nel sito Redmond in replica con un cluster nel sito Bellevue](./media/Cluster-to-Cluster-Storage-Replication/SR_ClustertoCluster.png)  

**FIGURA 1: Cluster a cluster di replica**  

## <a name="prerequisites"></a>Prerequisiti  

* Foresta di Active Directory Domain Services (non è necessario eseguire Windows Server 2016).  
* 4-128 server (due cluster di server 2-64) che esegue Windows Server 2016, Datacenter Edition o Windows Server 2019. Se si esegue Windows Server 2019, è possibile invece usare Standard Edition se si replicano bene solo un singolo volume fino a 2 TB di dimensioni.  
* Due set di risorse di archiviazione che usano JBOD SAS, SAN Fibre Channel, VHDX condiviso, Spazi di archiviazione diretta o destinazione iSCSI. L'archivio deve contenere una combinazione di supporti SSD e HDD. Ogni set di risorse di archiviazione verrà resa disponibile a un solo cluster senza accesso condiviso tra i cluster.  
* Ogni set di risorse di archiviazione deve consentire la creazione di almeno due dischi virtuali, uno per i dati replicati e uno per i registri. L'archiviazione fisica deve avere le stesse dimensioni di settore su tutti i dischi di dati. L'archiviazione fisica deve avere le stesse dimensioni di settore su tutti i dischi dei registri.  
* Almeno una connessione Ethernet/TCP su ogni server per la replica sincrona, ma preferibilmente RDMA.   
* Regole firewall e router appropriate per consentire ICMP, SMP (porta 445 più 5445 per SMB diretto) e traffico bidirezionale WS-MAN (porta 5985) tra tutti i nodi.  
* Una rete tra i server con larghezza di banda sufficiente per contenere il carico di lavoro di scrittura delle operazioni di I/O e una latenza media di andata e ritorno di =5 ms, per la replica sincrona. La replica asincrona non dispone di un'indicazione di latenza.  
* L'archiviazione replicata non può trovarsi nell'unità che contiene la cartella del sistema operativo Windows.
* Esistono importanti considerazioni e limitazioni per la replica di tipo spazi di archiviazione diretta, vedere le informazioni dettagliate seguenti.

Molti di questi requisiti possono essere determinati usando il cmdlet `Test-SRTopology`. Se si installano le funzionalità Replica archiviazione o Strumenti di gestione di Replica archiviazione in almeno un server è possibile accedere a questo strumento. Non è necessario configurare Replica archiviazione perché usi questo strumento, ma è necessario installare il cmdlet. Altre informazioni sono incluse nei passaggi seguenti.  

## <a name="step-1-provision-operating-system-features-roles-storage-and-network"></a>Passaggio 1: Effettuare il provisioning di sistema operativo, funzionalità, ruoli, archiviazione e rete

1.  Installare Windows Server in tutti i quattro nodi del server con un tipo di installazione di Windows Server **(esperienza Desktop)** . 

2.  Aggiungere informazioni di rete e unirle al dominio, quindi riavviarli.  

    > [!IMPORTANT]  
    > Da questo momento, accedere sempre a tutti i server come utente di dominio, ovvero un membro del gruppo amministratore incorporato. Ricordarsi di elevare i prompt di Windows PowerShell e CMD futuro durante l'esecuzione in un'installazione server con interfaccia grafica o in un computer Windows 10.  

3.  Collegare il primo set di alloggiamenti di archiviazione JBOD, la destinazione iSCSI, SAN FC o l'archiviazione su disco a dimensione fissa locale (DAS) server nel sito **Redmond**.  

4.  Collegare il secondo set di risorse di archiviazione al server nel sito **Bellevue**.  

5.  Se necessario, installare il sistema di archiviazione del fornitore e il firmware dell'enclosure più recente, i driver HBA del fornitore più recenti, i firmware BIOS o UEFI del fornitore più recenti, i driver di rete del fornitore più recenti e driver dei chipset della scheda madre più recenti in tutti e quattro i nodi. Se necessario riavviare i nodi.  

    > [!NOTE]  
    > Per la configurazione dell'archiviazione condivisa e dell'hardware di rete, consultare la documentazione del fornitore hardware.  

6.  Assicurarsi che le impostazioni BIOS/UEFI dei server abilitati consentano alte prestazioni, ad esempio la disabilitazione dei C-State, l'impostazione della velocità QPI, l'abilitazione di NUMA e l'impostazione della frequenza di memoria massima. Assicurarsi che il risparmio energia in Windows Server sia impostato su prestazioni elevate. Riavviare se necessario.  

7.  Configurare i ruoli come indicato di seguito:  

    -   **Metodo grafico**  

        1.  Eseguire **ServerManager.exe** e creare un gruppo di server aggiungendo tutti i nodi del server.  

        2.  Installare i ruoli e le funzionalità **File Server** e **Replica archiviazione** in ciascuno dei nodi e riavviarli.  

    -   **Metodo Windows PowerShell**  

        In un computer di gestione remota o SR-SRV04, eseguire il comando seguente nella console di Windows PowerShell per installare i ruoli e le funzionalità necessarie per un cluster esteso sui quattro nodi e riavviarli:  

        ```PowerShell
        $Servers = 'SR-SRV01','SR-SRV02','SR-SRV03','SR-SRV04'  

        $Servers | ForEach { Install-WindowsFeature -ComputerName $_ -Name Storage-Replica,Failover-Clustering,FS-FileServer -IncludeManagementTools -restart }  
        ```  

        Per altre informazioni su questi passaggi, vedere [Installazione o disinstallazione di ruoli, servizi ruolo o funzionalità](../../administration/server-manager/install-or-uninstall-roles-role-services-or-features.md)  

9. Configurare lo spazio di archiviazione come indicato di seguito:  

    > [!IMPORTANT]  
    > -   È necessario creare due volumi in ciascuna enclosure: uno per i dati e uno per i registri.  
    > -   I dischi di dati e registro devono essere inizializzati come **GPT**, non come **MBR**.  
    > -   I due volumi di dati devono avere le stesse dimensioni.  
    > -   I due volumi di registro devono avere le stesse dimensioni.  
    > -   Tutti i dischi di dati replicati devono avere le stesse dimensioni del settore.  
    > -   Tutti i dischi di registro devono avere le stesse dimensioni del settore.  
    > -   I volumi di registro devono usare un'archiviazione basata su flash, ad esempio le unità SSD.  Microsoft consiglia una velocità di archiviazione dei log superiore a quella dell'archiviazione dei dati. I volumi di log non devono essere utilizzati per altri carichi di lavoro.
    > -   I dischi di dati possono usare HDD, SSD o una combinazione a più livelli e spazi con mirroring o di parità o RAID 1 o 10, oppure RAID 5 o RAID 50.  
    > -   Il volume di log deve essere almeno 8GB per impostazione predefinita e può essere maggiore o inferiore in base ai requisiti del log.
    > -   Quando si usa spazi di archiviazione diretta (spazi di archiviazione diretta) con una cache NVME o unità SSD, viene visualizzato un maggiore rispetto a un aumento previsto della latenza durante la configurazione di replica di archiviazione tra cluster di spazi di archiviazione diretta. La modifica della latenza è proporzionalmente molto maggiore rispetto a viene visualizzato quando si usa unità SSD e NVME in delle prestazioni + configurazione della capacità e nessun livello HDD né a livelli di capacità.

    Questo problema si verifica a causa delle limitazioni dell'architettura all'interno di meccanismo di log del SR combinati con latenza estremamente bassa di NVME rispetto alla media più lento. Quando si usa cache di archiviazione spazi diretti spazi di archiviazione diretta, tutti i log dei / o di SR, insieme a tutti i recenti lettura/scrittura i/o delle applicazioni, verranno eseguita nella cache e mai sui livelli di prestazioni o la capacità. Ciò significa che tutte le attività di SR accade lo stesso supporto di velocità, questa configurazione non è supportata non consigliato (vedere https://aka.ms/srfaq per indicazioni per il log). 

    Quando si usa spazi di archiviazione diretta con unità disco rigido, non è possibile disattivare o evitare la cache. In alternativa, se si usa solo unità SSD e NVME, è possibile configurare solo i livelli di capacità e prestazioni. Se si usa la configurazione e inserendo i log di SR nel livello di prestazioni solo con i volumi di dati che si trova in solo il livello di capacità del servizio, si eviterà il problema ad alta latenza descritto in precedenza. È possibile eseguirla con una combinazione di unità SSD più veloce e più lento e nessun NVME.

    Questa soluzione non è ovviamente ideale e potrebbero non essere in grado di eseguire alcuni clienti di usarla. Il team SR sta lavorando meccanismo log aggiornato per il futuro per ridurre i colli di bottiglia artificiali che si verificano e ottimizzazioni. Non vi è alcun tempo Stimato per questo, ma quando è disponibile a toccare i clienti per il test, le domande frequenti verranno aggiornata. 

-   **Per le enclosure JBOD:**  

1. Assicurarsi che ogni cluster sia in grado di visualizzare solo gli alloggiamenti di archiviazione del sito e che le connessioni SAS siano configurate correttamente.  

2. Effettuare il provisioning dell'archiviazione mediante Spazi di archiviazione seguendo i **passaggi 1-3** indicati in [Distribuire Spazi di archiviazione in un server autonomo](../storage-spaces/deploy-standalone-storage-spaces.md) usando Windows PowerShell o Server Manager.  

-   **Per archiviazione di destinazione iSCSI:**  

1. Assicurarsi che ogni cluster possa visualizzare solo gli alloggiamenti di archiviazione di tale sito. Se si usa iSCSI, è necessario usare più di una singola scheda di rete.  

2. Effettua il provisioning dell'archiviazione usando la documentazione del fornitore. Se si usa la destinazione iSCSI basata su Windows, consultare [iSCSI Target Block Storage, How To](../iscsi/iscsi-target-server.md) (Procedura per l'archiviazione a blocchi nella destinazione iSCSI).  

-   **Per l'archiviazione FC SAN:**  

1. Assicurarsi che ogni cluster sia in grado di vedere solo gli alloggiamenti di archiviazione di tale sito e che gli host siano stati suddivisi correttamente in zone.  

2. Effettua il provisioning dell'archiviazione usando la documentazione del fornitore.  

-   **Spazi di archiviazione diretta:**  

1. Assicurarsi che ogni cluster possa visualizzare solo l'enclosure di archiviazione del sito tramite la distribuzione di Spazi di archiviazione diretta. (https://docs.microsoft.com/windows-server/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct) 

2. Assicurarsi che i volumi di log di Replica archiviazione siano presenti sempre sulla risorsa di archiviazione flash più veloce e che i volumi di dati lo siano sulla risorsa di archiviazione ad alta capacità più lenta.

3. Avviare Windows PowerShell e usare il cmdlet `Test-SRTopology` per determinare se siano stati soddisfatti tutti i requisiti di Replica archiviazione. È possibile usare il cmdlet in modalità dedicata ai requisiti per un rapido test, oppure in modalità di valutazione delle prestazioni a esecuzione prolungata.  
   Ad esempio,  

   ```PowerShell
   MD c:\temp

   Test-SRTopology -SourceComputerName SR-SRV01 -SourceVolumeName f: -SourceLogVolumeName g: -DestinationComputerName SR-SRV03 -DestinationVolumeName f: -DestinationLogVolumeName g: -DurationInMinutes 30 -ResultPath c:\temp        
   ```

     > [!IMPORTANT]
     > Quando si usa un server di prova privo di carichi di operazioni I/O di scrittura nel volume di origine specificato durante il periodo di valutazione, considerare l'aggiunta di un carico di lavoro o non verrà generato un report utile. È necessario eseguire il test con carichi di lavoro simili alla produzione per poter visualizzare i numeri reali e le dimensioni consigliate del registro. In alternativa, è sufficiente copiare alcuni file nel volume di origine durante il test o scaricare ed eseguire [DISKSPD](https://gallery.technet.microsoft.com/DiskSpd-a-robust-storage-6cd2f223) per generare operazioni di I/O di scrittura. Ad esempio, un campione con un carico di lavoro di I/O di scrittura basso per cinque minuti per il volume D: :  
     > `Diskspd.exe -c1g -d300 -W5 -C5 -b8k -t2 -o2 -r -w5 -h d:\test.dat`  

4. Esaminare il report **TestSrTopologyReport.html** per verificare che siano soddisfatti i requisiti di Replica archiviazione.  

   ![Schermata che mostra i risultati del report della topologia di replica](./media/Cluster-to-Cluster-Storage-Replication/SRTestSRTopologyReport.png)      

## <a name="step-2-configure-two-scale-out-file-server-failover-clusters"></a>Passaggio 2: Configurare due cluster di failover con un file server di scalabilità orizzontale  
Ora verranno creati due cluster di failover normale. Dopo la configurazione, la convalida e la fase di test, i cluster verranno replicati usando Replica archiviazione. È possibile eseguire tutti i passaggi seguenti nei nodi del cluster direttamente o da un computer di gestione remota che contiene strumenti di amministrazione di Windows Server Remote Server.  

### <a name="graphical-method"></a>Metodo grafico  

1.  Eseguire **cluadmin.msc** per un nodo in ogni sito.  

2.  Convalidare il cluster proposto e analizzare i risultati per assicurarsi di poter continuare. Nell'esempio vengono usati **SR-SRVCLUSA** e **SR-SRVCLUSB**.  

3.  Creare i due cluster. Verificare che il nome del cluster non superi i 15 caratteri di lunghezza.  

4.  Configurare un controllo di condivisione file o cloud.  

    > [!NOTE]  
    > WIndows Server include ora un'opzione per Cloud di Azure-controllo basato su. È possibile scegliere questa opzione di quorum anziché il controllo di condivisione file.  

    > [!WARNING]  
    > Per altre informazioni sulla configurazione del quorum, vedere la **configurazione del controllo** sezione [Configura e Gestisci Quorum](../../failover-clustering/manage-cluster-quorum.md). Per altre informazioni sul cmdlet `Set-ClusterQuorum`, vedere [Set-ClusterQuorum](https://docs.microsoft.com/powershell/module/failoverclusters/set-clusterquorum).  

5.  Aggiungere un disco al cluster CSV nel sito **Redmond**. A tale scopo, fare clic con il pulsante destro del mouse su un disco di origine nel nodo **Dischi** della sezione **Archiviazione**, e quindi fare clic su **Aggiungi a volumi condivisi cluster**.  

6.  Creare i file server in cluster con scalabilità orizzontale in entrambi i cluster seguendo le istruzioni della sezione [Configurare il file server di scalabilità orizzontale](https://technet.microsoft.com/library/hh831718.aspx)  

### <a name="windows-powershell-method"></a>Metodo Windows PowerShell  

1.  Testare il cluster proposto e analizzare i risultati per assicurarsi di poter continuare:  

    ```PowerShell
    Test-Cluster SR-SRV01,SR-SRV02  
    Test-Cluster SR-SRV03,SR-SRV04  
    ```  

2.  Creare i cluster (è necessario specificare i propri indirizzi IP statici per i cluster). Assicurarsi che il nome di ogni cluster non superi i 15 caratteri di lunghezza:  

    ```PowerShell
    New-Cluster -Name SR-SRVCLUSA -Node SR-SRV01,SR-SRV02 -StaticAddress <your IP here>  
    New-Cluster -Name SR-SRVCLUSB -Node SR-SRV03,SR-SRV04 -StaticAddress <your IP here>  
    ```  

3.  Configurare un controllo di condivisione file o un controllo cloud (Azure) in ogni cluster che punta a una condivisione ospitata nel controller di dominio o un altro server indipendente. Ad esempio:  

    ```PowerShell  
    Set-ClusterQuorum -FileShareWitness \\someserver\someshare  
    ```  

    > [!NOTE]  
    > WIndows Server include ora un'opzione per Cloud di Azure-controllo basato su. È possibile scegliere questa opzione di quorum anziché il controllo di condivisione file.  

    > [!WARNING]  
    > Per altre informazioni sulla configurazione del quorum, vedere la **configurazione del controllo** sezione [Configura e Gestisci Quorum](../../failover-clustering/manage-cluster-quorum.md). Per altre informazioni sul cmdlet `Set-ClusterQuorum`, vedere [Set-ClusterQuorum](https://docs.microsoft.com/powershell/module/failoverclusters/set-clusterquorum).  

4.  Creare i file server in cluster con scalabilità orizzontale in entrambi i cluster seguendo le istruzioni della sezione [Configurare il file server di scalabilità orizzontale](https://technet.microsoft.com/library/hh831718.aspx)  

## <a name="step-3-set-up-cluster-to-cluster-replication-using-windows-powershell"></a>Passaggio 3: Configurare la replica da Cluster a Cluster con Windows PowerShell  
Ora la replica da cluster a cluster verrà configurata usando Windows PowerShell. È possibile eseguire tutti i passaggi seguenti sui nodi direttamente o da un computer di gestione remota che contiene strumenti di amministrazione di Windows Server remoto Server  

1. Concedere l'accesso completo prima al cluster a altro cluster eseguendo il **Concedi SRAccess** cmdlet su un nodo qualsiasi del primo cluster, o in remoto.  Strumenti di amministrazione remota del Server di Windows Server

   ```PowerShell
   Grant-SRAccess -ComputerName SR-SRV01 -Cluster SR-SRVCLUSB  
   ```  

2. Concedere l'accesso completo al cluster secondo a altro cluster eseguendo il **Concedi SRAccess** cmdlet su qualsiasi nodo nel cluster secondo, o in remoto.  

   ```PowerShell
   Grant-SRAccess -ComputerName SR-SRV03 -Cluster SR-SRVCLUSA  
   ```  

3. Configurare la replica da cluster a cluster, specificando i dischi di origine e di destinazione, i registri di origine e di destinazione, i nomi dei cluster di origine e di destinazione e le dimensioni del registro. È possibile eseguire questo comando in locale nel server o usando un computer di gestione remota.  

   ```powershell  
   New-SRPartnership -SourceComputerName SR-SRVCLUSA -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\Volume2 -SourceLogVolumeName f: -DestinationComputerName SR-SRVCLUSB -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\Volume2 -DestinationLogVolumeName f:  
   ```  

   > [!WARNING]  
   > La dimensione predefinita del registro è 8 GB. In base ai risultati del cmdlet **Test-SRTopology**, è possibile decidere di usare **-LogSizeInBytes** con un valore superiore o inferiore.  

4. Per ottenere lo stato di origine e destinazione della replica, usare **Get-SRGroup** e **Get-SRPartnership** come indicato di seguito:  

   ```powershell
   Get-SRGroup  
   Get-SRPartnership  
   (Get-SRGroup).replicas  
   ```  

5. Determinare lo stato della replica come indicato di seguito:  

   1.  Nel server di origine eseguire il comando seguente, quindi esaminare gli eventi 5015, 5002, 5004, 1237, 5001 e 2200:
        
       ```PowerShell
       Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica -max 20
       ```
   2.  Nel server di destinazione, eseguire il comando seguente per visualizzare gli eventi di Replica archiviazione che mostrano la creazione della relazione. Questo evento indica il numero di byte copiati e il tempo impiegato. Esempio:  
        
       ```powershell
       Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | Where-Object {$_.ID -eq "1215"} | Format-List
       ```
       Ecco un esempio di output:
        
       ```
       TimeCreated  : 4/8/2016 4:12:37 PM  
       ProviderName : Microsoft-Windows-StorageReplica  
       Id           : 1215  
       Message      : Block copy completed for replica.  
           ReplicationGroupName: rg02  
           ReplicationGroupId:  
           {616F1E00-5A68-4447-830F-B0B0EFBD359C}  
           ReplicaName: f:\  
           ReplicaId: {00000000-0000-0000-0000-000000000000}  
           End LSN in bitmap:  
           LogGeneration: {00000000-0000-0000-0000-000000000000}  
           LogFileId: 0  
           CLSFLsn: 0xFFFFFFFF  
           Number of Bytes Recovered: 68583161856  
           Elapsed Time (seconds): 117  
       ```
   3. In alternativa, il gruppo del server di destinazione per la replica indica in qualsiasi momento il numero di byte rimanenti da copiare, inoltre è possibile eseguire query tramite PowerShell. Ad esempio:

      ```PowerShell
      (Get-SRGroup).Replicas | Select-Object numofbytesremaining
      ```

      Come esempio dello stato di avanzamento (che non terminerà):  

      ```PowerShell
        while($true) {  
        $v = (Get-SRGroup -Name "Replication 2").replicas | Select-Object numofbytesremaining  
        [System.Console]::Write("Number of bytes remaining: {0}`n", $v.numofbytesremaining)  
        Start-Sleep -s 5  
       }
       ```

6. Nel server di destinazione del cluster di destinazione eseguire il comando seguente ed esaminare gli eventi 5009, 1237, 5001, 5015, 5005 e 2200 per comprendere lo stato di avanzamento dell'elaborazione. Non dovrebbe essere presente alcun avviso di errori in questa sequenza. Ci saranno molti eventi 1237, perché questi indicano lo stato di avanzamento.  
    
   ```PowerShell
   Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | FL  
   ```
   > [!NOTE]
   > Il disco del cluster di destinazione verrà sempre visualizzato come **Online (Nessun accesso)** quando viene replicato.  

## <a name="step-4-manage-replication"></a>Passaggio 4: Gestire la replica

Ora è possibile usare e gestire la replica da cluster a cluster. È possibile eseguire tutti i passaggi seguenti nei nodi del cluster direttamente o da un computer di gestione remota che contiene strumenti di amministrazione di Windows Server Remote Server.  

1.  Usare **Get-ClusterGroup** o **Gestione cluster di failover** per determinare l'origine e la destinazione di replica attuale e il relativo stato.  Strumenti di amministrazione remota del Server di Windows Server

2.  Per misurare le prestazioni della replica, usare il cmdlet **Get-Counter** nei nodi di origine e di destinazione. I nomi dei contatori sono:  

    -   \Statistiche I/O partizione Replica archiviazione(*)\Numero di sospensioni scaricamento  

    -   \Statistiche I/O partizione Replica archiviazione(*)\Numero di I/O in attesa di scaricamento  

    -   \Statistiche I/O partizione Replica archiviazione(*)\Numero richieste ultima scrittura log  

    -   \Statistiche I/O partizione Replica archiviazione(*)\ Lunghezza media coda scaricamento  

    -   \Statistiche I/O partizione Replica archiviazione(*)\Lunghezza coda scaricamento corrente  

    -   \Statistiche I/O partizione Replica archiviazione(*)\Numero richieste scrittura applicazione  

    -   \Statistiche I/O partizione Replica archiviazione(*)\ Numero medio di richieste per scrittura di log  

    -   \Statistiche I/O partizione Replica archiviazione(*)\ Latenza media scrittura app  

    -   \Statistiche I/O partizione Replica archiviazione(*)\ Latenza media lettura app  

    -   \Statistiche Replica archiviazione(*)\RPO destinazione  

    -   \Statistiche Replica archiviazione(*)\RPO corrente  

    -   \Statistiche Replica archiviazione(*)\ Lunghezza media coda log  

    -   \Statistiche Replica archiviazione(*)\Lunghezza coda log corrente  

    -   \Statistiche Replica archiviazione(*)\Totale byte ricevuti  

    -   \Statistiche Replica archiviazione(*)\Totale byte inviati  

    -   \Statistiche Replica archiviazione(*)\ Latenza media invio rete  

    -   \Statistiche Replica archiviazione(*)\Stato replica  

    -   \Statistiche Replica archiviazione(*)\ Latenza media round trip messaggio  

    -   \Statistiche Replica archiviazione\Tempo trascorso ultimo ripristino  

    -   \Statistiche Replica archiviazione(*)\Numero di transazioni di ripristino scaricate  

    -   \Statistiche Replica archiviazione(*)\Numero di transazioni di ripristino  

    -   \Statistiche Replica archiviazione(*)\Numero di transazioni di replica scaricate  

    -   \Statistiche Replica archiviazione(*)\Numero di transazioni di replica  

    -   \Statistiche Replica archiviazione(*)\Quantità massima di numeri di sequenza del file di log  

    -   \Statistiche Replica archiviazione(*)\Numero di messaggi ricevuti  

    -   \Statistiche Replica archiviazione(*)\Numero di messaggi inviati  

    Per altre informazioni sui contatori delle prestazioni in Windows PowerShell, vedere [Get-Counter](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Diagnostics/Get-Counter).  

3.  Per spostare la direzione di replica da un sito, usare il cmdlet **Set-SRPartnership**.  

    ```PowerShell
    Set-SRPartnership -NewSourceComputerName SR-SRVCLUSB -SourceRGName rg02 -DestinationComputerName SR-SRVCLUSA -DestinationRGName rg01  
    ```  

    > [!NOTE]  
    > Windows Server impedisce il cambio di ruolo durante la sincronizzazione iniziale, perché può causare la perdita di dati se si tenta di cambio prima del completamento della replica iniziale. Non forzare il cambio delle direzioni fino al completamento della sincronizzazione iniziale.

    Controllare i registri eventi per visualizzare la direzione della modalità di modifica e ripristino della replica e quindi risolvere le differenze. Le operazioni di I/O di scrittura possono essere effettuate nell'archiviazione di proprietà nel nuovo server di origine. La modifica la direzione di replica blocca le operazioni di I/O di scrittura nel computer di origine precedente.  

    > [!NOTE]  
    > Il disco del cluster di destinazione verrà sempre visualizzato come **Online (Nessun accesso)** quando viene replicato.  

4.  Per modificare le dimensioni del log da 8GB predefiniti, usare **Set-SRGroup** in gruppi di Replica di archiviazione di origine e di destinazione.  

    > [!IMPORTANT]  
    > La dimensione predefinita del registro è 8 GB. In base ai risultati del cmdlet **Test-SRTopology**, è possibile decidere di usare -LogSizeInBytes con un valore superiore o inferiore.  

5.  Per rimuovere la replica, usare **Get-SRGroup**, **Get-SRPartnership**, **Remove SRGroup** e **Remove SRPartnership** in ogni cluster.  

    ```powershell
    Get-SRPartnership | Remove-SRPartnership  
    Get-SRGroup | Remove-SRGroup  
    ```  

    > [!NOTE]  
    > Replica archiviazione smonta i volumi di destinazione. Questo comportamento è da progettazione.

## <a name="see-also"></a>Vedere anche

-   [Panoramica di Replica di archiviazione](storage-replica-overview.md) 
-   [Replica di Cluster esteso tramite l'archiviazione condivisa](stretch-cluster-replication-using-shared-storage.md)  
-   [Replica di archiviazione da server a Server](server-to-server-storage-replication.md)  
-   [Replica di archiviazione: Problemi noti](storage-replica-known-issues.md)  
-   [Replica di archiviazione: domande frequenti](storage-replica-frequently-asked-questions.md)  
-   [Spazi di archiviazione diretta in Windows Server 2016](../storage-spaces/storage-spaces-direct-overview.md)  