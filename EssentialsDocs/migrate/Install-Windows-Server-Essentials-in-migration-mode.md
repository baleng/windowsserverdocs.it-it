---
title: Installare Windows Server Essentials in modalità 1 della migrazione
description: Viene descritto come utilizzare Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fd7196ac-cfa6-46a5-ba77-6962b47a825e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 74c40cc0f06d73a922a3d7fb819f7e71b47ac088
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432961"
---
# <a name="install-windows-server-essentials-in-migration-mode1"></a>Installare Windows Server Essentials in modalità 1 della migrazione

>Si applica a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

È possibile avere un solo server sulla rete che esegue Windows Server Essentials e tale server deve essere un controller di dominio per la rete.  
  
 Quando si installa Windows Server Essentials in modalità di migrazione, l'installazione guidata esegue le attività seguenti:  
  
1.  Installa e configura il software del server Windows Server Essentials nel Server di destinazione.  
  
2.  Aggiorna lo schema del dominio alla versione più recente.  
  
3.  Aggiunge il server di destinazione al dominio esistente. Il server di origine e quello di destinazione possono essere entrambi membri dello stesso dominio fino al termine del processo di migrazione. Al termine della migrazione, è necessario rimuovere il server di origine dalla rete entro 21 giorni.  
  
    > [!WARNING]
    >  Un messaggio di errore viene aggiunto al registro eventi ogni giorno durante il periodo di prova di 21 giorni finché non si rimuove il server-di origine dalla rete. Il testo del messaggio è "Controllo del ruolo FSMO: rilevato ambiente non conforme al criterio di gestione licenze. Il server di gestione deve rivestire i ruoli di controller di dominio primario e di master per la denominazione dei domini in Active Directory. Trasferire questi ruoli Active Directory al server di gestione. Il server verrà automaticamente arrestato se il problema non viene risolto entro 21 giorni dal momento in cui è stata rilevata questa condizione". Dopo il periodo di prova di 21 giorni, il server di origine verrà arrestato.  
  
4.  Trasferisce i ruoli di master operazioni (noto anche come FSMO, Flexible Single Master Operation) dal server di origine a quello di destinazione. I ruoli di master operazioni sono specializzati nelle attività del controller di dominio che vengono usate quando i metodi standard di trasferimento dati e aggiornamento si rivelano inadeguati. Quando un server di destinazione diventa controller di dominio, deve contenere i ruoli di master operazioni.  
  
5.  Configura il server di destinazione come server di catalogo globale. Il server di catalogo globale è un controller di dominio che gestisce un archivio di dati distribuiti. Contiene una rappresentazione parziale e ricercabile di ogni oggetto in ogni dominio della foresta di Active Directory.  
  
6.  Configura il server di destinazione come server licenze del tipo "site license".  
  
##  <a name="BKMK_Install"></a> Installare Windows Server Essentials nel Server di destinazione  
 Per installare e configurare Windows Server Essentials nel Server di destinazione in modalità di migrazione, eseguire la procedura seguente.  
  
#### <a name="to-install-windows-server-essentials-on-the-destination-server"></a>Per installare Windows Server Essentials nel Server di destinazione  
  
1. Attivare il Server di destinazione e inserire l'unità DVD di Windows Server Essentials DVD1. Se viene visualizzato un messaggio che chiede se si vuole avviare da un CD o DVD, premere un tasto qualsiasi.  
  
   > [!NOTE]
   >  Se il Server di destinazione supporta l'avvio da un'unità flash USB, è possibile usare la **strumento di Download USB/DVD di Windows 7** per creare un'unità Flash USB avviabile dal file ISO di Windows Server Essentials. Con un'unità flash USB è possibile velocizzare notevolmente il processo di installazione perché le unità flash leggono i dati molto più rapidamente delle unità DVD-ROM. Dopo aver creato un'unità flash USB di avvio, è possibile aggiungere un file di risposte nell'unità flash. È possibile [scaricare lo strumento di Download USB/DVD di Windows 7](https://go.microsoft.com/fwlink/p/?LinkId=248282) gratuito sul sito Web di Microsoft Store.  
  
   > [!NOTE]
   >  Se il server di destinazione non viene avviato dal DVD, riavviare il computer e controllare le impostazioni del BIOS per verificare che **DVD-ROM** sia elencato per primo nella sequenza di avvio. Per altre informazioni su come cambiare la sequenza di avvio delle impostazioni del BIOS, vedere la documentazione del produttore hardware.  
  
2. Fare clic su **Nuova installazione**.  
  
3. Se un'unità disco rigido interna non è visualizzata nell'elenco, fare clic su **Carica driver** e installare il driver necessario prima di continuare.  
  
4. Selezionare la casella di controllo per eliminare tutti i file e le cartelle sull'unità disco rigido primaria e quindi fare clic su **Installa**.  
  
5. Nella pagina **Scegli modalità di installazione server** fare clic su **Migrazione del server** e quindi immettere le informazioni sulla migrazione richieste.  
  
6. Quando viene visualizzato un messaggio simile a **Migrazione del server completata** , fare clic su **Chiudi**.  
  
   Al termine dell'installazione, si accede automaticamente con l'account utente amministratore e la password specificati nel file di risposte della migrazione.  
  
> [!NOTE]
>  Per sbloccare il desktop durante l'installazione di Windows Server Essentials, usare l'account predefinito administrator e lasciare vuota la password.  
  
##  <a name="BKMK_VerifyTheHealthOfDC"></a> Verificare l'integrità del controller di dominio  
 Prima di procedere con la migrazione, è necessario assicurarsi che il controller di dominio e la rete di Windows Server Essentials siano integri.  
  
 Nella tabella seguente sono indicati gli strumenti che è possibile usare per diagnosticare eventuali problemi nel server di destinazione, nella rete e nel dominio:  
  
|Strumento|Descrizione|  
|----------|-----------------|  
|Netdiag|Consente di isolare problemi di rete e di connettività. Per altre informazioni e per scaricare lo strumento, vedere [Netdiag](https://go.microsoft.com/fwlink/?LinkId=217388).|  
|Dcdiag.exe|Analizza lo stato dei controller di dominio in una foresta o in un'organizzazione e segnala i problemi per facilitarne la risoluzione. Per altre informazioni e per scaricare lo strumento, vedere [Dcdiag](https://go.microsoft.com/fwlink/?LinkId=217389).|  
|Repadmin.exe|Consente di diagnosticare i problemi di replica tra controller di dominio. Questo strumento richiede l'esecuzione dei parametri della riga di comando. Per altre informazioni e per scaricare lo strumento, vedere [Repadmin](https://go.microsoft.com/fwlink/?LinkId=217387).|  
  
 Prima di procedere con la migrazione, è necessario correggere tutti i problemi segnalati da questi strumenti.  
  
> [!NOTE]
>  Se si prevede di eseguire la migrazione di posta elettronica a un altro server di Exchange in locale, vedere [integrare un Server di Exchange On-Premises con Windows Server Essentials](../manage/Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md) per informazioni su come configurare il server di Exchange in locale.
