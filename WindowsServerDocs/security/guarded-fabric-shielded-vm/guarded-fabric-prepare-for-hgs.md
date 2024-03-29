---
title: Verificare i prerequisiti di HGS
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: f4b4d1a8-bf6d-4881-9150-ddeca8b48038
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 9024557dd42ede27144bf10aa5873b6bb12d585c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403489"
---
# <a name="review-prerequisites-for-the-host-guardian-service"></a>Verificare i prerequisiti per il servizio sorveglianza host

>Si applica a: Windows Server 2019, Windows Server (canale semestrale), Windows Server 2016


In questo argomento vengono illustrati i prerequisiti di HGS e i passaggi iniziali per preparare la distribuzione di HGS.

## <a name="prerequisites"></a>Prerequisiti 

-   **Hardware**: HGS può essere eseguito su macchine fisiche o virtuali, ma sono consigliate macchine fisiche.

    Se si desidera eseguire HGS come cluster fisico a tre nodi (per la disponibilità), è necessario disporre di tre server fisici. Come procedura consigliata per il clustering, i tre server dovrebbero avere hardware molto simile.
  
-   **Sistema operativo**: L'attestazione della chiave host richiede Windows Server 2019 standard o Datacenter Edition che opera con l' [attestazione V2](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#versioned-attestation-policies). Per l'attestazione basata su TPM, HGS può eseguire Windows Server 2019 o Windows Server 2016, standard o Datacenter Edition.

-   **Ruoli del server**: Il servizio sorveglianza host e i ruoli del server di supporto.

-   **Autorizzazioni/privilegi di configurazione per il dominio dell'infrastruttura (host)** : Sarà necessario configurare l'invio DNS tra il dominio dell'infrastruttura (host) e il dominio HGS. 
    
## <a name="upgrading-hgs"></a>Aggiornamento di HGS

Se è già stata eseguita la distribuzione di HGS e si vuole aggiornare il sistema operativo, seguire le [indicazioni](guarded-fabric-upgrade-to-2019.md) per l'aggiornamento per aggiornare i server HGS e Hyper-V al sistema operativo più recente.

## <a name="next-step"></a>Passaggio successivo

> [!div class="nextstepaction"]
> [Ottenere i certificati per HGS](guarded-fabric-obtain-certs.md)