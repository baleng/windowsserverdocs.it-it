---
ms.assetid: 8c3536b7-d091-4ee6-ad04-24713f070862
title: Distribuzione di AD FS nell'organizzazione partner account
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 63c080904482814f9f62451e8e7cfa4862d19927
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359249"
---
# <a name="deploying-ad-fs-in-the-account-partner-organization"></a>Distribuzione di AD FS nell'organizzazione partner account

Un partner account in Active Directory Federation Services \(AD FS @ no__t-1 rappresenta l'organizzazione nella relazione di trust federativa che archivia fisicamente gli account utente in un archivio di attributi supportato. Per ulteriori informazioni sugli archivi di attributi supportati, vedere [ruolo degli archivi di attributi](../../ad-fs/technical-reference/The-Role-of-Attribute-Stores.md).  
  
Il server federativo nell'organizzazione partner account autentica gli utenti locali e crea i token di sicurezza usati dal partner risorse per prendere decisioni relative alle autorizzazioni. Le relying party, ad esempio siti Web e servizi Web, possono quindi registrarsi facilmente con il server federativo e utilizzare i token emessi per l'autenticazione e il controllo di accesso.  
  
Negli scenari in cui è necessario fornire agli utenti l'accesso a più applicazioni o servizi federati, quando ogni applicazione o servizio è ospitato da un'organizzazione diversa, è possibile configurare il server federativo partner account in modo che sia possibile distribuire più relying party.  
  
Per ulteriori informazioni su come installare e configurare un'organizzazione partner account, vedere [Checklist: Configurazione dell'organizzazione partner account @ no__t-0.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Rivedere il ruolo del server federativo nel partner account](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)  
  
-   [Rivedere il ruolo del proxy server federativo nel partner account](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Account-Partner.md)  
  
-   [Preparare i computer client nel partner account](Prepare-Client-Computers-in-the-Account-Partner.md)  
  
## <a name="see-also"></a>Vedere anche
[Guida alla progettazione di AD FS in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
