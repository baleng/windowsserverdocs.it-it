---
title: Client RADIUS
description: Questo argomento fornisce una panoramica dei client RADIUS per server dei criteri di rete in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: d3a09ac9-75f8-4f57-aab4-b0fdfe110118
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1dfc1bb71d2800a8a9587e54147950dfd7fb371f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71396004"
---
# <a name="radius-clients"></a>Client RADIUS

>Si applica a: Windows Server (Canale semestrale), Windows Server 2016

Un server di accesso alla rete \(NAS @ no__t-1 è un dispositivo che fornisce un certo livello di accesso a una rete più ampia. Un NAS che usa un'infrastruttura RADIUS è anche un client RADIUS, che invia le richieste di connessione e i messaggi di contabilità a un server RADIUS per l'autenticazione, l'autorizzazione e l'accounting.

>[!NOTE]
>I computer client, ad esempio computer portatili e altri computer che eseguono sistemi operativi client, non sono client RADIUS. I client RADIUS sono server di accesso alla rete, ad esempio punti di accesso wireless, commutatori di autenticazione 802.1 X, rete privata virtuale \(VPN @ no__t-1 server e server di connessione remota, perché utilizzano il protocollo RADIUS per comunicare con i server RADIUS, ad esempio come server dei criteri di rete \(NPS @ no__t-3 server.

Per distribuire NPS come server RADIUS o proxy RADIUS, è necessario configurare i client RADIUS in NPS.

## <a name="radius-client-examples"></a>Esempi di client RADIUS

Esempi di server di accesso alla rete sono:

- Server di accesso alla rete che forniscono la connettività di accesso remoto a una rete aziendale o a Internet. Un esempio è un computer che esegue il sistema operativo Windows Server 2016 e il servizio di accesso remoto che fornisce servizi di accesso remoto tradizionale o VPN (Virtual Private Network) a una Intranet dell'organizzazione.
- Punti di accesso wireless che forniscono accesso a livello fisico a una rete aziendale tramite tecnologie di trasmissione e ricezione basate su wireless.
- Opzioni che forniscono l'accesso a livello fisico alla rete di un'organizzazione, usando le tecnologie LAN tradizionali, ad esempio Ethernet.
- Proxy RADIUS che inoltrano le richieste di connessione ai server RADIUS che sono membri di un gruppo di server RADIUS remoto configurato sul proxy RADIUS.

## <a name="radius-access-request-messages"></a>Accesso RADIUS-messaggi di richiesta

I client RADIUS creano i messaggi di richiesta di accesso RADIUS e li trasmettono a un proxy RADIUS o a un server RADIUS oppure eseguono il inoltro dei messaggi di richiesta di accesso a un server RADIUS che hanno ricevuto da un altro client RADIUS ma non hanno creato se stessi.

I client RADIUS non elaborano i messaggi di richiesta di accesso eseguendo l'autenticazione, l'autorizzazione e l'accounting. Solo i server RADIUS eseguono queste funzioni.

NPS, tuttavia, può essere configurato sia come proxy RADIUS sia come server RADIUS simultaneamente, in modo che elabori alcuni messaggi di richiesta di accesso e inoltri altri messaggi.

## <a name="nps-as-a-radius-client"></a>Server dei criteri di server come client RADIUS

NPS funge da client RADIUS quando viene configurato come proxy RADIUS per l'inoltro dei messaggi di richiesta di accesso ad altri server RADIUS per l'elaborazione. Quando si usa NPS come proxy RADIUS, sono necessari i passaggi di configurazione generali seguenti:

1. I server di accesso alla rete, ad esempio punti di accesso wireless e server VPN, sono configurati con l'indirizzo IP del proxy NPS come server RADIUS designato o server di autenticazione. Questo consente ai server di accesso alla rete, che creano messaggi di richiesta di accesso in base alle informazioni ricevute dai client Access, di inviare messaggi al proxy NPS.

2. Il proxy NPS viene configurato aggiungendo ciascun server di accesso alla rete come client RADIUS. Questo passaggio di configurazione consente al proxy server dei criteri di rete di ricevere messaggi dai server di accesso alla rete e di comunicare con essi attraverso l'autenticazione. Inoltre, i criteri di richiesta di connessione nel proxy NPS sono configurati per specificare i messaggi di richiesta di accesso da inviare a uno o più server RADIUS. Questi criteri vengono configurati anche con un gruppo di server RADIUS remoti, che indica a server dei criteri di rete dove inviare i messaggi ricevuti dai server di accesso alla rete.

3. Il server dei criteri di gruppo o altri server RADIUS membri del gruppo di server RADIUS remoti sul proxy NPS sono configurati per la ricezione di messaggi dal proxy NPS. Questa operazione viene eseguita configurando il proxy NPS come client RADIUS.

## <a name="radius-client-properties"></a>Proprietà client RADIUS

Quando si aggiunge un client RADIUS alla configurazione server dei criteri di rete tramite la console server dei criteri di rete o tramite l'utilizzo dei comandi Netsh per NPS o i comandi di Windows PowerShell, si sta configurando NPS per la ricezione di messaggi di richiesta di accesso RADIUS da un server di accesso alla rete o da un Proxy RADIUS.

Quando si configura un client RADIUS in NPS, è possibile definire le proprietà seguenti:

### <a name="client-name"></a>Nome client

 Nome descrittivo per il client RADIUS, che consente di identificare più facilmente quando si utilizza lo snap-in NPS o i comandi Netsh per NPS.

### <a name="ip-address"></a>L'indirizzo IP

Il protocollo Internet versione 4 \(IPv4 @ no__t-1 o il Domain Name System \(DNS @ no__t-3 nome del client RADIUS.

### <a name="client-vendor"></a>Client-fornitore

Fornitore del client RADIUS. In caso contrario, è possibile utilizzare il valore standard RADIUS per client-fornitore.

### <a name="shared-secret"></a>Segreto condiviso

Stringa di testo utilizzata come password tra i client RADIUS, i server RADIUS e i proxy RADIUS. Quando si usa l'attributo Authenticator del messaggio, il segreto condiviso viene usato anche come chiave per crittografare i messaggi RADIUS. Questa stringa deve essere configurata nel client RADIUS e nello snap-in NPS.

### <a name="message-authenticator-attribute"></a>Attributo dell'autenticatore del messaggio

Descritto in RFC 2869, "RADIUS Extensions", a Message Digest 5 \(MD5 @ no__t-1 hash dell'intero messaggio RADIUS. Se è presente l'attributo dell'autenticatore del messaggio RADIUS, viene verificato. Se la verifica ha esito negativo, il messaggio RADIUS viene ignorato. Se le impostazioni client richiedono l'attributo Authenticator del messaggio e non sono presenti, il messaggio RADIUS viene ignorato. È consigliabile utilizzare l'attributo Authenticator del messaggio.

>[!NOTE]
>L'attributo Authenticator del messaggio è obbligatorio e abilitato per impostazione predefinita quando si usa l'autenticazione Extensible Authentication Protocol \(EAP @ no__t-1. 

Per ulteriori informazioni su NPS, vedere [Server dei criteri di rete (NPS)](nps-top.md).

