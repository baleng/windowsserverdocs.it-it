---
title: Monitorare il carico esistente nel server di accesso remoto
description: Questo argomento fa parte della Guida per il monitoraggio e l'accounting di accesso remoto in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 62fa2895-62ae-42cf-817c-53e06ac2a26c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 43c447205a5ef0cbd33b0486e01d630e6d00c633
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71367225"
---
# <a name="monitor-the-existing-load-on-the-remote-access-server"></a>Monitorare il carico esistente nel server di accesso remoto

>Si applica a: Windows Server (Canale semestrale), Windows Server 2016

**Nota:** Windows Server 2012 riunisce DirectAccess e il servizio Routing e Accesso remoto (RRAS) in un singolo ruolo Accesso remoto.  
  
Il termine **Load** indica le statistiche correlate al numero di connessioni nel server di accesso remoto. Di seguito sono riportati i passaggi necessari per tenere traccia del carico sul server di accesso remoto.  
  
È possibile utilizzare il dashboard di monitoraggio disponibile nella console di gestione del server di accesso remoto per visualizzare le statistiche di caricamento per il server oppure utilizzare i contatori di performance monitor per tenere traccia delle statistiche.  
  
> [!NOTE]  
> È necessario essere connessi come membro del gruppo Domain Admins o un membro del gruppo Administrators su ciascun computer per completare le attività descritte in questo argomento. Se è possibile completare un'attività mentre si è connessi con un account membro del gruppo Administrators, provare a eseguire l'attività mentre si è connessi con un account membro del gruppo Domain Admins.  
  
#### <a name="to-use-the-monitoring-dashboard-to-monitor-the-remote-access-server-load"></a>Per utilizzare il dashboard di monitoraggio per monitorare il carico del server di accesso remoto  
  
1.  In **Server Manager**, fare clic su **strumenti**, quindi fare clic su **Gestione accesso remoto**.  
  
2.  Fare clic su **DASHBOARD** per passare a **Dashboard di Accesso remoto** nella **console di gestione di Accesso remoto**.  
  
3.  Nel dashboard di monitoraggio, notare il riquadro **stato client remoto** nel riquadro **stato server** . In questo riquadro sono elencate le statistiche, ad esempio il numero totale di client remoti connessi, il numero totale di client DirectAccess connessi e il numero massimo di utenti connessi nelle ultime 24 ore.  
  
4.  È possibile fare clic su **Aggiorna** in **attività** nel riquadro destro per ricaricare lo stato di integrità. Per modificare l'intervallo di aggiornamento predefinito, fare clic su **Configura intervallo di aggiornamento** in **attività**.  
  
#### <a name="to-use-the-performance-monitor-tool-to-monitor-performance-counters-on-the-remote-access-server"></a>Per utilizzare lo strumento Performance Monitor per monitorare i contatori delle prestazioni nel server di accesso remoto  
  
1.  Fare clic sul pulsante **Start**, scegliere **strumenti di amministrazione**, quindi fare doppio clic su **Performance Monitor**.  
  
2.  In **prestazioni**fare clic su **Performance Monitor**.  
  
3.  Nella barra degli strumenti di **Performance Monitor** fare clic sul pulsante **Aggiungi** (indicato da un'icona a forma di verde).  
  
4.  Dall'elenco dei **contatori disponibili**selezionare tutti i contatori nelle categorie **RAS** e **RAmgmtsvc** , quindi fare clic su **Aggiungi > >** .  
  
5.  Anche in questo caso, nell'elenco dei **contatori disponibili**selezionare tutti i contatori nella categoria **connessioni IPSec** , quindi fare clic su **Aggiungi > >.**  
  
6.  Fare clic su **OK** per aggiungere i contatori selezionati nella console di **Performance Monitor** per il rilevamento.  
  
In **Performance Monitor** verranno ora visualizzate graficamente le statistiche di carico del server selezionate.  
  
](../../../media/Monitor-the-existing-load-on-the-Remote-Access-server/PowerShellLogoSmall.gif)***<em>comandi equivalenti</em> di PowerShell per Windows PowerShell @no__t 0Windows***  
  
Il cmdlet o i cmdlet di Windows PowerShell seguenti eseguono la stessa funzione della procedura precedente. Immettere ogni cmdlet in una singola riga, anche se qui può sembrare che siano divisi su più righe a causa di vincoli di formattazione.  
  
```  
PS> Get-RemoteAccessConnectionStatisticsSummary  
```  
  


