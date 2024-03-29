---
title: Use local resources on Hyper-V virtual machine with VMConnect
description: Descrive i requisiti per l'uso delle risorse locali con VMConnect
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18eface5-7518-4c6b-9282-93e2e3e87492
author: KBDAzure
ms.author: kathyDav
ms.date: 12/06/2016
ms.openlocfilehash: 70bf72ec2277679820d985c9f78f10a4ea6e04df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392891"
---
# <a name="use-local-resources-on-hyper-v-virtual-machine-with-vmconnect"></a>Use local resources on Hyper-V virtual machine with VMConnect

>Si applica a: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2

Virtual Machine Connection (VMConnect) consente di usare le risorse locali di un computer in una macchina virtuale, ad esempio un'unità flash USB rimovibile o una stampante. La modalità sessione avanzata consente anche di ridimensionare la finestra VMConnect. Questo articolo illustra come configurare l'host e quindi concedere alla macchina virtuale l'accesso a una risorsa locale.

La modalità sessione avanzata e il testo degli Appunti di tipo sono disponibili solo per le macchine virtuali che eseguono sistemi operativi Windows recenti. Requisiti \(See [per l'uso delle risorse locali](#requirements-for-using-local-resources), sotto. \) 

Per le macchine virtuali che eseguono Ubuntu, vedere [Modifica risoluzione dello schermo di Ubuntu in una macchina Virtuale Hyper-V](https://blogs.msdn.microsoft.com/virtual_pc_guy/2014/09/19/changing-ubuntu-screen-resolution-in-a-hyper-v-vm/). 
  
## <a name="turn-on-enhanced-session-mode-on-a-hyper-v-host"></a>Attivare la modalità sessione avanzata in un host Hyper-V  
Se l'host Hyper-V esegue Windows 10 o Windows 8.1, la modalità sessione avanzata è abilitata per impostazione predefinita, pertanto è possibile ignorare questo passaggio e passare alla sezione successiva. Tuttavia, se l'host esegue Windows Server 2016 o Windows Server 2012 R2, eseguire prima questa operazione. 
  
Attivare la modalità sessione avanzata:

1.  Connettersi al computer che ospita la macchina virtuale.  
  
2.  In Hyper-V Manager, selezionare nome del computer dell'host.  
  
    ![Schermata che mostra un host come nome del computer elencato in Gestione Hyper-V nel riquadro a sinistra.](media/Hyper-V-HyperVManager-HostNameSelected.png)  
  
3.  Selezionare **Impostazioni Hyper-V**.  
  
    ![Schermata che mostra l'opzione Impostazioni Hyper-V in azioni nel riquadro di destra.](media/HyperV-ActionsHyperVSettings.png)  
  
4.  Nella sezione **Server**, selezionare **Criteri modalità sessione avanzata**.  
  
    ![Schermata che mostra l'opzione di criteri modalità sessione avanzata nella sezione sicurezza.](media/Hyper-V-Settings-ServerEnhancedSessionModePolicy.png)  
  
5.  Selezionare la casella di controllo **Consenti modalità sessione avanzata** .  
  
    ![Schermata che mostra la Consenti migliorato sessione modalità casella di controllo criteri modalità sessione avanzata.](media/Hyper-V-Settings-EnhancedSessionModePolicyCheckBox.png)  
  
6.  Nella sezione **Utente**, selezionare **Modalità sessione avanzata**.  
  
    ![Schermata che mostra l'opzione della modalità sessione avanzata nella sezione utente. ](media/Hyper-V-Settings-UserEnhancedSessionMode.png)  
  
7.  Selezionare la casella di controllo **Consenti modalità sessione avanzata** .  
  
8.  Fare clic su **OK**.  
  
## <a name="choose-a-local-resource"></a>Scegliere una risorsa locale

Le risorse locali includono stampanti, appunti e un'unità locale nel computer in cui si esegue VMConnect. Per ulteriori informazioni, vedere i [requisiti per l'utilizzo delle risorse locali](#requirements-for-using-local-resources)di seguito.  
  
Per scegliere una risorsa locale:
  
1.  Aprire VMConnect.  
  
2.  Spegnere la macchina virtuale a cui ci si vuole connettere.  
  
3.  Fare clic su **Mostra opzioni**.  
  
    ![Schermata che mostra le opzioni nella parte inferiore sinistra della finestra di dialogo chiama.](media/HyperV-VMConnect-DisplayConfig.png)  
  
4.  Selezionare **Risorse locali**.  
  
    ![Schermata in cui viene visualizzato nella scheda risorse locali.](media/HyperV-VMConnect-DisplayConfig-LocalResources.png)  
  
5.  Fare clic su **Altro**.  
  
    ![Schermata in cui viene visualizzato il pulsante altro.](media/HyperV-VMConnect-DisplayConfig-LocalResourcesMore.png)  
  
6.  Selezionare l'unità che si vuole usare nella macchina virtuale e fare clic su **Ok**.  
  
    ![Schermata che mostra le risorse locali e le unità che è possibile selezionare.](media/HyperV-VMConnect-Settings-LocalResourcesDrives.png)  
  
7.  Selezionare **Salva impostazioni per connessioni future alla macchina virtuale**.  
  
    ![Schermata che chiama la casella di controllo per selezionare questa opzione.](media/HyperV-VMConnect-SaveSettings.png)  
  
8.  Fare clic su **Connetti**.  
  
## <a name="edit-vmconnect-settings"></a>Modificare le impostazioni di VMConnect

È possibile modificare facilmente le impostazioni di connessione per VMConnect eseguendo il comando seguente in Windows PowerShell o nel prompt dei comandi:  
  
`VMConnect.exe <ServerName> <VMName> /edit`  
  
## <a name="requirements-for-using-local-resources"></a>Requisiti per l'utilizzo delle risorse locali

Per poter usare le risorse locali del computer in una macchina virtuale:  
  
-   Per l'host Hyper-V devono essere attivate le impostazioni **criteri modalità sessione avanzata** e **modalità sessione avanzata** .  
  
-   Il computer in cui si usa VMConnect deve eseguire Windows 10, Windows 8.1, Windows Server 2016 o Windows Server 2012 R2.  
  
-   Per la macchina virtuale deve essere abilitato Servizi Desktop remoto ed eseguire Windows 10, Windows 8.1, Windows Server 2016 o Windows Server 2012 R2 come sistema operativo guest.  
  
Se il computer che esegue VMConnect e la macchina virtuale soddisfano entrambi i requisiti, è possibile usare una delle risorse locali seguenti, se disponibili:  
  
-   Configurazione dello schermo  
  
-   Audio
  
-   Stampanti  
  
-   Appunti per copiare e incollare  
  
-   Smart card  
  
-   Dispositivi USB  
  
-   Unità  
  
-   Dispositivi Plug and Play supportati  
  
## <a name="why-use-a-computers-local-resources"></a>Perché utilizzare le risorse locali del computer?
È possibile utilizzare le risorse locali del computer per:  
  
-   Risolvere i problemi di una macchina virtuale senza una connessione di rete alla macchina virtuale.  
  
-   Copiare e incollare i file da e verso la macchina virtuale con la stessa procedura usata con una Connessione Desktop remoto.  
  
-   Accedere alla macchina virtuale usando una smart card.  
  
-   Eseguire la stampa da una macchina virtuale su una stampante locale.  
  
-   Testare e risolvere i problemi delle applicazioni dello sviluppatore che richiedono il reindirizzamento dell'audio e dei dispositivi USB senza usare RDP.  
  
## <a name="see-also"></a>Vedere anche  
[Connettersi a una macchina virtuale](https://technet.microsoft.com/library/cc742407.aspx)  
[È consigliabile creare una macchina virtuale di generazione 1 o 2 in Hyper-V?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)



