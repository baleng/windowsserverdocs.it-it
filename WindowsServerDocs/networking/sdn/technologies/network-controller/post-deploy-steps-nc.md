---
title: Passaggi di post-distribuzione per il controller di rete
description: In questo argomento vengono fornite le istruzioni per la configurazione dei certificati per le distribuzioni non Kerberos del controller di rete in Windows Server 2016 datacenter.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: eea0aca9-8d89-48fb-8068-fca40c90d34b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3f95d2884a808239c1d171eecbc983e26e799102
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355622"
---
# <a name="post-deployment-steps-for-network-controller"></a>Passaggi di post-distribuzione per il controller di rete

Quando si installa il controller di rete, è possibile scegliere le distribuzioni Kerberos o non Kerberos.

Per le distribuzioni non @ no__t-0Kerberos, è necessario configurare i certificati.

## <a name="configure-certificates-for-non-kerberos-deployments"></a>Configurare i certificati per le distribuzioni non Kerberos

Se i computer o le macchine virtuali \(VMs @ no__t-1 per il controller di rete e il client di gestione non sono Domain @ no__t-2joined, è necessario configurare l'autenticazione del certificato @ no__t-3based completando i passaggi seguenti.

- Creare un certificato nel controller di rete per l'autenticazione del computer. Il nome del soggetto del certificato deve corrispondere al nome DNS del computer o della macchina virtuale del controller di rete.

- Creare un certificato nel client di gestione. Questo certificato deve essere considerato attendibile dal controller di rete.
  
- Registrare un certificato nel computer del controller di rete o nella macchina virtuale. Il certificato deve soddisfare i requisiti seguenti.
  
    -  Sia lo scopo di autenticazione del server che lo scopo di autenticazione client devono essere configurati in utilizzo chiavi avanzato \(EKU @ no__t-1 o estensioni criteri di applicazione. L'identificatore di oggetto per l'autenticazione del server è 1.3.6.1.5.5.7.3.1. L'identificatore di oggetto per l'autenticazione client è 1.3.6.1.5.5.7.3.2.
  
    - Il nome del soggetto del certificato deve essere risolto in:
  
        - Indirizzo IP del computer del controller di rete o della macchina virtuale, se il controller di rete viene distribuito in un singolo computer o macchina virtuale.

        - Indirizzo IP REST, se il controller di rete viene distribuito su più computer, più macchine virtuali o entrambi.
  
    - Questo certificato deve essere considerato attendibile da tutti i client REST. Il certificato deve anche essere considerato attendibile dai computer host di bilanciamento del carico software (SLB) multiplexer (MUX) e da quelli a sud gestiti dal controller di rete.
  
    - Il certificato può essere registrato da un'autorità di certificazione (CA) o può essere un certificato autofirmato. I certificati autofirmati non sono consigliati per le distribuzioni di produzione, ma sono accettabili per gli ambienti Lab di test.
  
    - È necessario eseguire il provisioning dello stesso certificato in tutti i nodi del controller di rete. Dopo aver creato il certificato in un nodo, è possibile esportare il certificato (con chiave privata) e importarlo negli altri nodi.

Per altre informazioni, vedere [Controller di rete](Network-Controller.md).
