---
title: Commutatore virtuale Hyper-V
description: Questo argomento fornisce una panoramica del Commuter virtuale Hyper-V in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: article
ms.assetid: 398440ac-5988-41ce-b91e-eab343a255d3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c508005af67e9dd5b0c9a22693aca25eb19e8e48
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366827"
---
# <a name="hyper-v-virtual-switch"></a>Commutatore virtuale Hyper-V

>Si applica a: Windows Server (Canale semestrale), Windows Server 2016

Questo argomento fornisce una panoramica del Commuter virtuale Hyper-V, che consente di connettere le macchine virtuali \(VMs @ no__t-1 alle reti esterne all'host Hyper @ no__t-2V, inclusa la rete Intranet dell'organizzazione e Internet. 

È anche possibile connettersi alle reti virtuali sul server che esegue Hyper @ no__t-0V quando si distribuisce software defined networking \(SDN @ no__t-2.

> [!NOTE]  
> Oltre a questo argomento, è disponibile la documentazione seguente relativa al Commuter virtuale Hyper-V.  
>   
> - [Gestire il commutatore virtuale Hyper-V](Manage-Hyper-V-Virtual-Switch.md) 
> - [Accesso diretto a memoria remota (RDMA) e Switch Embedded Teaming (SET)](RDMA-and-Switch-Embedded-Teaming.md)
> - [Cmdlet del team del commutire di rete in Windows PowerShell](https://technet.microsoft.com/library/jj553812.aspx)
> - [Novità di VMM 2016](https://docs.microsoft.com/system-center/vmm/whats-new#networking)
> - [Configurare l'infrastruttura di rete VMM](https://docs.microsoft.com/system-center/vmm/manage-networks)
> - [Creare reti con VMM 2012](https://social.technet.microsoft.com/wiki/contents/articles/3140.create-networks-with-vmm-2012.aspx)  
> - [Hyper-V: Configurare VLAN e tag VLAN @ no__t-0  
> - [Hyper-V: È necessario abilitare l'estensione del Commuter virtuale di WFP se è richiesta da estensioni di terze parti @ no__t-0
>
> Per ulteriori informazioni sulle altre tecnologie di rete, vedere la pagina relativa [alla rete in Windows Server 2016](https://docs.microsoft.com/windows-server/networking/networking).
  
Hyper @ no__t-0V Virtual Switch è uno switch di rete Ethernet di livello 2 Basato su software disponibile in Hyper @ no__t-1V Manager quando si installa il ruolo del server Hyper @ no__t-2V.

Il Commuter virtuale Hyper-V include funzionalità gestite ed estendibili a livello di codice per connettere le macchine virtuali a entrambe le reti virtuali e alla rete fisica. Il commutatore virtuale Hyper-V supporta inoltre l'imposizione di criteri per sicurezza, l'isolamento e i livelli di servizio.  
  
> [!NOTE]  
> Il commutatore virtuale Hyper-V supporta solo Ethernet e non supporta altre tecnologie di rete locale cablata (LAN), ad esempio Infiniband e Fibre Channel.  
  
Il Commuter virtuale Hyper-V include funzionalità di isolamento dei tenant, shaping del traffico, protezione da macchine virtuali dannose e risoluzione dei problemi semplificata. 

Con il supporto incorporato per la specifica di interfaccia dispositivo di rete \(NDIS @ no__t-1 driver di filtro e Windows Filtering Platform \(WFP @ no__t-3 callout Drivers, il Commuter virtuale Hyper-V Abilita fornitori di software indipendenti \(ISVs @ no__ t-5 per creare plug-in estendibili, detti estensioni del Commuter virtuale, che possono fornire funzionalità di rete e sicurezza avanzate. Le estensioni del commutatore virtuale aggiunte al commutatore virtuale Hyper-V sono elencate nell'area Gestione commutatori virtuali della console di gestione di Hyper-V.
  
Nella figura seguente, una macchina virtuale dispone di una scheda di interfaccia di rete virtuale connessa al compartitore virtuale Hyper-V tramite una porta di commutazione.  
  
![Connessioni Commuter virtuali](../media/Hyper-V-Virtual-Switch/Vswitch_01.jpg)  
  
Le funzionalità del Commuter virtuale Hyper-V offrono altre opzioni per l'applicazione dell'isolamento dei tenant, il data shaping e il controllo del traffico di rete e l'uso di misure di protezione contro le VM dannose.

>[!NOTE]
> In Windows Server 2016, una VM con una scheda di interfaccia di rete virtuale Visualizza accuratamente la velocità effettiva massima per la scheda di interfaccia di rete virtuale. Per visualizzare la velocità della scheda di interfaccia di rete virtuale in **connessioni di rete**, fare clic con il pulsantedestro del mouse sull'icona della scheda di interfaccia di rete virtuale Verrà visualizzata la finestra di dialogo **stato** scheda di interfaccia di rete virtuale. In **connessione**, il valore di **Speed** corrisponde alla velocità della scheda di interfaccia di rete fisica installata nel server.
  
## <a name="bkmk_apps"></a>Usi per il Commuter virtuale Hyper-V

Di seguito sono riportati alcuni scenari di casi d'uso per il Commuter virtuale Hyper-V.

**Visualizzazione di statistiche**: uno sviluppatore presso un fornitore di cloud ospitati implementa un pacchetto di gestione che visualizza lo stato attuale del commutatore virtuale Hyper-V. Utilizzando WMI, il pacchetto di gestione è in grado di recuperare informazioni su funzionalità correnti dell'intero commutatore, impostazioni di configurazione e statistiche di rete per le singole porte. Mostra quindi lo stato del commutatore per fornire agli amministratori una visualizzazione rapida dello stato del commutatore.  
  
**Rilevamento delle risorse**: una società di hosting vende servizi di hosting con prezzo variabile in base al livello dell'abbonamento. Ai vari livelli di abbonamento corrispondono livelli diversi di prestazioni della rete. L'amministratore alloca le risorse in base agli SLA, in maniera tale da bilanciare la disponibilità della rete. L'amministratore tiene traccia a livello di codice delle informazioni, ad esempio l'uso corrente della larghezza di banda assegnata e il numero di canali VMQ (Virtual Machine Queue) assegnati alla macchina virtuale (VM) o IOV. Lo stesso programma periodicamente registra anche le risorse in uso, oltre alle risorse assegnate per macchina virtuale, per effettuare un controllo incrociato delle risorse.  
  
**Gestione dell'ordine delle estensioni del Commuter**: un'azienda ha installato nel proprio host Hyper-V estensioni che consentono di monitorare il traffico e segnalare le intrusioni rilevate. Durante la manutenzione alcune estensioni potrebbero essere aggiornate, determinando un cambiamento dell'ordine. Viene eseguito un semplice programma script per riordinare le estensioni dopo gli aggiornamenti.  
  
L' **estensione di avanzamento gestisce l'ID VLAN**: un'importante società di switch sta realizzando un'estensione di inoltro che applica tutti i criteri per le funzionalità di rete. Gli elementi gestiti includono gli ID delle reti locali virtuali (VLAN, Virtual Local Area Network). Il commutatore virtuale cede il controllo della VLAN a un'estensione di inoltro. L'installazione della società del commutatore chiama a livello di codice un Application Programming Interface di Strumentazione gestione Windows (WMI) che attiva la trasparenza, indicando al commutatore virtuale Hyper-V di passare senza eseguire alcuna azione sui tag VLAN.  
  
## <a name="bkmk_func"></a>Funzionalità del Commuter virtuale Hyper-V
 
Le principali funzionalità incluse in commutatore virtuale Hyper-V sono:  
  
-   **Protezione da poisoning (spoofing) ARP/ND**: protegge il sistema da una macchina virtuale dannosa che usa lo spoofing ARP per rubare indirizzi IP da altre macchine virtuali. Protegge il sistema dai potenziali attacchi a IPv6 tramite spoofing ND.  
  
-   **Protezione DHCP Guard**: protegge il sistema da una macchina virtuale dannosa che si identifica come server DHCP (Dynamic Host Configuration Protocol) per gli attacchi man-in-the-middle.  
  
-   **ACL delle porte**: consente di filtrare il traffico in base agli indirizzi o intervalli MAC (Media Access Control) o IP (Internet Protocol), permettendo di configurare l'isolamento delle reti virtuali.  
  
-   **Modalità trunk per una macchina virtuale**: consente agli amministratori di configurare una macchina virtuale specifica come appliance virtuale e quindi indirizzare il traffico di varie VLAN a tale macchina virtuale.  
  
-   **Monitoraggio del traffico di rete**: consente agli amministratori di esaminare il traffico che attraversa il commutatore di rete.  
  
-   **VLAN isolata (privata)** : consente agli amministratori di separare il traffico su più VLAN, per creare più facilmente community tenant isolate.  
  
Di seguito sono elencate le funzionalità che migliorano le possibilità di utilizzo del commutatore virtuale Hyper-V:  
  
-   **Limite della larghezza di banda e supporto di**espansione: la larghezza di banda minima garantisce la quantità di larghezza di banda riservata. La larghezza di banda massima pone un limite alla quantità di larghezza di banda utilizzabile da una macchina virtuale.  
  
-   **Supporto per contrassegno esplicito di congestione (ECN)** :  Il contrassegno ECN, noto anche come data contrassegni ECN (DCTCP), consente al commutere fisico e al sistema operativo di regolamentare il flusso del traffico in modo che le risorse del buffer del commutino non vengano sovraccaricate, con conseguente aumento della velocità effettiva del traffico.  
  
-   **Diagnostica**: la diagnostica semplifica il tracciamento e il monitoraggio degli eventi e dei pacchetti che attraversano il commutatore virtuale.
