---
ms.assetid: 663a2482-33d1-4c19-8607-2e24eef89fcb
title: Server farm federativa che usa Database interno di Windows
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f0f3d8c70a41d512e7cd33282524bc401ce84600
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191426"
---
# <a name="federation-server-farm-using-wid"></a>Server farm federativa che usa Database interno di Windows

La topologia predefinita per Active Directory Federation Services \(ADFS\) è una server farm federativa, utilizzare Database interno di Windows \(WID\), costituito da un massimo di cinque server federativi ospitano il Servizio federativo dell'organizzazione. In questa topologia, ADFS utilizza WID come archivio per il database di configurazione di ADFS per tutti i server federativi che sono connessi alla farm. La farm replica e mantiene i dati del servizio federativo nel database di configurazione di tutti i server della farm.  
  
La creazione del primo server federativo in una farm crea anche un nuovo servizio federativo. Quando si usa database interno di Windows per il database di configurazione di ADFS, il primo server federativo che si crea la farm è detto il *server federativo primario*. Ciò significa che il computer è configurato con un'operazione di lettura\/scrivere copia del database di configurazione di AD FS.  
  
Tutti gli altri server di federazione configurato per questa farm vengono dette *i server federativi secondari* poiché devono replicare tutte le modifiche apportate nel server federativo primario per la lettura\-solo copie del database di configurazione di ADFS che memorizzano localmente.  
  
> [!NOTE]  
> È consigliabile utilizzare almeno due server federativi in un carico\-configurazione bilanciato.  
  
## <a name="deployment-considerations"></a>Considerazioni sulla distribuzione  
Questa sezione vengono descritte varie considerazioni sui destinatari, vantaggi e limitazioni di cui è associate a questa topologia di distribuzione.  
  
### <a name="who-should-use-this-topology"></a>Chi dovrebbe utilizzare questa topologia?  
  
-   Le organizzazioni con un massimo di 100 relazioni di trust configurato che è necessario fornire agli utenti interni \(connesso al computer connessi fisicamente alla rete aziendale\) con single sign-\-in \(SSO\) accesso alle applicazioni federate o servizi  
  
-   Organizzazioni che desiderano offrire agli utenti interni di accesso SSO a Microsoft Online Services o Microsoft Office 365  
  
-   Organizzazioni di piccole dimensioni che richiedono servizi scalabili ridondanti  
  
> [!NOTE]  
> Le organizzazioni con database di dimensioni superiori considerare l'uso di [Federation Server Farm utilizzando SQL Server](Federation-Server-Farm-Using-SQL-Server.md) topologia di distribuzione, verrà illustrata più avanti in questa sezione. Devono prendere in considerazione le organizzazioni con utenti che accedono dall'esterno della rete utilizzando il [Federation Server Farm utilizzando WID e proxy](Federation-Server-Farm-Using-WID-and-Proxies.md) topologia o [Federation Server Farm utilizzando SQL Server](Federation-Server-Farm-Using-SQL-Server.md) topologia.  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Quali sono i vantaggi dell'utilizzo di questa topologia?  
  
-   Fornisce l'accesso SSO per gli utenti interni  
  
-   La ridondanza dei dati e del servizio federativo \(ciascun server federativo replica le modifiche in altri server federativi nella stessa farm\)  
  
-   La farm può essere ampliata aggiungendo fino a cinque server federativi  
  
-   Database interno di Windows è incluso in Windows; Pertanto, non è necessario per l'acquisto di SQL Server  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Quali sono le limitazioni dell'utilizzo di questa topologia?  
  
-   Una farm WID ha un limite di cinque server federativi. Per altre informazioni, vedere [Considerazioni sulla topologia di distribuzione di ADFS](AD-FS-Deployment-Topology-Considerations.md).  
  
-   Una farm database interno di Windows non supporta la risoluzione di rilevamento o elemento riproduzione token \(fa parte di Security Assertion Markup Language \(SAML\) protocollo\).  
  
## <a name="server-placement-and-network-layout-recommendations"></a>Consigli di layout posizionamento e la rete di server  
Si è pronti per iniziare a distribuire la topologia della rete, è necessario pianificare la collocazione di tutti i server federativi della rete aziendale dietro un bilanciamento del carico di rete \(Bilanciamento carico di RETE\) host che può essere configurato per un cluster di bilanciamento carico di RETE con un cluster dedicato Domain Name System \(DNS\) indirizzo IP del cluster e nome.  
  
> [!NOTE]  
> Questo nome DNS del cluster deve corrispondere al nome servizio federativo, ad esempio, fs.fabrikam.com.  
  
L'host di bilanciamento carico di RETE può utilizzare le impostazioni definite in questo cluster NLB per allocare le richieste client per i server federativi singoli. La figura seguente mostra come la società fittizia Fabrikam, Inc., imposta la prima fase della relativa distribuzione tramite due\-server farm federativa computer \(fs1 e fs2\) con WID e il collocamento di un server DNS e un singolo host di bilanciamento carico di RETE che è collegato alla rete aziendale.  
  
![server farm con database interno di Windows](media/FarmWID.gif)  
  
> [!NOTE]  
> Se si verifica un errore in questo host NLB singolo, gli utenti non saranno in grado di accedere alle applicazioni federate o servizi. Se i propri requisiti aziendali non consentono un singolo punto di errore, aggiungere altri host NLB.  
  
Per ulteriori informazioni su come configurare l'ambiente di rete per l'utilizzo con i server federativi, vedere [requisiti di risoluzione dei nomi per i server federativi](Name-Resolution-Requirements-for-Federation-Servers.md) nella Guida alla progettazione di ADFS.  
  
## <a name="see-also"></a>Vedere anche
[Guida alla progettazione di AD FS in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)