---
title: Configurare le reti locali virtuali per Hyper-V
description: Vengono fornite istruzioni per la configurazione di una rete locale virtuale (VLAN) per l'utilizzo da parte di macchine virtuali in un host Hyper-V.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8510a709-001c-4eee-b6d6-c451e8a8a836
author: KBDAzure
ms.author: kathydav
ms.date: 10/11/2016
ms.openlocfilehash: f2c240a3ad9f9783e509efb288cc6c6410339685
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364284"
---
# <a name="configure-virtual-local-area-networks-for-hyper-v"></a>Configurare le reti locali virtuali per Hyper-V
Le reti locali virtuali \(VLANs @ no__t-1 offrono un modo per isolare il traffico di rete. Le VLAN sono configurate in commutatori e router che supportano 802.1 q. Se si configurano più VLAN e si desidera che si verifichi la comunicazione tra di esse, sarà necessario configurare i dispositivi di rete in modo da consentirne l'esecuzione. 

Per configurare le VLAN, è necessario quanto segue:  
  
-   Una scheda di rete fisica e un driver che supporti la codifica VLAN 802.1 q.  
-   Uno switch di rete fisico che supporta la codifica VLAN 802.1 q.  
  
Nell'host verrà configurato il Commuter virtuale per consentire il traffico di rete sulla porta di commutazione fisica. Per gli ID VLAN che si desidera utilizzare internamente con le macchine virtuali. Successivamente, si configura la macchina virtuale per specificare la VLAN che verrà utilizzata dalla macchina virtuale per tutte le comunicazioni di rete.  
  
#### <a name="to-allow-a-virtual-switch-to-use-a-vlan"></a>Per consentire a un commutire virtuale di usare una VLAN  
  
1.  Aprire Hyper @ no__t-0V Manager.  
  
2.  Scegliere **gestione Commutiri virtuali**dal menu azioni.  
  
3.  In **commutatori virtuali**selezionare un commutatore virtuale connesso a una scheda di rete fisica che supporta le VLAN. 

4. Nel riquadro destro, in ID VLAN, selezionare **Abilita identificazione LAN virtuale** , quindi digitare un numero per l'ID VLAN.  
  
    Tutto il traffico che passa attraverso la scheda di rete fisica connessa al Commuter virtuale verrà contrassegnato con l'ID VLAN impostato.  
  
#### <a name="to-allow-a-virtual-machine-to-use-a-vlan"></a>Per consentire a una macchina virtuale di usare una VLAN  
  
1.  Aprire Hyper @ no__t-0V Manager.  
  
2.  Nel riquadro dei risultati, in **macchine virtuali**, selezionare la macchina virtuale appropriata e quindi fare clic con il pulsante destro del mouse su **Impostazioni**.  

3.  In **hardware**selezionare un Commuter virtuale configurato con una VLAN.
  
4.  Nel riquadro di destra selezionare **Abilita identificazione LAN virtuale**, quindi digitare lo stesso ID VLAN di quello specificato per il Commuter virtuale. 

Se la macchina virtuale deve usare più VLAN, eseguire una delle operazioni seguenti:  
  
-   Connettere più schede di rete virtuali ai commutatori virtuali appropriati e assegnare gli ID VLAN. Assicurarsi di configurare correttamente gli indirizzi IP e che il traffico che si vuole indirizzare tramite la VLAN usi anche l'indirizzo IP corretto.  
  
-   Configurare la scheda di Word della rete virtuale in modalità trunk usando il [set @ no__t-1VMNetworkAdapterVlan](https://technet.microsoft.com/library/hh848475.aspx) cmdlet.
  
## <a name="see-also"></a>Vedere anche  
 
[Commuter virtuale Hyper @ no__t-1V](https://technet.microsoft.com/windows-server-docs/networking/technologies/hyper-v-virtual-switch/hyper-v-virtual-switch)