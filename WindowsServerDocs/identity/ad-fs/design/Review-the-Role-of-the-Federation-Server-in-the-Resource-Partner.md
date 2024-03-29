---
ms.assetid: f88238ea-d851-4129-8b4e-a3a62b813614
title: Rivedere il ruolo del server federativo nel partner risorse
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: fd9f20eb7559f5862ee50bdd8364fa1604d3c1b6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358975"
---
# <a name="review-the-role-of-the-federation-server-in-the-resource-partner"></a>Rivedere il ruolo del server federativo nel partner risorse

Il server federativo nell'organizzazione partner risorse intercetta i token di sicurezza in ingresso inviati da un server federativo di account, li convalida e li firma e quindi rilascia i propri token di sicurezza destinati all'applicazione Web @ no__t-0based .  
  
> [!NOTE]  
> Quando gli utenti federati usano i Web browser per accedere alle applicazioni Web @ no__t-0based, il server federativo nell'organizzazione partner risorse compila un nuovo cookie di autenticazione e lo scrive nel browser. Questo cookie Abilita le funzionalità Single @ no__t-0sign @ no__t-1Sulla Barra \(SSO @ no__t-3 in modo che gli utenti non debbano accedere di nuovo al server federativo nel partner account quando gli utenti tentano di accedere a diverse applicazioni Web @ no__t-4based nella risorsa partner.  
  
Nel progetto Web SSO è necessario installare almeno un server federativo nella rete perimetrale. Nel progetto SSO Web federativo deve essere installato almeno un server federativo nella rete aziendale dell'organizzazione partner account e almeno un server federativo installato nella rete aziendale dell'organizzazione partner risorse.  
  
> [!NOTE]  
> Prima di poter configurare un computer server federativo nell'organizzazione partner risorse, è innanzitutto necessario aggiungere il computer a qualsiasi dominio Active Directory nell'organizzazione partner risorse. Per ulteriori informazioni, vedere [Elenco di controllo: Configurazione di un server federativo @ no__t-0.  
  
## <a name="see-also"></a>Vedere anche
[Guida alla progettazione di AD FS in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

