---
title: Risolvere i problemi relativi al monitoraggio di computer in Windows Server Essentials
description: Viene descritto come utilizzare Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f1e6b377-4a24-4d28-9b25-05910914826b
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1adf8ae2dd8763d0bc5a514609bb2470de6acde4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436077"
---
# <a name="troubleshoot-computer-monitoring-in-windows-server-essentials"></a>Risolvere i problemi relativi al monitoraggio di computer in Windows Server Essentials

>Si applica a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

In questo argomento contiene informazioni sulla risoluzione dei problemi riscontrati durante il monitoraggio dello stato di integrità del computer nel Visualizzatore avvisi e tramite le notifiche di posta elettronica in Windows Server Essentials.  
  
> [!NOTE]
>  Per informazioni aggiornate sulla risoluzione dei problemi dalla community di Windows Server Essentials, si consiglia di visitare il [Forum di Windows Server Essentials](https://social.technet.microsoft.com/Forums/winserveressentials/threads). Il forum di Windows Server Essentials è ideale per cercare informazioni o per porre una domanda.  
  
##  <a name="BKMK_TS"></a> Risoluzione dei problemi relativi a notifiche di posta elettronica per gli avvisi  
 In questa sezione sono elencati i vari problemi che possono verificarsi quando si usano le notifiche di posta elettronica per gli avvisi.  
  
### <a name="cannot-send-the-test-email-for-the-alert"></a>Non è possibile inviare il messaggio di posta elettronica di prova per l'avviso  
 **Problema** si verifica un errore messaggio non è possibile inviare il messaggio di prova per l'avviso.  
  
 **Causa** L'errore può essere dovuto a uno dei problemi seguenti nelle impostazioni relative alle notifiche di avviso:  
  
- Il nome del server SMTP o il numero di porta non è corretto.  
  
- È stato specificato erroneamente che il server SMTP richiede una connessione SSL.  
  
- Il server SMTP richiede l'autenticazione e sono state immesse credenziali errate.  
  
  **Soluzioni** Correggere gli eventuali errori nelle impostazioni delle notifiche di posta elettronica.  
  
##### <a name="to-identify-issues-in-your-email-notification-settings"></a>Per identificare eventuali problemi nelle impostazioni delle notifiche di posta elettronica  
  
-   Rivolgersi al proprio provider di servizi Internet (ISP) per informazioni sul nome del server SMTP, il numero di porta e l'uso di SSL.  
  
-   Esaminare i file di log per le notifiche di posta elettronica relative all'avviso nel server, nel percorso seguente:  
  
     %ProgramData%\Microsoft\Windows Server\Logs\SharedServiceHost-AlertServiceConfig.log  
  
    > [!TIP]
    >  Per vedere la cartella ProgramData è necessario visualizzare gli elementi nascosti. Se non trovi la cartella ProgramData, della barra multifunzione **View** nella scheda il **Mostra/Nascondi** gruppo, selezionare il **elementi nascosti** casella di testo.  
  
##### <a name="to-update-your-email-notification-setup-for-alerts"></a>Per aggiornare la configurazione delle notifiche di posta elettronica per gli avvisi  
  
1.  Nel dashboard fare clic su qualsiasi icona di avviso nell'angolo superiore destro per aprire il Visualizzatore avvisi.  
  
2.  Nella parte inferiore del Visualizzatore avvisi fare clic su **Configura notifiche di posta elettronica per gli avvisi**.  
  
3.  Nella finestra di dialogo **Configura notifiche di posta elettronica per gli avvisi** fare clic su **Abilita**.  
  
4.  Nella finestra di dialogo **Impostazioni SMTP** aggiornare le impostazioni e fare clic su **OK**.  
  
5.  Per testare le impostazioni aggiornate, fare clic su **Applica e invia posta elettronica**.  
  
6.  Dopo avere verificato il corretto invio del messaggio di posta elettronica di prova, fare clic su **OK** per salvare le impostazioni aggiornate.  
  
### <a name="test-email-notification-does-not-list-any-alerts"></a>La notifica di posta elettronica di prova non contiene avvisi  
 **Problema** Le notifiche di posta elettronica di prova per gli avvisi non contengono avvisi, anche se il Visualizzatore avvisi ne contiene.  
  
 **Soluzione** Non tutti gli avvisi segnalati nel Visualizzatore avvisi generano una notifica tramite posta elettronica. Solo gli avvisi configurati per eseguire l'escalation come notifica di posta elettronica all'interno dei relativi file di definizione dell'integrità vengono inviati come messaggi di posta elettronica ai destinatari specificati.  
  
 Quando si fa clic su **Applica e invia posta elettronica**, si riceve in genere una notifica di posta elettronica di esempio, senza che siano elencati avvisi. Se tuttavia durante il processo di test viene identificato un avviso di stato configurato per l'invio di una notifica di posta elettronica, l'avviso sarà incluso nel messaggio di posta elettronica di prova.  
  
### <a name="active-alerts-are-displayed-for-an-uninstalled-application"></a>Vengono visualizzati avvisi attivi per un'applicazione disinstallata  
 **Problema** Vengono visualizzati avvisi attivi per un'applicazione, anche se l'applicazione e il file di definizione dell'integrità sono stati disinstallati.  
  
 **Soluzione** È necessario eliminare manualmente gli avvisi attivi dell'applicazione disinstallata. Per eliminare un avviso, eseguire le operazioni seguenti.  
  
##### <a name="to-delete-an-alert-from-the-server-by-using-the-dashboard"></a>Per eliminare un avviso dal server tramite il dashboard  
  
1.  Dal server, aprire il dashboard.  
  
2.  Nel riquadro di spostamento fare clic su una delle icone di avviso visualizzate (messaggio critico, di avviso o informativo). Verrà avviato il Visualizzatore avvisi.  
  
3.  Nel Visualizzatore avvisi fare clic con il pulsante destro del mouse sull'avviso da eliminare, quindi scegliere **Elimina avviso**.
