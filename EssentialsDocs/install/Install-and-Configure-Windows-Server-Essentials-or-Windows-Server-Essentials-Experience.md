---
title: Installare e configurare Windows Server Essentials o Esperienza Windows Server Essentials
description: Viene descritto come utilizzare Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 48ea6cd4-3955-4aaf-9236-2515a6c3e730
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f5593c21b99f4f8cb22979d5dc201a38e54be84c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433484"
---
# <a name="install-and-configure-windows-server-essentials-or-windows-server-essentials-experience"></a>Installare e configurare Windows Server Essentials o Esperienza Windows Server Essentials

>Si applica a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server Essentials è ideale come primo server per piccole imprese con fino a 25 utenti e 50 dispositivi. Per le organizzazioni con un massimo di 100 utenti e 200 dispositivi, è ora possibile usare Windows Server 2012 R2 con il ruolo esperienza Windows Server Essentials installato. In questo argomento sono illustrati entrambi gli scenari.  
  
Esperienza Windows Server Essentials è un ruolo in Windows Server 2016 che consente di sfruttare i vantaggi di tutte le funzionalità (ad esempio accesso Web remoto e PC backup) che sono disponibili in Windows Server Essentials senza i relativi blocchi e limiti in  Windows Server Essentials. Questo ruolo del server è disponibile anche in Windows Server Essentials e viene abilitato per impostazione predefinita.
  
Prima di installare il ruolo esperienza Essentials o Windows Server Essentials, tenere presente le limitazioni seguenti.  
  
|Esperienza Windows Server Essentials in Windows Server Essentials|Esperienza Windows Server Essentials in Windows Server 2016
|----|----|
|-Deve essere il controller di dominio nella radice della foresta e del dominio e deve contenere tutti i ruoli FSMO.<br /><br /> -Non può essere installato in un ambiente con un dominio di Active Directory preesistente (tuttavia, vi è un periodo di tolleranza di 21 giorni per eseguire le migrazioni).|-Non è necessario essere un controller di dominio se è installato in un ambiente con un dominio di Active Directory preesistente.<br /><br /> -Se un dominio Active Directory non esiste, l'installazione del ruolo creerà un dominio Active Directory e il server diventerà il controller di dominio nella radice della foresta e del dominio, che contiene tutti i ruoli FSMO.  
|Può essere distribuito solo in un singolo dominio.|Può essere distribuito solo in un singolo dominio.  
|Nel dominio non può esistere un controller di dominio di sola lettura.|Nel dominio non può esistere un controller di dominio di sola lettura.

> [!NOTE]
>  Per scaricare versioni di valutazione dei sistemi operativi, visitare il sito TechNet Evaluation Center:  
>   
>  [Download di Windows Server 2016](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016)  
>   
>  [Download di Windows Server Essentials](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016-essentials)
  
## <a name="installation-options"></a>Opzioni di installazione  
 Questo documento fornisce istruzioni dettagliate per l'installazione e la configurazione di Windows Server Essentials. A seconda dell'ambiente di rete, sono disponibili le opzioni di installazione seguenti:  
  
-    Windows Server Essentials (con il ruolo esperienza Windows Server Essentials abilitato per impostazione predefinita)  
  
-    Windows Server 2016 con il ruolo esperienza Windows Server Essentials installato  
 
|Ambiente di distribuzione|Descrizione|Sezioni correlate|  
|----------------------------|-----------------|---------------------|  
|Nuovo ambiente Active Directory|È possibile installare Windows Server Essentials per creare un nuovo ambiente Active Directory.|[Distribuire Windows Server Essentials per configurare un nuovo ambiente Active Directory](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_NewAD)|  
|Ambiente Active Directory esistente|È possibile installare Windows Server Essentials in un ambiente Active Directory esistente.|[Distribuire Windows Server Essentials in un ambiente Active Directory esistente](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_ExistingAD)|  
|Ambiente virtuale|È possibile distribuire Windows Server Essentials come macchina virtuale.|[Virtualizzare l'ambiente](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_VirtualWSE)|  
|Distribuzione automatica|È possibile automatizzare la distribuzione di Windows Server Essentials tramite Windows PowerShell.|[Installare e configurare Windows Server Essentials tramite Windows PowerShell](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_PowerShell)|  
  
## <a name="before-you-begin"></a>Prima di iniziare  
 Prima di iniziare l'installazione, consultare la documentazione seguente:  
  
-   [Panoramica sul prodotto di Windows Server Essentials](https://www.microsoft.com/server-cloud/windows-server-essentials/windows-server-2012-r2-essentials.aspx)  
  

-   [Requisiti di sistema per Windows Server Essentials](../get-started/system-requirements.md)   

  
##  <a name="BKMK_NewAD"></a> Distribuire Windows Server Essentials per configurare un nuovo ambiente Active Directory  
 Windows Server Essentials consente di configurare rapidamente un ambiente Active Directory e le funzionalità server correlate.  
  
###  <a name="BKMK_WSEDeploy"></a> Distribuzione di Windows Server Essentials  
 Se si usa Windows Server Essentials, Windows Server Essentials Experience è già abilitato. È comunque necessario eseguire alcuni passaggi per configurare il server.  
  
##### <a name="to-configure-windows-server-essentials-on-a-physical-server"></a>Per configurare Windows Server Essentials in un server fisico  
  
1. Dopo la pagina **iniziale** di Windows, sul desktop viene visualizzata la procedura guidata **Configurazione di Windows Server Essentials**.  
  
2. Seguire le istruzioni per completare la procedura guidata:  
  
   1.  Nella pagina **Configurazione di Windows Server Essentials** fare clic su **Avanti**.  
  
   2.  In **Impostazioni data/ora**verificare la correttezza di data, ora e fuso orario, quindi fare clic su **Avanti**.  
  
   3.  In **Informazioni società**digitare il nome della società, ad esempio **Contoso,Ltd.** , quindi fare clic su **Avanti**. Facoltativamente, è possibile modificare il nome di dominio interno e il nome del server.  
  
   4.  In **Crea account amministratore di rete**digitare un nome e una password per il nuovo account amministratore.  
  
       > [!NOTE]
       >  Non usare il nome account e la password **Administrator** predefiniti.  
  
   5.  Fare clic su **configurare**.  
  
3. Il server verrà riavviato più volte durante il processo di configurazione e l'accesso verrà eseguito automaticamente fino al termine della configurazione. Il processo richiede circa 20 minuti.  
  
4. Sul desktop fare clic sull'icona del dashboard per avviare il dashboard del server. In **Home** completare le **Attività iniziali** elencate nella scheda **Configura**.  
  
   Al termine della configurazione, il server che esegue Windows Server Essentials sarà configurato come controller di dominio.  
  
###  <a name="BKMK_DeployWSERole"></a> Distribuzione del ruolo esperienza Windows Server Essentials in Windows Server 2012 R2 Standard e Datacenter  
 È possibile utilizzare Server Manager per abilitare e configurare il ruolo esperienza Windows Server Essentials in Windows Server 2012 R2 Standard o Windows Server 2012 R2 Datacenter utilizzando la procedura seguente.  
  
##### <a name="to-deploy-the-windows-server-essentials-experience-role-in-windows-server-2012-r2"></a>Per distribuire il ruolo Esperienza Windows Server Essentials in Windows Server 2012 R2  
  
1.  Accedere al server come amministratore locale.  
  
2.  Aprire **Server Manager**e fare clic su **Aggiungi ruoli e funzionalità**.  
  
3.  In **Selezione ruoli server**selezionare il ruolo **Esperienza Windows Server Essentials** . Nella finestra di dialogo fare clic su **Aggiungi funzionalità**e quindi su **Avanti**.  
  
4.  In **Funzionalità**fare clic su **Avanti**.  
  
5.  Esaminare la descrizione del ruolo **Esperienza Windows Server Essentials** , quindi fare clic su **Avanti**.  
  
6.  Nelle pagine successive fare clic su **Avanti**, quindi nella pagina di conferma fare clic su **Installa**.  
  
7.  Al termine dell'installazione, Windows Server Essentials Experience dovrebbe essere elencato come ruolo server in Server Manager.  
  
8.  Nell'area di notifica flag in Server Manager fare clic sul flag e quindi su **Configura Windows Server Essentials**.  
  
9. (Facoltativo) Se necessario, modificare il nome del server.  
  
    > [!IMPORTANT]
    >  Non è possibile modificare il nome del server dopo aver configurato Windows Server Essentials.  
  

10. Seguire la procedura guidata per configurare Windows Server Essentials come descritto nella sezione precedente di [Deploying Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) sezione.  

10. Seguire la procedura guidata per configurare Windows Server Essentials come descritto nella sezione precedente di [Deploying Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) sezione.  

  
##  <a name="BKMK_ExistingAD"></a> Distribuire Windows Server Essentials in un ambiente Active Directory esistente  
 È possibile distribuire Windows Server Essentials anche se nell'organizzazione è già presente un ambiente Active Directory. Inoltre, è possibile scegliere se distribuire Windows Server Essentials come controller di dominio.  
  
> [!IMPORTANT]
>  Questa opzione è disponibile solo se si distribuisce il ruolo esperienza Windows Server Essentials in Windows Server 2012 R2 Standard o Windows Server 2012 R2 Datacenter.  
  
#### <a name="to-deploy-windows-server-essentials-in-an-existing-active-directory-environment"></a>Per distribuire Windows Server Essentials in un ambiente Active Directory esistente  
  
1.  (Facoltativo) Se necessario, modificare il nome del server.  
  
    > [!IMPORTANT]
    >  Non è possibile modificare il nome del server dopo aver configurato Windows Server Essentials.  
  
2.  Aggiungere il server che esegue Windows Server Essentials a un dominio esistente nel modo seguente:  
  
    1.  Se si vuole che il server sia un controller di dominio, configurarlo come controller di dominio di replica.  
  
    2.  In caso contrario, aggiungere il server al dominio tramite gli strumenti nativi di Windows.  
  
3.  Riavviare il server e accedere al server come amministratore di dominio.  
  
4.  Aprire Server Manager e fare clic su **Aggiungi ruoli e funzionalità**.  
  
5.  Nelle pagine successive fare clic su **Avanti**.  
  
6.  In **Selezione ruoli server**selezionare **Esperienza Windows Server Essentials**. Nella finestra di dialogo fare clic su **Aggiungi funzionalità**e quindi su **Avanti**.  
  
7.  In **Funzionalità**fare clic su **Avanti**.  
  
8.  Esaminare la descrizione di **Esperienza Windows Server Essentials**, quindi fare clic su **Avanti**.  
  
9. Nelle pagine successive fare clic su **Avanti**, quindi nella pagina di conferma fare clic su **Installa**.  
  
10. Al termine dell'installazione, Windows Server Essentials Experience verrà elencato come un ruolo del server in Server Manager.  
  
11. Nell'area di notifica flag in **Server Manager** fare clic sul flag e quindi su **Configura Windows Server Essentials**.  
  
12. Eseguire la procedura guidata per configurare Windows Server Essentials. A seconda della configurazione di Active Directory, verrà indicato se Windows Server Essentials viene configurato come controller di dominio o come membro del dominio. Fare clic su **Configura** per avviare la configurazione. Il processo di configurazione richiede circa 10 minuti.  
  
##  <a name="BKMK_VirtualWSE"></a> Virtualizzare l'ambiente  
  Windows Server Essentials, Windows Server 2012 R2 Standard e Windows Server 2012 R2 Datacenter possono essere eseguiti come macchine virtuali. Per eseguire le macchine virtuali, usare gli strumenti di gestione di Hyper-V in un server che esegue Hyper-V. Da una prospettiva di gestione delle licenze, Windows Server Essentials consente di configurare il ruolo Hyper-V e virtualizzare l'ambiente. La licenza consente di configurare un altro sistema operativo guest che esegue Windows Server Essentials. A seconda del provider di sistema "e configurazione, Windows Server Essentials consente di configurare facilmente un ambiente virtualizzato.  
  
#### <a name="to-deploy-windows-server-essentials-as-a-virtual-machine"></a>Per distribuire Windows Server Essentials come macchina virtuale  
  
1.  Dopo la pagina iniziale di Windows (a seconda della "configurazione del sistema del provider e s), il **prima di iniziare** pagina offre un'opzione per configurare Windows Server Essentials come istanza virtuale o hardware fisico. La disponibilità di queste opzioni è predefinita dal provider di sistema e non sempre sono presenti entrambe le opzioni. Per installare Windows Server Essentials come macchina virtuale, in **installa Windows Server Essentials**, selezionare **installa come un'istanza virtuale**, quindi fare clic su **configura**.  
  
2.  Verrà eseguito il provisioning di una macchina virtuale. L'operazione richiede circa cinque minuti.  
  

3.  Configurare quindi Windows Server Essentials come descritto nella sezione precedente di [Deploying Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) sezione.  

3.  Configurare quindi Windows Server Essentials come descritto nella sezione precedente di [Deploying Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy) sezione.  

  
##  <a name="BKMK_PowerShell"></a> Installare e configurare Windows Server Essentials tramite Windows PowerShell  
 È possibile automatizzare l'installazione di Windows Server Essentials tramite i cmdlet di Windows PowerShell.  
  
#### <a name="to-install-windows-server-essentials-by-using-windows-powershell"></a>Per installare Windows Server Essentials tramite Windows PowerShell  
  
1.  Aprire la console di Windows PowerShell da un prompt dei comandi con privilegi elevati.  
  
2.  Installare il ruolo esperienza Windows Server Essentials tramite il comando seguente:  
  
    ```  
    Add-WindowsFeature ServerEssentialsRole  
    ```  
  
3.  Eseguire `Get-Help Start-WssConfigurationService`.  
  
    1.  Eseguire il comando seguente per avviare la configurazione di Windows Server Essentials come controller di dominio:  
  
        ```  
        Start-WssConfigurationService -CompanyName "ContosoTest" -DNSName "ContosoTest.com" -NetBiosName "ContosoTest" -ComputerName "YourServerName  œNewAdminCredential $cred  
        ```  
  
    2.  Eseguire il comando seguente per avviare la configurazione di Windows Server Essentials come membro di un dominio esistente: È necessario essere membro del gruppo Enterprise Admins e del gruppo Domain Admins in Active Directory per eseguire questa attività:  
  
        ```  
        Start-WssConfigurationService  œCredential <Your Credential>  
  
        ```  
  
4.  Monitorare lo stato dell'installazione tramite i comandi seguenti:  
  
    -   Per fare in modo che lo stato dell'installazione venga visualizzato sull'indicatore di stato, eseguire `Get-WssConfigurationStatus  œShowProgress`.  
  
    -   Per ottenere lo stato di avanzamento immediato senza l'indicatore di stato, eseguire `Get-WssConfigurationStatus`.  
  
## <a name="see-also"></a>Vedere anche  
  
-   [Quali sono le novità in Windows Server Essentials](../get-started/what-s-new.md)  
  
-   [Installare Windows Server Essentials](Install-Windows-Server-Essentials.md)  
  
-   [Introduzione a Windows Server Essentials](../get-started/get-started.md)
