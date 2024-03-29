---
title: Ripristinare un intero sistema dal backup di un computer client esistente
description: Viene descritto come utilizzare Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47e498a6-1b71-47de-88f6-8c13c221d108
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c78a2a2d950c8542bcf56005eb340ec78619acdb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433096"
---
# <a name="restore-a-full-system-from-an-existing-client-computer-backup"></a>Ripristinare un intero sistema dal backup di un computer client esistente

>Si applica a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials 
  
 I guasti hardware e gli errori del sistema operativo sono rari, ma possono verificarsi. Il malfunzionamento di una ventola potrebbe surriscaldare la scheda madre del computer e renderlo inutilizzabile. Il sistema operativo potrebbe venire danneggiato e non riavviarsi. Incendi e allagamenti possono causare danni permanenti all'hardware. Potrebbero verificarsi errori su un'unità disco rigido o si potrebbe decidere di sostituirla con un disco rigido più capiente.  
  
 Questo documento contiene informazioni sugli argomenti seguenti:  
  
-   [Che cos'è il ripristino completo del sistema del computer?](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_WhatIs)  
  
-   [Come funziona l'ambiente di ripristino?](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_HowDoes)  
  
-   [Creare un'unità flash USB avviabile per ripristinare un computer client](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_CreateBootable)  
  
-   [Utilizzo della procedura guidata Ripristino configurazione di sistema completo](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_Using)  
  
-   [Dove trovare i driver per l'hardware in uso?](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_FindDrivers)  
  
##  <a name="BKMK_WhatIs"></a> Che cos'è il ripristino completo del sistema del computer?  
 Se si decide di sostituire un'unità disco rigido o se il computer risulta danneggiato fino al punto cui non sia possibile usato o avviarlo, è possibile ripristinare il sistema da un backup precedente del computer. Il ripristino della configurazione di sistema completo ripristina lo stato del sistema al momento del backup.  
  
> [!IMPORTANT]
>  Non è possibile eseguire un ripristino della configurazione di sistema completo sull'hardware del computer, quale una scheda di sistema, diverso da quello che viene sostituito. Il sistema operativo installato dipende in grande misura dall'hardware sottostante del computer. Tuttavia, è possibile eseguire il ripristino della configurazione di sistema completo su un disco rigido di dimensioni pari o superiori al disco che viene sostituito.  
  
 Quando si esegue un ripristino della configurazione di sistema completo, è possibile scegliere un backup del computer specifico per ripristinare il sistema con tutte le applicazioni, configurazioni e impostazioni personalizzate prima dell'errore, della situazione di emergenza o del furto. È inoltre possibile scegliere i volumi da ripristinare.  
  
 Durante la pianificazione o la preparazione del ripristino del sistema completo in un computer di rete, considerare quanto segue:  
  
### <a name="windows-preinstallation-environment"></a>Ambiente preinstallazione di Windows  
 Ambiente preinstallazione di Windows (Windows PE) è un sistema operativo minimo messo a punto per preparare un computer per l'installazione di Windows. Per i server che esegue Windows Server Essentials, Windows PE viene installato automaticamente quando si inserisce il supporto di ripristino in un computer da ripristinare. Per i server che esegue Windows Server Essentials, Windows PE viene installato automaticamente quando si avvia il computer con il servizio Ripristino client o con l'unità flash USB.  
  
 Windows PE non supporta le connessioni wireless. Per questo motivo, il computer da ripristinare deve essere fisicamente connesso alla rete Small Business.  
  
### <a name="bitlocker"></a>BitLocker  
 Crittografia unità BitLocker (BitLocker) è una funzionalità di protezione dei dati che è disponibile in alcune versioni di Windows Vista, Windows 7 e Windows 8. BitLocker protegge da furti o esposizione dei dati in caso di smarrimento o furto del computer e offre un'eliminazione più sicura dei dati quando i computer vengono privati delle autorizzazioni.  
  
 **Per Windows Server Essentials:** Se il computer da ripristinare era stato crittografato con BitLocker (sia nel caso della sola unità del sistema operativo che dell'unità del sistema operativo e di altre unità fisse singole o multiple), è ancora possibile usare il supporto del ripristino completo del sistema presente sul CD fornito con il server e la procedura guidata Ripristino configurazione di sistema completo per reinstallare l'immagine dell'unità disco rigido, compreso il sistema operativo, da un backup e ripristinare i dati nel computer nuovo o riparato.  
  
 **Per Windows Server Essentials:** Se il computer da ripristinare era stato crittografato con BitLocker (sia nel caso della sola unità del sistema operativo che dell'unità del sistema operativo e di altre unità fisse singole o multiple), è ancora possibile usare la procedura guidata Ripristino configurazione di sistema completo per reinstallare l'immagine dell'unità disco rigido, compreso il sistema operativo, da un backup e ripristinare i dati nel computer nuovo o riparato.  
  
 Quando il server esegue il backup di unità, cartelle e file, sul server viene salvata una versione non crittografata di questi elementi. Durante il ripristino completo del sistema, questa versione non crittografata viene copiata nel computer.  
  
> [!NOTE]
>  Dopo il completamento del ripristino completo, è necessario riattivare BitLocker sul computer.  
>   
>  Per istruzioni su come abilitare BitLocker sui computer che eseguono Windows 8, vedere [BitLocker: Come abilitare BitLocker](https://go.microsoft.com/fwlink/p/?LinkID=254918).  
>   
>  Per istruzioni su come abilitare BitLocker sui computer che eseguono Windows 7, vedere [BitLocker Drive Encryption Step Guide for Windows 7](https://go.microsoft.com/fwlink/p/?LinkId=140225).  
  
 Per altre informazioni sulle nozioni di base relative a Crittografia unità BitLocker, vedere [Domande frequenti su BitLocker](https://go.microsoft.com/fwlink/p/?LinkID=254917).  
  
### <a name="encrypting-file-system-encrypted-files"></a>File crittografati con la tecnologia EFS (Encrypting File System)  
 La funzione EFS (Encrypting File System) in Windows offre un livello aggiuntivo di crittografia dei file basato sull'utente per diversi livelli di sicurezza tra più utenti dello stesso computer. È importante notare che, diversamente dalle unità crittografate con BitLocker, le cartelle e i file basati sulla tecnologia EFS continuano ad essere crittografati in ogni backup del computer. EFS non è disponibile in Windows XP Home Edition, Windows Vista Starter, Windows Vista Home Basic, Windows Vista Home Premium, Windows 7 Starter, Windows 7 Home Basic, Windows 7 Home Premium o Windows 8. È disponibile solo in Windows 8 Pro.  
  
> [!WARNING]
>  Diversamente da BitLocker, è possibile accedere ai file protetti tramite EFS unicamente dal sistema operativo che li ha crittografati.  
  
### <a name="disk-partitions"></a>Partizioni del disco  
 Se le dimensioni del disco rigido sul nuovo computer sono pari o superiori a quelle dell'originale, il disco rigido viene automaticamente riformattato e ripartizionato. Fare riferimento al grafico sotto per le specifiche:  
  
|Computer originale|Computer nuovo o ripristinato|  
|-----------------------|------------------------------|  
|Singolo disco con più partizioni|Singolo disco con più partizioni e l'eventuale spazio aggiuntivo viene allocato all'ultima partizione|  
|Singolo disco con una singola partizione|Singolo disco con una singola partizione e tutto lo spazio disponibile viene usato per la singola partizione|  
  
> [!NOTE]
>  Se vi sono differenze di dimensioni del disco e del layout di partizione tra il computer originale e quello nuovo o ripristinato, è necessario utilizzare Gestione disco per creare le partizioni appropriate sul computer nuovo o ripristinato. A tal fine è possibile usare la procedura guidata Ripristino configurazione di sistema completo.  
  
### <a name="raid-and-dynamic-disks"></a>RAID e dischi dinamici  
 Il backup degli array di dischi indipendenti (RAID) e dei dischi dinamici non è supportato.  
  
##  <a name="BKMK_HowDoes"></a> Come funziona l'ambiente di ripristino?  
 Il supporto di ripristino di sistema fornito con Windows ServerÂ® 2012 Essentials consente di installare Windows Preinstallation Environment (Windows PE) sul computer. Windows PE sostituisce l'ambiente MS-DOS e contiene i principali file di programma per Windows. In Windows Server Essentials, esistono due modi per ripristinare un sistema: utilizza il servizio Ripristino client, che usa una rete e non si basa su supporti, o tramite USB, unità memoria flash.  
  
> [!NOTE]
>  Windows PE non supporta le connessioni wireless. Per questo motivo, il computer da ripristinare deve essere fisicamente connesso alla rete Small Business.  
  
 L'ambiente di ripristino del sistema è fornito con i file di programma per i sistemi a 32 bit (x86) e a 64 bit (x64). Dopo aver inserito il supporto di ripristino del sistema, scegliere la versione dei file appropriata. 32 bit (x86) è la versione predefinita e viene selezionata automaticamente se l'utente non fa una scelta entro 30 secondi. Se sul server sono presenti aggiornamenti ai file di programma del ripristino configurazione di sistema completo, i file aggiornati vengono scaricati sul computer automaticamente.  
  
 Una volta configurato l'ambiente di preinstallazione, viene avviata la procedura guidata Ripristino configurazione di sistema completo. Questa procedura consente di ripristinare il contenuto del computer da un backup precedente. È anche possibile usare l'ambiente di ripristino del sistema per ripristinare un backup su un altro computer con hardware simile.  
  
 Nella maggior parte dei casi, i driver e i file di programma contenuti nell'ambiente di ripristino sono sufficienti per riavviare il computer nuovo o ripristinato. A seconda dell'hardware del computer nuovo o ripristinato, è possibile che l'ambiente di ripristino non includa tutti i driver della scheda di rete e del dispositivo di archiviazione che sono necessari quando si riavvia il computer ripristinato. La procedura guidata Ripristino configurazione di sistema completo consente di installare i driver, se necessario. Per informazioni su come individuare i driver hardware, vedere [Dove trovare i driver per l'hardware in uso](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_FindDrivers). Per informazioni su come usare il supporto di ripristino del sistema, vedere [Utilizzo della procedura guidata Ripristino configurazione di sistema completo](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_Using).  
  
##  <a name="BKMK_CreateBootable"></a> Creare un'unità flash USB avviabile per ripristinare un computer client  
 Se è necessario ripristinare un computer client da un oggetto esistente, eseguire il backup ma non riesce a individuare il CD di ripristino fornito con il server (in Windows Server Essentials) o non desiderate configurare il servizio Ripristino client sul server (in Windows Server Essentials) , è possibile creare un'unità flash USB avviabile. Usando poi l'unità flash USB è possibile avviare il computer client e ripristinare il sistema. L'unità flash USB deve avere una dimensione di almeno 1 GB.  
  
#### <a name="to-create-a-bootable-usb-flash-drive"></a>Per creare un'unità flash USB di avvio  
  
1.  Aprire il **Dashboard**.  
  
2.  Fare clic sulla scheda **Dispositivi**.  
  
3.  Nel riquadro **Attività** , fare clic su **Personalizza impostazioni di backup del computer e cronologia file**.  
  
    > [!NOTE]
    >  In Windows Server Essentials, fare clic su **attività di backup computer Client**.  
  
4.  Fare clic sulla scheda **Strumenti** e quindi selezionare **Crea chiave** nella sezione **Ripristino del computer**. Viene visualizzata la procedura guidata Creazione chiave di ripristino per il computer.  
  
5.  Inserire nel server un'unità flash USB da almeno 1 GB e seguire le istruzioni della procedura guidata.  
  
    > [!CAUTION]
    >  Tutti i dati presenti sull'unità flash USB verranno eliminati.  
  
##  <a name="BKMK_Using"></a> Utilizzo della procedura guidata Ripristino configurazione di sistema completo  
 Dopo aver usato il supporto di ripristino, il servizio Ripristino client o l'unità flash USB per avviare il computer e verificare che tutti i driver dell'hardware siano caricati sul computer client nuovo o ripristinato, verrà visualizzata la procedura guidata Ripristino configurazione di sistema completo. Questa procedura guidata consente di accedere al server, al backup del computer e ai volumi di origine da ripristinare sul computer ed esegue l'effettivo processo di ripristino.  
  
> [!NOTE]
>   Windows Server Essentials non supporta i seguenti scenari di ripristino:  
> 
> - Il ripristino di un disco di Strumentazione gestione Windows (MBR, Master Boot Record) in un computer basato su UEFI Unified Extensible Firmware Interface.  
>   -   Ripristino di un backup UEFI/GPT su un sistema BIOS.  
> 
>   Se si ripristinano i dati in uno di questi scenari, non sarà possibile avviare il sistema. Inoltre, potrebbe non essere possibile utilizzare i dischi rigidi la cui dimensione supera i 2 TB.  
  
 **Prerequisiti:**  
  
-   Prima di avviare il ripristino della configurazione di sistema completo, usare un cavo di rete (connessione cablata) per connettere il computer alla stessa rete usata dal server. Verificare di poter accedere a tutti i dischi rigidi sul computer client.  
  
    > [!WARNING]
    >  Non tentare di eseguire un ripristino del sistema completo su un computer che utilizza una connessione wireless alla rete.  
  
-   Se si è certi che nel computer mancano driver critici di rete o dei dispositivi di archiviazione, è necessario individuarli e copiarli su un'unità flash prima di avviare il processo di ripristino del sistema completo. Per Windows Server Essentials: Se si usa il supporto per il ripristino completo fornito su CD, il CD deve restare nell'unità durante la prima fase del processo di ripristino. Di conseguenza, non copiare i driver mancanti su un CD o un DVD, a meno che non si disponga di una seconda unità CD/DVD. Copiare invece i driver mancanti su un'unità flash USB.  
  
     Per informazioni su come individuare i driver per il computer in uso, vedere [Dove trovare i driver per l'hardware in uso](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_FindDrivers).  
  
-   Per Windows Server Essentials: Se non è possibile individuare il CD di ripristino configurazione di Windows Server Essentials, è possibile creare un'unità flash USB avviabile. Per altre informazioni, vedere [Create a bootable USB flash drive to restore a client computer](Restore-a-full-system-from-an-existing-client-computer-backup.md#BKMK_CreateBootable).  
  
#### <a name="to-use-the-full-system-restore-wizard"></a>Per usare la procedura guidata Ripristino configurazione di sistema completo  
  
1. Effettua una delle seguenti operazioni:  
  
   -   Windows Server Essentials: Accendere il computer da ripristinare, inserire il supporto di ripristino e spegnere il computer.  
  
        Riaccendere il computer e durante il POST (Power On Self Test), premere il tasto funzione (tasto-F) appropriato per accedere al menu Dispositivo di avvio e selezionare l'unità CD/DVD. Si avvierà Windows Boot Manager.  
  
   -   Windows Server Essentials: Se usa il servizio Ripristino client, riavviare il computer con l'opzione **Bootstrap da rete**. Altrimenti avviare il computer con la chiave USB.  
  
        Riaccendere il computer e durante il POST (Power On Self Test), premere il tasto funzione (tasto-F) appropriato per accedere al menu Dispositivo di avvio e selezionare **Bootstrap da rete** . È anche possibile scegliere di avviare dalla chiave USB. Si avvierà Windows Boot Manager.  
  
   > [!NOTE]
   >  Consultare la documentazione fornita dal produttore del computer per individuare il tasto funzione che consente di accedere al menu Dispositivo di avvio.  
  
2. Il supporto di ripristino del computer contiene le opzioni di avvio per i sistemi a 32 bit (x86) e a 64 bit (x64). In Windows Boot Manager, scegliere **Ripristino configurazione di sistema completo (x86)** o **Ripristino configurazione di sistema completo (x64)** . Se i driver dell'hardware del computer sono a 32 bit, scegliere x86, mentre se sono a 64 bit, scegliere x64. Verranno caricati i file di Windows e la procedura guidata Ripristino configurazione di sistema completo eseguirà una verifica per accertarsi che siano disponibili tutti i driver dell'hardware.  
  
3. Nella finestra **Procedura guidata Ripristino configurazione di sistema completo**, scegliere la lingua desiderata e fare clic sulla freccia.  
  
4. Scegliere il **Formato ora e valuta** appropriato e il **Layout di tastiera o metodo di input** per il computer. Scegliere **Continua**.  
  
5. Se mancano i driver, viene visualizzato il messaggio che il processo di ripristino non è possibile verificare i driver. Fare clic su **Chiudi**, quindi nella finestra di dialogo iniziale scegliere **Carica driver**.  
  
   1.  Nella finestra di dialogo **Rileva componenti hardware** , fare clic su **Installa driver**.  
  
   2.  Inserire l'unità flash USB che contiene i driver dell'hardware e scegliere **Analizza** nella finestra di dialogo **Installa driver**.  
  
   3.  Nella finestra di dialogo **Installa driver** , fare clic su **OK** quando vengono trovati i driver.  
  
   4.  Nella finestra di dialogo di **rilevamento dell'hardware** scegliere **Continua**.  
  
6. Se tutti i driver sono stati trovati durante il controllo iniziale o al momento dell'installazione di tutti i driver critici, scegliere **Continua** nella finestra di dialogo **Ripristino configurazione di sistema completo**.  
  
7. Nella pagina **Procedura guidata Ripristino configurazione di sistema completo** fare clic su **Avanti**.  
  
8. La procedura guidata esegue la ricerca del server.  
  
   1.  Se non è possibile individuare il server, sarà possibile rieseguire la ricerca o immettere l'indirizzo IP del server.  
  
   2.  Sono vengono rilevati più server, verrà chiesto di selezionarne uno.  
  
   3.  Se il server è disponibile, il **accedere a < nomeserver\>**  viene visualizzata la pagina.  
  
9. Nel **accedere al < nomeserver\>**  , digitare *< NomeAccountAmministratore\>*  nel **nome utente** casella di testo e il password dell'account amministratore nella **Password** casella di testo e quindi fare clic su **successivo**.  
  
    > [!IMPORTANT]
    >  È necessario usare un account amministratore creato in inglese. Se non è disponibile, è necessario creare un nuovo account amministratore. A questo scopo, aprire prima la scheda **Utenti** nel dashboard del server, poi impostare il formato della lingua della tastiera su Inglese e quindi eseguire l'attività **Aggiunti account utente** per creare l'account amministratore. Usare quindi il nuovo account amministratore per continuare a ripristinare il computer client.  
  
10. Nella pagina **Selezionare un computer da ripristinare**, scegliere il computer da ripristinare e quindi **Avanti**. È possibile scegliere **< ComputerName\>: (Questo computer)**  o scegliere un altro computer in rete dai **un altro computer** nell'elenco a discesa.  
  
    > [!NOTE]
    >  Se il computer non è noto al server (ad esempio, nel caso di un computer nuovo o riassegnato), l'opzione **Questo computer** non verrà visualizzata.  
  
11. Nella pagina **Selezionare il backup da ripristinare**, esaminare l'elenco di backup disponibili e selezionare quello da ripristinare sul computer.  
  
    > [!NOTE]
    >  Si consiglia di selezionare un backup completato correttamente (segno di spunta verde). Ciò garantisce che tutti i file di dati e di sistema vengano ripristinati correttamente.  
  
12. (*Facoltativo*) Selezionare un backup e fare clic su **Dettagli** per aprire la pagina **Dettagli backup** e visualizzare ulteriori informazioni sul backup. Usare le informazioni riportate nella pagina **Dettagli backup** per confrontare più backup e decidere quale sia il backup migliore. Scegliere **Chiudi** nella pagina **Dettagli backup** per tornare alla pagina **Selezionare il backup da ripristinare**.  
  
13. Nella pagina **Selezionare il backup da ripristinare**, scegliere un backup e quindi il pulsante **Avanti**.  
  
14. Nella pagina **Selezionare opzione di ripristino** scegliere una delle operazioni seguenti e quindi fare clic su **Avanti**.  
  
    > [!NOTE]
    >  Se il partizionamento automatico non è supportato, questa pagina non viene visualizzata.  
  
    1.  **Ripristino automatico completo del computer (scelta consigliata)** . Questa opzione consente di garantire che il computer sarà ripristinato allo stato in cui si trovava prima dell'ora e della data del backup scelto. Se si sceglie questa opzione, andare al passaggio 15.  
  
    2.  **Consenti la selezione dei volumi da ripristinare (avanzata)** . Questa opzione consente di scegliere i volumi da ripristinare e il relativo punto di ripristino. È inoltre possibile creare partizioni sul disco rigido.  
  
15. Nella pagina **Selezionare i volumi da ripristinare** è possibile scegliere i volumi da ripristinare.  
  
    > [!NOTE]
    >  Questa pagina viene visualizzata se sul computer di origine del backup ci sono più dischi rigidi o se sull'unità di destinazione del ripristino lo spazio di archiviazione è inferiore a quello dell'unità di origine del backup.  
  
    1. La procedura guidata tenterà di abbinare i volumi di origine a quelli di destinazione. È consigliabile verificare che il mapping predefinito sia corretto.  
  
       1.  Per deselezionare un volume, fare clic sulla freccia del menu elenco per il volume e quindi su **Nessuno**.  
  
       2.  Dopo aver selezionato i volumi, fare clic su **Avanti**.  
  
    2. Se la dimensione del volume di origine e di quello di destinazione è la stessa, o se la dimensione di quello originale è inferiore rispetto alla destinazione, tra i due verrà visualizzata una freccia verde. Se le dimensioni dei volumi non corrispondono (volume originale di dimensioni superiori a quello di destinazione), tra l'origine e la destinazione verrà visualizzata una X rossa.  
  
       > [!NOTE]
       >  La X rossa viene visualizzata anche quando:  
       > 
       > - La dimensione del settore del disco sul volume origine non corrisponde a quella del volume dei destinazione. Questo può accadere se si sostituisce il disco fisico con un disco che ha una diversa dimensione dei settori oppure se si configurano gli spazi di archiviazione (che potrebbero avere una dimensione dei settori diversa da quella del disco fisico).  
       >   -   Viene raggiunto il limite del numero di cluster. Per ripristinare il volume di origine sul volume di destinazione, è necessario formattare il volume di destinazione con lo stesso numero di cluster del volume origine. Se il volume di destinazione è troppo grande e la dimensione dei settori troppo piccola, è possibile che si raggiunga il limite del numero di cluster.  
  
       1. Scegliere **Esegui Gestione disco (avanzata)** e creare un nuovo volume delle stesse dimensioni del volume riservato per il sistema.  
  
          > [!NOTE]
          >  Se un computer client è basato su Unified Extensible Firmware Interface UEFI, è necessario usare il **diskpart** dello strumento per inizializzare il disco del sistema. Per fare ciò, aprire una finestra di comando (tenere premuto Ctrl+Alt+Maiusc per 5 secondi nell'ambiente WinPE), eseguire **diskpart.exe** e quindi i seguenti comandi:  
          > 
          > 1. **DISKPART > disco elenco**  
          >    2. **DISKPART > select disk #** *< disco\>*  
          >    3. **DISKPART > Pulisci**  
          >    4. **DISKPART > convertire gpt**  
          >    5. **DISKPART > creare partizione efi dimensioni =** *100* (dove *100* è un esempio di dimensione di partizione in MB, deve essere uguale a quella della partizione originale)  
          >    6. **DISKPART > creare partizione msr dimensioni =** *128* (dove *128* è un esempio di dimensione di partizione in MB, deve essere uguale a quella della partizione originale)  
          >    7. **DISKPART > uscire**  
  
       2. *(Facoltativo)* Selezionare l'opzione **Non assegnare lettera o percorso unità**.  
  
       3. Formattare il volume come **NTFS**.  
  
       4. Al termine della formattazione, fare clic con il pulsante destro del mouse sul nuovo volume di sistema e quindi selezionare **Contrassegna partizione come attiva**.  
  
       5. Se sono presenti altri volumi che devono corrispondere ad altri volumi nel backup, ripetere i passaggi da *ii* a *iv* per creare e attivare i volume e chiudere **Gestione disco**.  
  
       6. Nella pagina **Seleziona volumi da ripristinare** , associare il volume riservato per il sistema al volume della stessa dimensione creato nel passo *v*.  
  
       7. Associare tutti gli altri volumi di origine ai volumi di destinazione corrispondenti.  
  
       8. Fare clic su **Avanti** per continuare con il ripristino.  
  
16. Nella pagina **Confermare i volumi da ripristinare** esaminare le associazioni e fare clic su **Avanti**. Se è necessario apportare delle modifiche, fare clic su **Indietro** e ripetere il passaggio 14.  
  
17. Il **Restoring < ComputerName\> da < data e ora del backup\>**  pagina viene riportato lo stato di avanzamento del processo di ripristino.  
  
18. Nella pagina **Ripristino terminato correttamente**, rimuovere il supporto di ripristino e fare clic su **Fine**. Il computer verrà riavviato.  
  
    > [!IMPORTANT]
    >  Se prima del ripristino era stata attivata l'opzione Crittografia unità BitLocker, dopo il riavvio del computer è necessario attivare BitLocker manualmente.  
  
##  <a name="BKMK_FindDrivers"></a> Dove trovare i driver per l'hardware in uso?  
 A seconda dell'hardware del computer nuovo o ripristinato, è possibile che il supporto di ripristino non includa tutti i driver della scheda di rete e del dispositivo di archiviazione che sono necessari quando si riavvia il computer ripristinato. È necessario determinare quali driver mancano, individuarli nei supporti esistenti o sul sito Web del produttore, copiarli su un'unità flash, quindi copiarli dall'unità flash al nuovo o ripristino computer quando si esegue la procedura guidata Ripristino configurazione di sistema completo.  
  
 Quando viene eseguito il backup di un computer, i relativi driver vengono salvati in tale backup. Se il supporto di ripristino non include tutti i driver necessari, è possibile aprire un backup del computer e copiare quindi i driver su un'unità flash USB.  
  
#### <a name="to-copy-drivers-from-a-backup-to-a-usb-flash-drive"></a>Per copiare i driver da un backup su un'unità flash USB  
  
1. In un altro computer aprire il dashboard.  
  
2. Fare clic su **Dispositivi** e quindi sul computer per cui sono necessari i driver.  
  
3. Fare clic su **Ripristina file o cartelle per il computer**. Verrà visualizzata la procedura guidata Ripristino file o cartelle.  
  
4. Scegliere il backup completato correttamente più recente e successivamente fare clic su **Avanti**.  
  
5. Scegliere un volume da aprire e quindi fare clic su **Avanti**. Verrà visualizzata una finestra in cui sono elencati i file e le cartelle compresi nel backup.  
  
6. Inserire l'unità flash USB in un connettore USB sul computer e copiare i driver della cartella di ripristino della configurazione di sistema completo nell'unità flash USB.  
  
   > [!NOTE]
   >  Potrebbe essere necessario selezionare **Livello superiore** fino a quando si raggiunge la radice del volume di sistema.  
  
7. Rimuovere l'unità flash e quindi inserirla nel computer che viene ripristinato.  
  
   È possibile usare l'unità flash USB per installare i driver del computer da ripristinare. La procedura guidata di ripristino di file o cartelle cerca altri driver su questa unità flash USB mentre è in corso la procedura guidata Ripristino configurazione di sistema completo. I driver che con maggiore probabilità saranno necessari includono quello della scheda di rete e i driver del dispositivo di archiviazione.  
  
## <a name="see-also"></a>Vedere anche  
  
-   [Gestire il Backup e ripristino](Manage-Backup-and-Restore-in-Windows-Server-Essentials.md)  
  
-   [Gestire Windows Server Essentials](Manage-Windows-Server-Essentials.md)
