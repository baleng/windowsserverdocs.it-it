---
title: Abbassare di livello e rimuovere il Server di origine dal nuovo network1 di Windows Server Essentials
description: Viene descritto come utilizzare Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d9f18b29-8e03-439e-bdf0-1dac5e4f70c5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e5bcdd58f4d88f7a555151d755bf427ecc9b5108
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433007"
---
# <a name="demote-and-remove-the-source-server-from-the-new-windows-server-essentials-network1"></a>Abbassare di livello e rimuovere il Server di origine dal nuovo network1 di Windows Server Essentials

>Si applica a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Dopo aver finito di installare Windows Server Essentials e aver completato le attività della migrazione guidata, è necessario eseguire le attività seguenti:  
  

1.  [Disinstallare Exchange Server 2003](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_UninstallExchangeServer2003).  
  
2.  [Disconnettere le stampanti direttamente connesse al server di origine](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_PhysicallyDisconnect).  
  
3.  [Abbassare di livello il server di origine](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_DemoteTheSourceServer).  
  
4.  [Spostare il ruolo Server DHCP dal Server di origine al router](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_MoveTheDHCPRole).  
  
5.  [Rimuovere e reimpiegare il server di origine](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer).  

1.  [Disinstallare Exchange Server 2003](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_UninstallExchangeServer2003).  
  
2.  [Disconnettere le stampanti direttamente connesse al server di origine](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_PhysicallyDisconnect).  
  
3.  [Abbassare di livello il server di origine](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_DemoteTheSourceServer).  
  
4.  [Spostare il ruolo Server DHCP dal Server di origine al router](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_MoveTheDHCPRole).  
  
5.  [Rimuovere e reimpiegare il server di origine](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer).  

  
###  <a name="BKMK_UninstallExchangeServer2003"></a> Disinstallare Exchange Server 2003  
  
> [!IMPORTANT]
>  Se si aggiungono gli account utente dopo aver spostato le cassette postali al Server di destinazione e prima di disinstallare Exchange Server 2003 dal Server di origine, le cassette postali vengono aggiunte nel Server di origine. Questo comportamento è da progettazione. È necessario spostare le cassette postali nel server di destinazione per tutti gli account utente aggiunti in questa fase. Ripetere le istruzioni riportate in cassette postali di Exchange Server spostare e le impostazioni per la migrazione a Windows Server Essentials prima di disinstallare Exchange Server 2003.  
  
 Prima di abbassarlo, è necessario disinstallare Exchange Server 2003 dal Server di origine. Questa operazione rimuove tutti i riferimenti in Active Directory Domain Services (AD DS) per Exchange Server nel Server di origine. È necessario disporre del supporto di Windows Small Business Server 2003 per rimuovere Exchange Server 2003.  
  
##### <a name="to-uninstall-exchange-server-2003-from-the-source-server"></a>Per disinstallare Exchange Server 2003 dal Server di origine  
  
1. Accedere al server di origine come amministratore.  
  
2. Fare clic su **Start**, su **Pannello di controllo** e infine su **Installazione applicazioni**.  
  
3. Nell'elenco dei programmi, selezionare **Windows Small Business Server 2003**, quindi fare clic su **Cambia/Rimuovi**.  
  
4. Nell'Installazione guidata fare clic su **Avanti** fino a visualizzare la pagina **Selezione componenti**.  
  
5. Nella pagina Selezione componenti espandere **Exchange Server** e quindi scegliere **Rimuovi**.  
  
   > [!NOTE]
   > 
   >  Exchange Server eseguirà una verifica per accertarsi che non ci siano cassette postali o cartelle pubbliche sul server. Se rimangono dei dati, viene visualizzato un messaggio di errore quando si fa clic su **Rimuovi**. Per evitare questo problema, assicurarsi di aver completato tutte le procedure riportate nell'argomento [SBS 2003 sposta impostazioni e i dati nel Server di destinazione](Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  
   > 
   >  Exchange Server eseguirà una verifica per accertarsi che non ci siano cassette postali o cartelle pubbliche sul server. Se rimangono dei dati, viene visualizzato un messaggio di errore quando si fa clic su **Rimuovi**. Per evitare questo problema, assicurarsi di aver completato tutte le procedure riportate nell'argomento [SBS 2003 sposta impostazioni e i dati nel Server di destinazione](../migrate/Move-Windows-SBS-2003-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  

  
6. Fare clic su **Avanti**.  
  
7. Quando richiesto, inserire Windows Small Business Server 2003 CD n. 3 e seguire le istruzioni visualizzate.  
  
###  <a name="BKMK_PhysicallyDisconnect"></a> Disconnettere le stampanti direttamente connesse al Server di origine  
 Prima di abbassare di livello il server di origine, scollegare fisicamente le stampanti direttamente connesse al server di origine e condivise con il server di origine. Verificare che non rimanga alcun oggetto Active Directory per le stampanti direttamente connesse al server di origine. Le stampanti possono quindi essere direttamente connesso al Server di destinazione e condivisi da Windows Server Essentials.  
  
###  <a name="BKMK_DemoteTheSourceServer"></a> Abbassare di livello il Server di origine  
 Prima di abbassare di livello il server di origine dal ruolo del controller di dominio di Servizi di dominio Active Directory al ruolo di un server membro di dominio, verificare che le impostazioni di Criteri di gruppo siano applicate a tutti i computer client, come descritto nella procedura seguente.  
  
> [!IMPORTANT]
>  Il server di origine e il server di destinazione devono essere connessi alla rete mentre le modifiche a Criteri di gruppo vengono aggiornate nei computer client.  
  
##### <a name="to-force-a-group-policy-update-on-a-client-computer"></a>Per forzare un aggiornamento di Criteri di gruppo in un computer client  
  
1.  Accedere al computer client come amministratore.  
  
2.  Aprire una finestra del prompt dei comandi come amministratore.  
  
3.  Al prompt dei comandi digitare **gpupdate /force**, quindi premere INVIO.  
  
4.  Per completare il processo, potrebbe essere necessario disconnettersi e riconnettersi. Fare clic su **Sì** per confermare.  
  
##### <a name="to-demote-the-source-server"></a>Per abbassare di livello il server di origine  
  
1. Nel server di origine fare clic su **Start**, scegliere **Esegui**, digitare **dcpromo** e quindi fare clic su **OK**.  
  
2. Fare clic due volte su **Avanti** .  
  
   > [!NOTE]
   >  Non selezionare **Questo server è l'ultimo controller di dominio nel dominio**.  
  
3. Digitare una password per il nuovo account amministratore sul server e quindi fare clic su **Avanti**.  
  
4. Nel **riepilogo** nella finestra di dialogo si viene informati che verranno rimossi dal computer di Active Directory Domain Services e che il server diventerà membro del dominio. Fare clic su **Avanti**.  
  
5. Scegliere **Fine**. Il server di origine viene riavviato.  
  
6. Dopo che il server di origine è stato riavviato, aggiungerlo come membro di un gruppo di lavoro prima di disconnetterlo dalla rete.  
  
   Dopo aver aggiunto il server di origine come membro di un gruppo di lavoro e averlo disconnesso dalla rete, è necessario rimuoverlo da Servizi di dominio Active Directory sul server di destinazione.  
  
##### <a name="to-remove-the-source-server-from-active-directory"></a>Per rimuovere il server di origine da Active Directory  
  
1.  Nel server di destinazione aprire **Utenti e computer di Active Directory**.  
  
2.  Nella console di **Utenti e computer di Active Directory** espandere il nome di dominio e quindi fare clic su **Computer**.  
  
3.  Fare clic con il pulsante destro del mouse sul nome del server di origine se esiste ancora nell'elenco di server, scegliere **Elimina** e quindi fare clic su **Sì**.  
  
4.  Verificare che il server di origine non sia nell'elenco e quindi chiudere **Utenti e computer di Active Directory**.  
  
###  <a name="BKMK_MoveTheDHCPRole"></a> Spostare il ruolo Server DHCP dal Server di origine al router  
  
> [!NOTE]
> 
>  Se questa attività è già stata eseguita prima di avviare il processo di migrazione, continuare con la sezione [Rimuovere e reimpiegare il server di origine](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer).  
> 
>  Se questa attività è già stata eseguita prima di avviare il processo di migrazione, continuare con la sezione [Rimuovere e reimpiegare il server di origine](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md#BKMK_RemoveTheSourceServer).  

  
 Se il server di origine esegue il ruolo DHCP, eseguire i passaggi seguenti per spostare il ruolo DHCP nel router.  
  
##### <a name="to-move-the-dhcp-role-from-the-source-server-to-the-router"></a>Per spostare il ruolo DHCP dal server di origine al router  
  
1.  Disattivare il servizio DHCP sul server di origine, nel modo seguente:  
  
    1.  Nel server di origine fare clic su **Start**, scegliere **Strumenti di amministrazione**e quindi fare clic su **Servizi**.  
  
    2.  Nell'elenco di servizi attualmente in esecuzione fare clic con il pulsante destro del mouse su **Windows Server** e quindi scegliere **Proprietà**.  
  
    3.  Per **Tipo di avvio**, selezionare **Disabilitato**.  
  
    4.  Arrestare il servizio.  
  
2.  Attivare il ruolo DHCP sul router  
  
    1.  Seguire le istruzioni della documentazione del router per attivare il ruolo DHCP sul router.  
  
    2.  Per essere certi che gli indirizzi IP rilasciati dal server di origine rimangano gli stessi, seguire le istruzioni della documentazione del router per configurare un intervallo DHCP sul router uguale a quello sul server di origine.  
  
    > [!IMPORTANT]
    >  Se non è stato configurato un IP statico o prenotazioni DHCP sul router per il server di destinazione e l'intervallo DHCP non è uguale a quello del server di origine, è possibile che il router rilascerà un nuovo indirizzo IP per il server di destinazione. In questo caso, reimpostare le regole di port forwarding del router per l'inoltro al nuovo indirizzo IP del server di destinazione.  
  
###  <a name="BKMK_RemoveTheSourceServer"></a> Rimuovere e reimpiegare il Server di origine  
 Spegnere il server di origine e scollegarlo dalla rete. È consigliabile non riformattare il server di origine per almeno una settimana per essere certi che la migrazione al server di destinazione di tutti i dati necessari sia stata eseguita. Dopo aver verificato che sia stata eseguita la migrazione di tutti i dati, è possibile reinstallare questo server nella rete come server secondario per altre attività, se necessario.  
  
> [!NOTE]
>  Dopo aver abbassato di livello e rimosso il server di origine, riavviare il server di destinazione.  
  
 Il server di origine, dopo essere stato abbassato di livello, non è in uno stato integro. Se si vuole reimpiegare il server di origine, il modo più semplice è riformattarlo, installare un sistema operativo server e quindi configurarlo per l'uso come server aggiuntivo.
