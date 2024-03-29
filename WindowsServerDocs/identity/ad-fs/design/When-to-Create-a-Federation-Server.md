---
ms.assetid: 824005ae-c3c1-459b-9baa-1660158918ab
title: Quando creare un server federativo
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 91c260dad1bd260a7dad7320fecd15e6472c50a3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407889"
---
# <a name="when-to-create-a-federation-server"></a>Quando creare un server federativo

Quando si crea un server federativo Active Directory Federation Services \(AD FS @ no__t-1, si fornisce un mezzo con cui l'organizzazione può:  
  
-   Per la comunicazione basata su Web single @ no__t-0sign @ no__t-1Sulla Barra \(SSO @ no__t-3, con un'altra organizzazione \(that dispone anche di almeno un server federativo @ no__t-5 e, quando necessario, con i dipendenti dell'organizzazione \(who Need accesso tramite Internet @ no__t-7.  
  
-   Abilitare i servizi front-end per rappresentare utenti nei servizi di infrastruttura tramite la delega di identità. Per altre informazioni, vedere [When to Use Identity Delegation](When-to-Use-Identity-Delegation.md).  
  
Nelle sezioni seguenti vengono descritte alcune delle decisioni chiave per determinare quando e dove creare uno o più server federativi.  
  
## <a name="determine-the-organizational-role-for-the-federation-server"></a>Determinare il ruolo dell'organizzazione per il server federativo  
Per prendere una decisione consapevole su quando creare un nuovo server federativo, è necessario innanzitutto determinare in quale organizzazione risiederà il server. Il ruolo svolto da un server federativo in un'organizzazione varia a seconda che si inserisca il server federativo nell'organizzazione partner account o nell'organizzazione partner risorse.  
  
Quando un server federativo si trova nella rete aziendale del partner account, il suo ruolo consiste nell'autenticare le credenziali utente del browser, del servizio Web o dei client del selettore di identità e inviare i token di sicurezza ai client. Per altre informazioni, vedere [rivedere il ruolo del Server federativo nel Partner Account](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md).  
  
Quando un server federativo si trova nella rete aziendale del partner risorse, il suo ruolo consiste nell'autenticare gli utenti, in base a un token di sicurezza emesso da un server federativo nell'organizzazione partner risorse, oppure il suo ruolo consiste nel reindirizzare le richieste di token da applicazioni Web o servizi Web configurati all'organizzazione partner account a cui appartiene il client. Per altre informazioni, vedere [rivedere il ruolo del Server federativo nel Partner risorse](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md).  
  
## <a name="determine-which-ad-fs-design-to-deploy"></a>Determinare quale progettazione di AD FS distribuire  
I server federativi vengono creati nell'organizzazione ogni volta che si desidera distribuire uno dei seguenti tipi di AD FS:  
  
-   [Progetto di Web SSO](Web-SSO-Design.md)  
  
-   [Progetto di Web SSO federativo](Federated-Web-SSO-Design.md)  
  
Se necessario, un'organizzazione che distribuisce un progetto Web SSO federativo può configurare un singolo server federativo in modo che agisca sia nel ruolo partner account che nel ruolo di partner risorse. In questo caso, il server federativo può produrre token Security Assertion Markup Language \(SAML @ no__t-1, in base agli account utente nella propria organizzazione, o reindirizzare le richieste di token all'organizzazione, in base alla posizione in cui risiedono gli account degli utenti.  
  
> [!NOTE]  
> Per il progetto SSO Web federativo, deve essere presente almeno un server federativo nel partner account e almeno un server federativo nel partner risorse.  
  
## <a name="differences-between-a-federation-server-and-a-federation-server-proxy"></a>Differenze tra un server federativo e un proxy server federativo  
Un server federativo può utilizzare le pagine Web per Sign @ no__t-0cm, Policy, Authentication e Discovery nello stesso modo in cui viene utilizzato da un proxy server federativo. Le principali differenze tra un server federativo e un proxy server federativo riguardano le operazioni che un server federativo può eseguire che un proxy server federativo non è in grado di eseguire.  
  
Di seguito sono riportate le operazioni che possono essere eseguite solo da un server federativo:  
  
-   Il server federativo esegue le operazioni di crittografia che producono il token. Sebbene i proxy server federativi non possano produrre token, possono essere usati per indirizzare o reindirizzare i token ai client e, quando necessario, di nuovo al server federativo. Per ulteriori informazioni sull'utilizzo dei server federativi, vedere [quando creare un proxy server federativo](When-to-Create-a-Federation-Server-Proxy.md).  
  
-   I server federativi supportano l'uso dell'autenticazione integrata di Windows per i client nella rete aziendale. i proxy server federativi non lo sono. Per ulteriori informazioni sull'utilizzo dell'autenticazione integrata di Windows con il server federativo, vedere [quando creare una server farm federativa](When-to-Create-a-Federation-Server-Farm.md).  
  
> [!CAUTION]  
> La comunicazione tra server federativi e database di configurazione di SQL Server, archivi di attributi di SQL Server, controller di dominio e istanze di AD LDS non offre protezione dell'integrità o della riservatezza per impostazione predefinita. Per ridurre questo inconveniente, valutare la possibilità di proteggere il canale di comunicazione tra questi server usando IPSEC o una connessione fisicamente sicura tra tutti questi server. Per la comunicazione tra i server federativi e i server SQL, valutare l'uso della protezione SSL nella stringa di connessione. Per le connessioni tra server federativi e i controller di dominio, valutare la possibilità di attivare la firma e la crittografia Kerberos. Per LDAP, LDAP @ no__t-0 non è supportato per AD LDS @ no__t-1AD DS.  
  
## <a name="how-to-create-a-federation-server"></a>Come creare un server federativo  
È possibile creare un server federativo utilizzando la configurazione guidata server federativo di AD FS o lo strumento Fsconfig. exe comando @ no__t-0line. Quando si usa uno di questi strumenti, è possibile selezionare una qualsiasi delle opzioni seguenti per un server federativo.  
  
-   Creare un supporto\-server federativo da solo  
  
    Per ulteriori informazioni su come configurare un server federativo stand @ no__t-0alone, vedere la pagina relativa alla [creazione di un server federativo](../../ad-fs/deployment/Create-a-Stand-Alone-Federation-Server.md)autonomo.  
  
-   Creare il primo server federativo in una server farm federativa  
  
    Per altre informazioni su come configurare il primo server federativo o aggiungere un server federativo a una farm, vedere [creare il primo Server federativo in una Server Farm federativa](../../ad-fs/deployment/Create-the-First-Federation-Server-in-a-Federation-Server-Farm.md).  
  
-   Aggiungere un server federativo a una server farm federativa  
  
    Per altre informazioni su come aggiungere un server federativo a una farm, vedere [aggiungere un Server federativo a una Server Farm federativa](../../ad-fs/deployment/Add-a-Federation-Server-to-a-Federation-Server-Farm.md).  
  
Per altre informazioni su come funziona ciascuna di queste opzioni, vedere [il ruolo del Database di configurazione AD FS](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md).  
  
Per ulteriori informazioni su come configurare tutti i prerequisiti necessari per distribuire un server federativo, vedere [Checklist: Configurazione di un server federativo @ no__t-0.  
  
## <a name="see-also"></a>Vedere anche
[Guida alla progettazione di AD FS in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

