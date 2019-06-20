---
title: Novità di Windows Server 2019
description: Panoramica delle nuove funzionalità in Windows Server 2019, tra cui Esperienza desktop, il servizio di migrazione della risorsa di archiviazione, le informazioni dettagliate di sistema, la scheda di rete di Azure, miglioramenti agli Spazi di archiviazione diretta e altre modifiche.
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: high
ms.date: 06/04/2019
ms.openlocfilehash: 7110fe78982fec616174a93514d86fb2e1cf9fa5
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66810771"
---
# <a name="whats-new-in-windows-server-2019"></a>Novità di Windows Server 2019

> Si applica a: Windows Server 2019

In questo argomento vengono descritte alcune delle nuove funzionalità di Windows Server 2019. Windows Server 2019 si basa la solida base di Windows Server 2016 e include numerose innovazioni di quattro temi principali: Cloud ibrido, sicurezza, piattaforma di applicazioni e infrastruttura Iperconvergente (HCL).

Per scoprire nuove funzionalità di versioni canale semestrale di Windows Server, vedere [What ' s New in Windows Server](../get-started/whats-new-in-windows-server.md).

## <a name="general"></a>Generale

### <a name="windows-admin-center"></a>Windows Admin Center

Windows Admin Center è un'app distribuita in locale e basata su browser che consente di gestire server, cluster, infrastruttura iperconvergente e PC Windows 10. Non prevede costi aggiuntivi rispetto a Windows ed è pronta per essere usata in produzione.

È possibile installare Windows Admin Center in Windows Server 2019 così come Windows 10 e versioni precedenti di Windows e Windows Server e usarlo per gestire server e cluster che esegue Windows Server 2008 R2 e versioni successive.

Per altre informazioni, vedi [Windows Admin Center](../manage/windows-admin-center/understand/windows-admin-center.md).

### <a name="desktop-experience"></a>Esperienza desktop

Poiché Windows Server 2019 è una versione LTSC (Long-Term Servicing Channel), include l'<b>esperienza Desktop</b>. (Canale semestrale \(SAC\) versioni non includono l'esperienza Desktop per impostazione predefinita; sono Server Core e la rilascia immagine del contenitore Nano Server.) Come con Windows Server 2016, durante l'installazione del sistema operativo è possibile scegliere tra le installazioni Server Core o Server con le installazioni di esperienza Desktop.

### <a name="system-insights"></a>Informazioni dettagliate di sistema

Informazioni dettagliate di sistema è una nuova funzione disponibile in Windows Server 2019 che offre funzionalità di analisi predittiva locale in modalità nativa per Windows Server. Queste funzionalità predittive, ognuna abbinata a un modello di apprendimento automatico, analizzano localmente i dati di sistema di Windows Server, ad esempio i contatori delle prestazioni e gli eventi, fornendo dati approfonditi in merito al funzionamento dei server e contribuendo a ridurre i costi operativi associati alla gestione reattiva delle problematiche di Windows Server.

## <a name="hybrid-cloud"></a>Cloud ibrido

### <a name="server-core-app-compatibility-feature-on-demand"></a>Funzionalità di compatibilità dell'app Server Core su richiesta

La [funzionalità di compatibilità dell'app Server Core su richiesta](https://docs.microsoft.com/windows-server/get-started-19/install-fod-19) migliora notevolmente la compatibilità dell'app dell'opzione di installazione dei componenti di base di Windows Server attraverso l'inclusione di un sottoinsieme di file binari e componenti di Windows Server con Esperienza desktop, senza l'aggiunta dell'ambiente grafico di Esperienza desktop di Windows Server.  Questo ha lo scopo di migliorare la funzionalità e la compatibilità di Server Core, mantenendolo comunque più snello possibile.  

Questa funzionalità su richiesta facoltativa è disponibile in un file ISO separato e può essere aggiunta solo alle immagini e alle installazioni di base di Windows Server, mediante Gestione e manutenzione immagini distribuzione. 

## <a name="security"></a>Sicurezza

### <a name="windows-defender-advanced-threat-protection-atp"></a>Windows Defender Advanced Threat Protection (ATP)

Sensori avanzati della piattaforma e azioni di risposta di ATP espongono agli attacchi a livello di memoria e kernel e rispondono eliminando file dannosi e terminando processi dannosi.

-   Per altre informazioni su Windows Defender ATP, vedi [Panoramica delle funzionalità di Windows Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/overview).

-   Per ulteriori informazioni sull'onboarding di server, vedi [Eseguire l'onboarding dei server al servizio Windows Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-server-endpoints-windows-defender-advanced-threat-protection).

**Windows Defender ATP Exploit Guard** è un nuovo gruppo di funzionalità di prevenzione delle intrusioni. I quattro componenti di Windows Defender Exploit Guard sono progettati per proteggere il dispositivo da un'ampia gamma di vettori di attacco e comportamenti di blocco comunemente utilizzati in attacchi di malware, consentendoti di trovare il giusto equilibrio tra rischi correlati alla sicurezza e requisiti di produttività.

-   [Riduzione della superficie di attacco](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/attack-surface-reduction-exploit-guard?ocid=cx-blog-mmpc) è un gruppo di controlli che le grandi imprese possono abilitare per impedire l'accesso al computer di malware attraverso il blocco di file dannosi sospetti (ad esempio, file di Office), script, spostamento laterale, comportamento ransomware e minacce basate sulla posta elettronica.

-   [Protezione di rete](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/network-protection-exploit-guard?ocid=cx-blog-mmpc) protegge l'endpoint da minacce basate sul Web bloccando qualsiasi processo in uscita nel dispositivo per gli indirizzi host o IP non attendibili tramite Windows Defender SmartScreen.

-   [Accesso controllato alle cartelle](https://cloudblogs.microsoft.com/microsoftsecure/2017/10/23/stopping-ransomware-where-it-counts-protecting-your-data-with-controlled-folder-access/?ocid=cx-blog-mmpc?source=mmpc) protegge i dati sensibili da ransomware impedendo l'accesso di processi non attendibili alle cartelle protette.

-   [Protezione dagli exploit](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/exploit-protection-exploit-guard) è un gruppo di misure di prevenzione per gli exploit di vulnerabilità (in sostituzione di EMET) che è possibile configurare facilmente per proteggere il sistema e le applicazioni.

[Controllo di applicazioni di Windows Defender](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) (noto anche come criteri di integrità del codice) è stato rilasciato in Windows Server 2016.
Sulla base dei feedback forniti dai clienti l'idea è ottima, ma difficile da implementare.
Per risolvere questo problema, abbiamo creato criteri di integrazione continua predefiniti, che consentono a tutti i file interni di Windows e alle applicazioni Microsoft, ad esempio SQL Server, di bloccare i file eseguibili noti che possono ignorare l'integrazione continua. 

### <a name="security-with-software-defined-networking-sdn"></a>Sicurezza con Software Defined Networking (SDN)

[Sicurezza con SDN](https://docs.microsoft.com/windows-server/networking/sdn/security/sdn-security-top) offre numerose funzionalità per aumentare la fiducia dei clienti che eseguono carichi di lavoro, in locale, o come provider di servizi nel cloud. 

Questi miglioramenti della sicurezza sono integrati nella piattaforma SDN completa introdotta in Windows Server 2016.

Per un elenco completo delle novità di SDN, vedi [Novità di SDN per Windows Server 2019](https://docs.microsoft.com/windows-server/networking/sdn/sdn-whats-new).

### <a name="shielded-virtual-machines-improvements"></a>Miglioramenti delle macchine virtuali schermate

- **Miglioramenti di branch office**

    Ora puoi eseguire macchine virtuali schermate in computer con connettività intermittente al servizio Sorveglianza host sfruttando le nuove funzionalità del [server HGS di fallback](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-manage-branch-office#fallback-configuration) e la [modalità offline](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-manage-branch-office#offline-mode). Il server HGS di fallback ti consente di configurare un secondo gruppo di URL per Hyper-V per provare se è in grado di raggiungere il server HGS primario.

    La modalità offline ti consente di continuare ad avviare le macchine virtuali schermate, anche se HGS non può essere raggiunto, purché la macchina virtuale sia stata avviata correttamente una volta e la configurazione di protezione dell'host non sia cambiata.

- **Miglioramenti di risoluzione dei problemi**

    Abbiamo anche semplificato la [risoluzione dei problemi delle macchine virtuali schermate](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-shielded-vms) abilitando il supporto per la modalità sessione avanzata VMConnect e PowerShell Direct. Questi strumenti sono particolarmente utili se hai perso la connettività di rete alla macchina virtuale e devi aggiornarne la configurazione per ripristinare l'accesso. 

    Queste funzionalità non devono essere configurate e vengono rese disponibili automaticamente quando una macchina virtuale schermata viene posizionata su un host Hyper-V che esegue Windows Server versione 1803 o successiva.

- **Supporto Linux**

    Se esegui ambienti di sistema operativo misto, adesso Windows Server 2019 supporta l'esecuzione di Ubuntu, Red Hat Enterprise Linux e SUSE Linux Enterprise Server in macchine virtuali schermate.

### <a name="http2-for-a-faster-and-safer-web"></a>HTTP/2 per un Web più veloce e sicuro

- Unione delle connessioni migliorata per un'esperienza di esplorazione senza interruzioni e correttamente crittografata.

- Negoziazione del pacchetto di crittografia lato server di HTTP/2 aggiornata per la prevenzione automatica di errori di connessione e facilità di distribuzione.

- Il provider di congestione TCP predefinito è stato modificato in Cubico per offrirti una velocità effettiva maggiore.

## <a name="storage"></a>Archiviazione

Ecco alcune delle modifiche che abbiamo apportato all'archiviazione in Windows Server 2019. Per altre informazioni, vedi [Novità in Archiviazione](../storage/whats-new-in-storage.md).

### <a name="storage-migration-service"></a>Servizio di migrazione della risorsa di archiviazione

Il servizio di migrazione della risorsa di archiviazione è una nuova tecnologia che semplifica la migrazione dei server a una versione più recente di Windows Server. Fornisce uno strumento grafico che esegue l'inventario dei dati nei server, trasferisce i dati e la configurazione nei server più recenti e, facoltativamente, sposta le identità dei server precedenti ai nuovi server in modo che le app e gli utenti non debbano apportare alcuna modifica. Per altre info, vedi [Servizio di migrazione della risorsa di archiviazione](../storage/storage-migration-service/overview.md).

### <a name="storage-spaces-direct"></a>Spazi di archiviazione diretta

Ecco un elenco delle novità in Spazi di archiviazione diretta. Per altre informazioni, vedi [Novità in Spazi di archiviazione diretta](../storage/whats-new-in-storage.md#storage-spaces-direct). Vedere anche [Azure Stack uomo](https://docs.microsoft.com/azure-stack/operator/azure-stack-hci-overview) per informazioni sull'acquisizione convalidati i sistemi di spazi di archiviazione diretta.

- **La deduplicazione e compressione per i volumi ReFS**
- **Supporto nativo per la memoria persistente**
- **Resilienza annidata per l'infrastruttura iperconvergente due nodi nella rete perimetrale**
- **Cluster di due server con una porta USB, unità memoria flash come server di controllo**
- **Supporto di Windows Admin Center**
- **Cronologia delle prestazioni**
- **Scalabilità fino a 4 per ogni cluster PB**
- **Parità con accelerazione mirror è 2 volte più veloce**
- **Unità di rilevamento degli outlier latenza**
- **Consente di delimitare manualmente l'allocazione dei volumi per aumentare la tolleranza di errore**

### <a name="storage-replica"></a>Replica archiviazione

Ecco le novità in Replica di archiviazione. Per altre informazioni, vedi [Novità in Replica di archiviazione](../storage/whats-new-in-storage.md#storage-replica).

- Replica di archiviazione è ora disponibile in Windows Server 2019 Standard Edition.
- Il failover di test è una nuova funzionalità che consente il montaggio dell'archiviazione di destinazione per convalidare i dati di replica o di backup. Per altre informazioni, vedi [Domande frequenti su Replica di archiviazione](../storage/storage-replica/storage-replica-frequently-asked-questions.md).
- Miglioramenti delle prestazioni del log per Replica di archiviazione
- Supporto di Windows Admin Center

## <a name="failover-clustering"></a>Clustering di failover

Ecco un elenco delle novità in Clustering di failover. Per altre informazioni, vedi [Novità in Clustering di failover](../failover-clustering/whats-new-in-failover-clustering.md).

- **Set di cluster**
- **Azure compatibile con cluster**
- **Migrazione del cluster tra domini**
- **Controllo del mirroring USB**
- **Miglioramenti all'infrastruttura di cluster**
- **Aggiornamento compatibile con cluster supporta la funzionalità spazi di archiviazione diretta**
- **Miglioramenti di controllo di condivisione di file**
- **Protezione avanzata dei cluster**
- **Cluster di failover non usa l'autenticazione NTLM**

## <a name="application-platform"></a>Piattaforma per applicazioni

### <a name="linux-containers-on-windows"></a>Contenitori di Linux in Windows

Ora è possibile eseguire contenitori basati su Linux e Windows nello stesso host contenitore, utilizzando lo stesso daemon docker. Ciò ti consente di disporre di un ambiente costituito da host contenitori eterogenei, offrendo nel contempo flessibilità agli sviluppatori di applicazioni.

### <a name="built-in-support-for-kubernetes"></a>Supporto incorporato per Kubernetes

Windows Server 2019 apporta continui miglioramenti in fatto di elaborazione, rete e archiviazione attraverso i rilasci del Canale semestrale, necessari per supportare Kubernetes su Windows. Altri dettagli sono disponibili nelle versioni future di Kubernetes.

- [Rete di contenitori](https://docs.microsoft.com/windows-server/networking/sdn/technologies/containers/container-networking-overview) in Windows Server 2019 migliora notevolmente l'usabilità di Kubernetes in Windows migliorando la resilienza di rete della piattaforma e il supporto di plug-in della rete dei contenitori.

- I carichi di lavoro distribuiti su Kubernetes sono in grado di usare la protezione di rete per la protezione dei servizi Linux e Windows con strumenti incorporati.

### <a name="container-improvements"></a>Miglioramenti ai contenitori
    
- **Identità integrata migliorata**

    L'impostazione Autenticazione integrata di Windows nei contenitori è stata resa più semplice e affidabile, risolvendo così diverse limitazioni rispetto alle versioni precedenti di Windows Server.

- **Migliore compatibilità tra applicazioni**

    Inserimento nei contenitori di applicazioni basate su Windows appena ora più semplice: La compatibilità dell'applicazione esistente *windowsservercore* immagine sia stata aumentata. Per le applicazioni con dipendenze API aggiuntive, è ora disponibile una terza immagine di base: *windows*.

- **Dimensione ridotta e prestazioni più elevate**

    Le dimensioni di download dell'immagine contenitore di base, la dimensione su disco e i tempi di avvio sono stati migliorati. Questo accelera i flussi di lavoro del contenitore

- **Esperienza di gestione tramite Windows Admin Center \(anteprima\)**

    Vedere quali contenitori sono in esecuzione nel computer e gestire i singoli contenitori con una nuova estensione per Windows Admin Center non è mai stato così semplice. Cerca l'estensione "Containers" nel [feed pubblico di Windows Admin Center](https://docs.microsoft.com/windows-server/manage/windows-admin-center/configure/using-extensions).

### <a name="encrypted-networks"></a>Reti crittografate

[Reti codificate](https://docs.microsoft.com/windows-server/networking/sdn/sdn-whats-new) - La codifica di rete virtuale consente la codifica del traffico di rete virtuale tra le macchine virtuali che comunicano tra loro all'interno di subnet contrassegnate come **Codifica abilitata**. Utilizza anche Datagram Transport Layer Security (DTLS) nella subnet virtuale per codificare pacchetti. DTLS impedisce intercettazioni, manomissioni e contraffazioni da parte di chiunque abbia accesso alla rete fisica.

### <a name="network-performance-improvements-for-virtual-workloads"></a>Miglioramenti nelle prestazioni di rete per i carichi di lavoro virtuali

[Miglioramenti alle prestazioni di rete per i carichi di lavoro virtuali](https://docs.microsoft.com/windows-server/networking/technologies/hpn/hpn-insider-preview) consente di ottimizzare la velocità di rete sulle macchine virtuali senza che dover costantemente sincronizzare o effettuare il provisioning eccessivo dell'host. Questo riduce le operazioni e i costi di manutenzione, migliorando la densità disponibile degli host. Queste nuove funzionalità sono:

* Unione segmenti ricevuti (RSC) nel commutatore virtuale

* Coda di più macchine virtuali dinamica (d.VMMQ)

### <a name="low-extra-delay-background-transport"></a>Low Extra Delay Background Transport

Low Extra Delay Background Transport (LEDBAT) è un provider di controllo della congestione della rete, ottimizzato per la latenza, progettato per produrre automaticamente larghezza di banda per gli utenti e le applicazioni, che usa l'intera larghezza di banda disponibile quando la rete non è in uso.   
Questa tecnologia è progettata per l'uso nella distribuzione di aggiornamenti critici e di grandi dimensioni in un ambiente IT senza influire sui servizi per i clienti e sulla larghezza di banda associata.

### <a name="windows-time-service"></a>Ora di Windows

Il [servizio Ora di Windows](https://docs.microsoft.com/windows-server/networking/windows-time-service/insider-preview) include un reale supporto di secondi intercalari conforme a UTC, un nuovo protocollo orario chiamato Precision Time Protocol e tracciabilità end-to-end.


### <a name="high-performance-sdn-gateways"></a>Gateway SDN ad alte prestazioni

[I gateway SDN ad alte prestazioni](https://docs.microsoft.com/windows-server/networking/sdn/gateway-performance) in Windows Server 2019 migliorano notevolmente le prestazioni per le connessioni IPsec e GRE, fornendo una velocità effettiva molto elevata con un utilizzo della CPU molto inferiore.
<br/>

### <a name="new-deployment-ui-and-windows-admin-center-extension-for-sdn"></a>Nuova estensione dell'interfaccia di distribuzione e di Windows Admin Center per SDN

Con Windows Server 2019, è facile distribuire e gestire tramite una nuova interfaccia utente di sviluppo e un'estensione di Windows Admin Center che consentono a tutti di sfruttare le potenzialità di SDN. 

### <a name="persistent-memory-support-for-hyper-v-vms"></a>Supporto della memoria persistente per macchine virtuali Hyper-V

Per sfruttare la velocità effettiva elevata e la bassa latenza della memoria persistente (ovvero memoria della classe di archiviazione) nelle macchine virtuali, adesso può essere proiettata direttamente nelle macchine virtuali. Ciò consente di ridurre notevolmente la latenza di transazione del database o i tempi di ripristino per i database in memoria a bassa latenza in caso di errore.
