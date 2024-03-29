---
title: Panoramica di servizio migrazione archiviazione
description: Il servizio di migrazione archiviazione semplifica la migrazione dei server a una versione più recente di Windows Server. Fornisce uno strumento grafico che archivia i dati nei server, quindi trasferisce i dati e la configurazione in server più recenti, tutto senza che le app o gli utenti debbano apportare alcuna modifica.
author: jasongerend
ms.author: jgerend
manager: elizapo
ms.date: 08/16/2019
ms.topic: article
ms.prod: windows-server
ms.technology: storage
ms.openlocfilehash: 022b0c3445c007960c490159f6580a702233ee41
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402980"
---
# <a name="storage-migration-service-overview"></a>Panoramica di servizio migrazione archiviazione

>Si applica a: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server (canale semestrale)

Il servizio di migrazione archiviazione semplifica la migrazione dei server a una versione più recente di Windows Server. Fornisce uno strumento grafico che archivia i dati nei server, quindi trasferisce i dati e la configurazione in server più recenti, tutto senza che le app o gli utenti debbano apportare alcuna modifica.

Questo argomento descrive il motivo per cui si vuole usare il servizio migrazione archiviazione, il funzionamento del processo di migrazione e i requisiti per i server di origine e di destinazione.

## <a name="why-use-storage-migration-service"></a>Perché usare il servizio migrazione archiviazione

Usare il servizio migrazione archiviazione perché si dispone di un server o di un numero elevato di server di cui si vuole eseguire la migrazione a hardware o macchine virtuali più recenti. Il servizio migrazione archiviazione è progettato per semplificare le operazioni seguenti:

- Inventario di più server e dei relativi dati
- Trasferimento rapido di file, condivisioni file e configurazione di sicurezza dai server di origine
- Facoltativamente, assumere l'identità dei server di origine (noto anche come riduzione), in modo che gli utenti e le app non debbano modificare nulla per accedere ai dati esistenti
- Gestire una o più migrazioni dall'interfaccia utente di Windows Admin Center

![Diagramma che mostra il servizio migrazione archiviazione che esegue la migrazione dei file & configurazione dai server di origine ai server di destinazione, alle macchine virtuali di Azure o Sincronizzazione file di Azure.](media/overview/storage-migration-service-diagram.png)

**Figura 1: Origini e destinazioni del servizio migrazione archiviazione**

## <a name="how-the-migration-process-works"></a>Funzionamento del processo di migrazione

La migrazione è un processo in tre passaggi:

1. **Server di inventario** per raccogliere informazioni sui file e sulla configurazione (mostrati nella figura 2).
2. **Trasferire (copiare) i dati** dai server di origine ai server di destinazione.
3. **Riduci ai nuovi server** (facoltativo).<br>I server di destinazione presuppongono le identità precedenti dei server di origine in modo che le app e gli utenti non debbano modificare alcun elemento. <br>I server di origine entrano in uno stato di manutenzione in cui contengono ancora gli stessi file che hanno sempre (i file non vengono mai rimossi dai server di origine) ma non sono disponibili per utenti e app. È quindi possibile rimuovere le autorizzazioni dei server per praticità.

![Screenshot che mostra un server pronto per essere](media/migrate/inventory.png)
analizzato**figura 2: Server di inventario servizio migrazione archiviazione**

## <a name="requirements"></a>Requisiti

Per usare il servizio migrazione archiviazione, è necessario quanto segue:

- Un **server di origine** o un **cluster di failover** per la migrazione di file e dati da
- Un **server di destinazione** che esegue Windows Server 2019 (cluster o autonomo) per la migrazione a. Anche Windows Server 2016 e Windows Server 2012 R2 funzionano ma sono più lenti al 50%
- Un server dell'agente di **orchestrazione** che esegue Windows Server 2019 per gestire la migrazione  <br>Se si esegue la migrazione solo di alcuni server e uno dei server esegue Windows Server 2019, è possibile usarlo come agente di orchestrazione. Se si esegue la migrazione di più server, è consigliabile usare un server dell'agente di orchestrazione separato.
- Un **PC o un server che esegue [l'interfaccia di amministrazione di Windows](../../manage/windows-admin-center/understand/windows-admin-center.md)** per eseguire l'interfaccia utente del servizio migrazione archiviazione, a meno che non si preferisca usare PowerShell per gestire la migrazione. L'interfaccia di amministrazione di Windows e la versione di Windows Server 2019 devono essere entrambe almeno la versione 1809.

Si consiglia vivamente che l'agente di orchestrazione e i computer di destinazione dispongano di almeno due core o due vCPU e almeno 2 GB di memoria. Le operazioni di inventario e trasferimento sono notevolmente più veloci con più processori e memoria.

### <a name="security-requirements-the-storage-migration-service-proxy-service-and-firewall-ports"></a>Requisiti di sicurezza, servizio proxy del servizio migrazione archiviazione e porte del firewall

- Un account di migrazione che è un amministratore dei computer di origine e del computer dell'agente di orchestrazione.
- Un account di migrazione amministratore nei computer di destinazione e nel computer dell'agente di orchestrazione.
- Il computer dell'agente di orchestrazione deve avere la regola firewall di condivisione file e stampanti (SMB-in) abilitata in *ingresso*.
- Per i computer di origine e di destinazione devono essere abilitate le seguenti regole firewall in *ingresso* (anche se è possibile che siano già state abilitate):
  - Condivisione di file e stampanti (SMB-In)
  - Servizio Netlogon (NP-in)
  - Strumentazione gestione Windows (DCOM-in)
  - Strumentazione gestione Windows (WMI-In)
  
  > [!TIP]
  > L'installazione del servizio proxy del servizio migrazione archiviazione in un computer Windows Server 2019 apre automaticamente le porte del firewall necessarie nel computer. A tale scopo, connettersi al server di destinazione nell'interfaccia di amministrazione di Windows, quindi passare a **Server Manager** (nell'interfaccia di amministrazione di windows) > **ruoli e funzionalità**, selezionare **proxy servizio migrazione archiviazione**e quindi selezionare **Installa**.


- Se i computer appartengono a un dominio Active Directory Domain Services, devono appartenere alla stessa foresta. Il server di destinazione deve inoltre trovarsi nello stesso dominio del server di origine se si desidera trasferire il nome di dominio dell'origine alla destinazione durante il trasferimento. Cutover tecnicamente funziona tra domini, ma il nome di dominio completo della destinazione sarà diverso da quello di origine...

### <a name="requirements-for-source-servers"></a>Requisiti per i server di origine

Il server di origine deve eseguire uno dei sistemi operativi seguenti:

- Windows Server, Canale semestrale
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2
- Windows Server 2008
- Windows Server 2003 R2
- Windows Server 2003
- Windows Small Business Server 2003 R2
- Windows Small Business Server 2008
- Windows Small Business Server 2011
- Windows Server 2012 Essentials
- Windows Server 2012 R2 Essentials
- Windows Server 2016 Essentials
- Windows Server 2019 Essentials

Nota: Windows Small Business Server e Windows Server Essentials sono controller di dominio. Il servizio migrazione archiviazione non è ancora in grado di superare i controller di dominio, ma è possibile eseguirne l'inventario e il trasferimento.   

È possibile eseguire la migrazione dei seguenti tipi di origine aggiuntivi se l'agente di orchestrazione esegue Windows Server, versione 1903 o successiva o se l'agente di orchestrazione esegue una versione precedente di Windows Server con [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) installato:

- Cluster di failover
- Server Linux che usano Samba. Sono stati testati gli elementi seguenti:
    - CentOS 7
    - Debian GNU/Linux 8
    - RedHat Enterprise Linux 7,6
    - SUSE Linux Enterprise Server (SLES) 11 SP4
    - Ubuntu 16,04 LTS e 12.04.5 LTS
    - Samba 4,8, 4,7, 4,3, 4,2 e 3,6

### <a name="requirements-for-destination-servers"></a>Requisiti per i server di destinazione

Il server di destinazione deve eseguire uno dei sistemi operativi seguenti:

- Windows Server, Canale semestrale
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2

> [!TIP]
> I server di destinazione che eseguono Windows Server 2019 o Windows Server, il canale semestrale o versioni successive hanno il doppio delle prestazioni di trasferimento delle versioni precedenti di Windows Server. Questo miglioramento delle prestazioni è dovuto all'inclusione di un servizio proxy del servizio di migrazione archiviazione integrato, che apre anche le porte del firewall necessarie se non sono già aperte.

## <a name="whats-new-in-storage-migration-service"></a>Novità del servizio migrazione archiviazione

Le nuove funzionalità seguenti sono disponibili quando si esegue l'agente di orchestrazione del server di migrazione archiviazione in Windows Server, versione 1903 o successiva o una versione precedente di Windows Server con [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) installato:

- Migrazione di utenti e gruppi locali al nuovo server
- Eseguire la migrazione dello spazio di archiviazione dai cluster di failover, eseguire la migrazione ai cluster di failover ed eseguire la migrazione tra server autonomi e cluster di failover
- Migrazione degli archivi da un server Linux che usa Samba
- Sincronizzazione semplificata tramite Sincronizzazione file di Azure delle condivisioni sottoposte a migrazione
- Migrazione a nuove reti, ad esempio Azure

## <a name="see-also"></a>Vedere anche

- [Eseguire la migrazione di un file server usando il servizio migrazione archiviazione](migrate-data.md)
- [Domande frequenti sui servizi di migrazione archiviazione](faq.md)
- [Problemi noti del servizio migrazione archiviazione](known-issues.md)
