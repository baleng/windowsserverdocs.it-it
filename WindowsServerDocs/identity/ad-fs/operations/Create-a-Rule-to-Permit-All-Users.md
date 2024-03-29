---
ms.assetid: 8c179884-f0d9-4c7a-973d-820119cf3c38
title: Creare una regola per consentire tutti gli utenti
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 1356218c5f9f47073f007286e8acfdf4c3608b73
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407624"
---
# <a name="create-a-rule-to-permit-all-users"></a>Creare una regola per consentire tutti gli utenti

In Windows Server 2016, è possibile utilizzare un **criteri di controllo di accesso** per creare una regola che consentirà tutti gli utenti di accedere a una relying party.  In Windows Server 2012 R2, usando il modello di regola **Consenti tutti gli utenti** in Active Directory Federation Services \(AD FS @ no__t-2, è possibile creare una regola di autorizzazione che consentirà a tutti gli utenti di accedere al relying party. 

È possibile utilizzare regole di autorizzazione aggiuntive per limitare ulteriormente l'accesso. Agli utenti che hanno ricevuto l'autorizzazione di accesso alla relying parti da parte del Servizio federativo potrebbe comunque essere negato l'accesso dalla stessa relying party.  
  
È possibile utilizzare le procedure seguenti per creare una regola attestazione con lo snap di gestione di ADFS\-in.  
  
Per completare questa procedura, è necessaria almeno l'appartenenza al gruppo **Administrators** oppure a un gruppo equivalente nel computer locale.  Informazioni dettagliate sull'utilizzo degli account appropriati e appartenenze [dominio gruppi predefiniti locali e](https://go.microsoft.com/fwlink/?LinkId=83477). 

## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2016"></a>Per creare una regola per consentire tutti gli utenti in Windows Server 2016

1.  In Server Manager, fare clic su **strumenti**, quindi selezionare **Gestione ADFS**.  
  
2.  Nell'albero della console, in **ADFS**, fare clic su **attendibilità**. 
![Crea regola](media/Create-a-Rule-to-Permit-All-Users/permitall1.PNG)

3.  Pulsante destro del mouse il **Trust della Relying Party** che si desidera consentire l'accesso a e selezionare **Modifica criteri di controllo di accesso**.  
![Crea regola](media/Create-a-Rule-to-Permit-All-Users/permitall2.PNG)

4. Per l'accesso alla controllo criteri selezionare **consentire tutti gli utenti** e quindi fare clic su **Applica** e **Ok**.
![Crea regola](media/Create-a-Rule-to-Permit-All-Users/permitall3.PNG)
  
## <a name="to-create-a-rule-to-permit-all-users-in-windows-server-2012-r2"></a>Per creare una regola per consentire tutti gli utenti in Windows Server 2012 R2 
  
1.  In Server Manager, fare clic su **strumenti**, quindi selezionare **Gestione ADFS**.  
  
2.  Nell'albero della console, in **ADFS\\relazioni di Trust\\attendibilità**, fare clic su una relazione di trust specifico nell'elenco in cui si desidera creare la regola.  

3.  Destra\-fare clic sul trust selezionato e quindi fare clic su **Modifica regole attestazione**.  
![Crea regola](media/Create-a-Rule-to-Permit-All-Users/permitall4.PNG)  

4.  Nel **Modifica regole attestazione** nella finestra di dialogo fare clic sul **regole di autorizzazione rilascio** scheda o **le regole di autorizzazione di delega** scheda \(in base al tipo di regola di autorizzazione necessari\), e quindi fare clic su **Aggiungi regola** per avviare il **Aggiunta guidata regole attestazione di autorizzazione**.  
![Crea regola](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)  
5.  Nel **Seleziona modello di regola** nella pagina **il modello di regola attestazione**, selezionare **consentire tutti gli utenti** dall'elenco, quindi fare clic su **Avanti**.  
![Crea regola](media/Create-a-Rule-to-Permit-All-Users/permitall6.PNG)    
6.  Nel **configurare la regola** pagina, fare clic su **Fine**.  
  
7.  Nel **Modifica regole attestazione** la finestra di dialogo, fare clic su **OK** per salvare la regola.  

## <a name="additional-references"></a>Altri riferimenti 
[Configurare le regole delle attestazioni](Configure-Claim-Rules.md)  
 
[Elenco di controllo: Creazione di regole delle attestazioni per un'istanza di attendibilità del componente](https://technet.microsoft.com/library/ee913578.aspx)  
  
[Quando usare una regola attestazioni di autorizzazione](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Ruolo delle attestazioni](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Ruolo delle regole delle attestazioni](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
