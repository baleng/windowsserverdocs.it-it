---
title: Sostituire l'URL dell'endpoint per acquisto/prova del modulo di integrazione O365 nell'assistenza per il contratto Microsoft Online Service Reseller Agreement
description: Viene descritto come utilizzare Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9860a6b9-baea-4bf0-9a9f-6f1a288f996e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: b690cedd2f692cc6d11af6e05dd0cd4b4ea5a1d6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833102"
---
# <a name="replace-o365-integration-module-buy-try-endpoint-url-in-support-of-microsoft-online-service-reseller-agreement"></a>Sostituire l'URL dell'endpoint per acquisto/prova del modulo di integrazione O365 nell'assistenza per il contratto Microsoft Online Service Reseller Agreement

>Si applica a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_O365"></a>   
 Se sei un partner di Microsoft Online Service rivenditore accordo (MOSRA), per garantire che le transazioni di iscrizione dei clienti siano elaborate mediante il portale, è necessario sostituire l'URL dell'endpoint usato dal modulo di integrazione di Office 365 di Windows Server Essentials.  
  
 Il modulo di integrazione utilizza i seguenti quattro URL dell’endpoint:  
  
1.  Un endpoint di acquisto per l’abbonamento a Office 365 Enterprise.  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   Tipo = REG-SZ  
  
    -   Nome chiave = MOSRASTDBUY  
  
    -   Valore = *xxxxx*, dove xxxxx è l’URL di acquisto abbonamento aziendale dell’utente. Ad esempio, valore = http://syndicatepartner.office365.com/enterprisebuy.html  
  
2.  Un endpoint di prova per l’abbonamento a Office 365 Enterprise.  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   Tipo = REG-SZ  
  
    -   Nome chiave = MOSRASTDTRY  
  
    -   Valore = *xxxxx*, dove xxxxx è l’URL di acquisto abbonamento aziendale dell’utente. Ad esempio, valore = http://syndicatepartner.office365.com/enterprisetry.html  
  
3.  Un endpoint di acquisto abbonamento Office 365 Small Business Premium.  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   Tipo = REG-SZ  
  
    -   Nome chiave = MOSRALITEBUY  
  
    -   Valore = *xxxxx*, dove xxxxx è l’URL di acquisto abbonamento aziendale dell’utente. Ad esempio, valore = http://syndicatepartner.office365.com/smallbizbuy.html  
  
4.  Endpoint versione di valutazione un abbonamento a Office 365 Small Business Premium.  
  
    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\MSO\  
  
    -   Tipo = REG-SZ  
  
    -   Nome chiave = MOSRALITETRY  
  
    -   Valore = *xxxxx*, dove xxxxx è l’URL di acquisto abbonamento aziendale dell’utente. Ad esempio, valore = http://syndicatepartner.office365.com/smallbiztry.html  
  
#### <a name="to-add-an-endpoint-url-key-to-the-registry"></a>Per aggiungere una chiave di URL dell’endpoint nel Registro di sistema  
  
1.  Nel computer di riferimento fare clic su **Start**, digitare **regedit** e quindi premere INVIO.  
  
2.  Nel riquadro a sinistra, espandere **HKEY_LOCAL_MACHINE**, espandere **SOFTWARE**, espandere **Microsoft**, espandere **Windows Server**, quindi espandere **MSO**.  
  
3.  Se MSO non esiste, fare clic con il pulsante destro del mouse su **Windows Server**, scegliere **Nuovo**, fare clic su **Chiave** e quindi digitare **MSO** come nome della chiave.  
  
4.  Fare clic con il tasto destro del mouse su MSO, quindi su **Valore stringa**. Digitare uno dei seguenti nomi stringa per endpoint come nome della stringa:  
  
    -   MOSRASTDBUY  
  
    -   MOSRASTDTRY  
  
    -   MOSRALITEBUY  
  
    -   MOSRALITETRY  
  
5.  Fare clic con il pulsante destro del mouse sulla nuova stringa nel riquadro a destra, quindi fare clic su **Modifica**.  
  
6.  Digitare il nuovo URL dell’endpoint nella casella di testo **Dati valore**, quindi fare clic su **OK**.  
  
7.  Ripetere i passaggi 4-6 per ogni nome di stringa elencato nel passaggio 4.  
  
## <a name="see-also"></a>Vedere anche  

 [Creazione e personalizzazione dell'immagine](Creating-and-Customizing-the-Image.md)   
 [Personalizzazioni aggiuntive](Additional-Customizations.md)   
 [Preparazione dell'immagine per la distribuzione](Preparing-the-Image-for-Deployment.md)   
 [Testare l'esperienza dei clienti](Testing-the-Customer-Experience.md) [creazione e personalizzazione dell'immagine](../install/Creating-and-Customizing-the-Image.md)   
 [Personalizzazioni aggiuntive](../install/Additional-Customizations.md)   
 [Preparazione dell'immagine per la distribuzione](../install/Preparing-the-Image-for-Deployment.md)   
 [Testare l'esperienza dei clienti](../install/Testing-the-Customer-Experience.md)

