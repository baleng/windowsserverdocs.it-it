---
title: 'Passaggio 4: configurare le impostazioni di criteri di gruppo per gli aggiornamenti automatici'
description: 'Argomento Windows Server Update Service (WSUS): configurare le impostazioni di Criteri di gruppo per Aggiornamenti automatici è il passaggio quattro in un processo in quattro passaggi per la distribuzione di WSUS'
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 62177d05-d832-4ea8-bca4-47a8cd34a19c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a01d8881e8f0f7ca6feff691938f926a12460db0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361658"
---
# <a name="step-4-configure-group-policy-settings-for-automatic-updates"></a>Passaggio 4: Configurare le impostazioni di Criteri di gruppo per Aggiornamenti automatici

>Si applica a: Windows Server (canale semestrale), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In un ambiente Active Directory è possibile utilizzare Criteri di gruppo per definire il modo in cui i computer e gli utenti (indicati in questo documento come client WSUS) possono interagire con gli aggiornamenti di Windows per ottenere gli aggiornamenti automatici da Windows Server Update Services (WSUS).

In questo argomento contiene due sezioni principali:

[Gruppo di impostazioni dei criteri per gli aggiornamenti client WSUS](#group-policy-settings-for-wsus-client-updates), che fornisce indicazioni e comportamento i dettagli sulle impostazioni di Windows Update e dell'utilità di pianificazione di manutenzione dei criteri di gruppo che controllano come i client WSUS possono interagire con Windows Update per ottenere gli aggiornamenti automatici.

[Informazioni supplementari](#supplemental-information) include le sezioni seguenti:

-   [Accesso alle impostazioni Windows Update in criteri di gruppo](#accessing-the-windows-update-settings-in-group-policy), che fornisce indicazioni generali sull'utilizzo di criteri di gruppo editor di gestione e informazioni sull'accesso alle estensioni dei criteri di Update Services e alle impostazioni dell'utilità di pianificazione di manutenzione nel gruppo Politica.

-   [Modifiche a WSUS pertinente per questa Guida](#changes-to-wsus-relevant-to-this-guide): per gli amministratori conoscono WSUS 3.2 e versioni precedenti, questa sezione viene fornita un breve riepilogo delle differenze principali tra la versione corrente e precedente di WSUS pertinente per questa Guida.

-   [Termini e definizioni](#terms-and-definitions): le definizioni per vari termini relativi ai servizi WSUS e aggiornamenti che vengono utilizzati in questa Guida.

## <a name="group-policy-settings-for-wsus-client-updates"></a>Impostazioni di criteri di gruppo per gli aggiornamenti client WSUS
Questa sezione vengono fornite informazioni su tre estensioni di criteri di gruppo. In queste estensioni sono disponibili le impostazioni che è possibile utilizzare per configurare come client WSUS possono interagire con Windows Update per ricevere gli aggiornamenti automatici.

-   [Configurazione computer &gt; Windows Update impostazioni dei criteri](#computer-configuration--windows-update-policy-settings)

-   [Configurazione computer &gt; impostazioni dei criteri dell'utilità di pianificazione di manutenzione](#computer-configuration--maintenance-scheduler-policy-settings)

-   [Configurazione utente &gt; Windows Update impostazioni dei criteri](#user-configuration--windows-update-policy-settings)

> [!NOTE]
> In questo argomento si presuppone che già utilizza e si ha familiarità con criteri di gruppo. Se non ha familiarità con criteri di gruppo, si consiglia di rivedere le informazioni di [informazioni supplementari](#supplemental-information) sezione di questo documento prima di tentare di configurare le impostazioni di criteri per Windows Server Update SERVICES.

### <a name="computer-configuration--windows-update-policy-settings"></a>Configurazione computer > Impostazioni di criteri di Windows Update
In questa sezione vengono forniti dettagli sulle impostazioni dei criteri basate sul computer seguenti:

-   [Consenti Aggiornamenti automatici installazione immediata](#allow-automatic-updates-immediate-installation)

-   [Consenti a non amministratori di ricevere notifiche di aggiornamento](#allow-non-administrators-to-receive-update-notifications)

-   [Consenti aggiornamenti firmati da un percorso del servizio di aggiornamento Microsoft nella rete Intranet](#allow-signed-updates-from-an-intranet-microsoft-update-service-location)

-   [Frequenza di rilevamento Aggiornamenti automatici](#automatic-updates-detection-frequency)

-   [Configurare Aggiornamenti automatici](#configure-automatic-updates)

-   [Ritarda riavvio per installazioni pianificate](#delay-restart-for-scheduled-installations)

-   [Non modificare l'opzione predefinita per "installa gli aggiornamenti e spegni" nella finestra di dialogo arresta Windows](#do-not-adjust-default-option-to-install-updates-and-shut-down-in-shut-down-windows-dialog)

-   [Non visualizzare l'opzione "installa gli aggiornamenti e spegni" nella finestra di dialogo arresta Windows](#do-not-display-install-updates-and-shut-down-option-in-shut-down-windows-dialog)

-   [Abilita destinazione lato client](#enable-client-side-targeting)

-   [Abilitazione di Windows Update risparmio energia per riattivare automaticamente il computer per installare gli aggiornamenti pianificati](#enabling-windows-update-power-management-to-automatically-wake-up-the-computer-to-install-scheduled-updates)

-   [Nessun riavvio automatico con utenti connessi per le installazioni pianificate degli aggiornamenti automatici](#no-auto-restart-with-logged-on-users-for-scheduled-automatic-updates-installations)

-   [Richiedi nuovamente il riavvio con installazioni pianificate](#re-prompt-for-restart-with-scheduled-installations)

-   [Ripianificazione Aggiornamenti automatici installazioni pianificate](#reschedule-automatic-updates-scheduled-installations)

-   [Specificare il percorso del servizio di aggiornamento Microsoft nella rete Intranet](#specify-intranet-microsoft-update-service-location)

-   [Attivare gli aggiornamenti consigliati tramite Aggiornamenti automatici](#turn-on-recommended-updates-via-automatic-updates)

-   [Attivare le notifiche software](#turn-on-software-notifications)

In Editor gestione criteri i criteri di Windows Update per la configurazione basata su computer si trovano nel percorso: *Policyname* > **Configurazione computer** > **criteri** > **modelli amministrativi** > **componenti Windows** > **Windows Update**.

> [!NOTE]
> Per impostazione predefinita, queste impostazioni non sono configurate.

#### <a name="allow-automatic-updates-immediate-installation"></a>Consenti installazione immediata aggiornamenti automatici
Specifica se aggiornamenti automatici installerà automaticamente gli aggiornamenti che non interrompere i servizi di Windows o il riavvio di Windows.

|Supportato in:|Esclusione:|
|---------|-------|
|Sistemi operativi Windows che si trovano all'interno vengono loro [prodotti di Microsoft Support Lifecycle](https://support.microsoft.com/gp/lifeselect).|null|

> [!NOTE]
> Se l'impostazione dei criteri "Configura Aggiornamenti automatici" è impostata su **disabilitato**, questo criterio non ha alcun effetto.

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Specifica che gli aggiornamenti non vengono installati immediatamente. Gli amministratori locali possono modificare questa impostazione utilizzando l'Editor Criteri di gruppo locale.|
|**Attivata**|Specifica che gli aggiornamenti automatici installa immediatamente gli aggiornamenti vengono scaricati e sono pronti per l'installazione.|
|**Disattivata**|Specifica che gli aggiornamenti non vengono installati immediatamente.|

**Opzioni:** Non sono disponibili opzioni per questa impostazione.

#### <a name="allow-non-administrators-to-receive-update-notifications"></a>Consentire a utenti non amministratori di ricevere le notifiche di aggiornamento
Specifica se gli utenti non amministratori riceveranno le notifiche di aggiornamento in base all'impostazione di criteri Configura Aggiornamenti automatici.

|Supportato in:|Esclusione:|
|---------|-------|
|Sistemi operativi Windows che si trovano all'interno vengono loro [prodotti di Microsoft Support Lifecycle](https://support.microsoft.com/gp/lifeselect).|Visualizzare i dettagli nella tabella seguente.|

> [!NOTE]
> Se l'impostazione dei criteri "Configura Aggiornamenti automatici" è disabilitata o non è configurata, questa impostazione dei criteri non ha alcun effetto.

> [!IMPORTANT]
> a partire da Windows 8 e Windows RT, questa impostazione dei criteri è abilitata per impostazione predefinita. In tutte le versioni precedenti di Windows, è disabilitato per impostazione predefinita.

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Specifica che gli utenti verranno sempre visualizzata una finestra di controllo dell'Account e richiedono autorizzazioni elevate per eseguire queste attività. Un amministratore locale può modificare questa impostazione utilizzando l'editor di Criteri di gruppo locale.|
|**Attivata**|Specifica che aggiornamenti automatici Windows e Microsoft Update includerà utenti non amministratori per determinare quale utente connesso riceverà le notifiche di aggiornamento. Gli utenti non amministratori saranno in grado di installare tutti i contenuti facoltativi, consigliati e importanti di aggiornamento per i quali ricevono una notifica. Non sarà possibile visualizzare una finestra di controllo dell'Account utente e non necessitano di autorizzazioni con privilegi elevate per installare questi aggiornamenti, tranne nel caso di aggiornamenti che contengono modifiche alle impostazioni dell'interfaccia utente, contratto di licenza o Windows Update.<br /><br />Esistono due casi in cui l'effetto di questa impostazione dipende dal computer operativo:<br /><br />1.  **Nascondere** o **ripristinare** aggiornamenti<br />2.  **Annulla** installazione di un aggiornamento<br /><br />In Windows Vista o Windows XP, se questa impostazione è abilitata, non sarà possibile visualizzare una finestra di controllo dell'Account utente e non necessitano di autorizzazioni con privilegi elevate per nascondere, ripristinare o annullare gli aggiornamenti.<br /><br />In Windows Vista, se questa impostazione è abilitata, non sarà possibile visualizzare una finestra di controllo dell'Account utente e non necessitano di autorizzazioni con privilegi elevate per nascondere, ripristinare o annullare gli aggiornamenti. Se questa impostazione non è abilitata, agli utenti verranno sempre visualizzato una finestra del controllo dell'Account e richiedono autorizzazioni elevate per nascondere, ripristinare o annullare gli aggiornamenti.<br /><br />In Windows 7, questa impostazione ha effetto. Gli utenti verranno sempre visualizzate una finestra del controllo dell'Account e richiedono autorizzazioni elevate per eseguire queste attività.<br /><br />In Windows 8 e Windows RT, questa impostazione ha effetto.|
|**Disattivata**|Specifica che ha effettuato l'accesso solo gli amministratori ricevono le notifiche di aggiornamento. **Nota:** In Windows 8 e Windows RT questa impostazione dei criteri è abilitata per impostazione predefinita. In tutte le versioni precedenti di Windows, è disabilitato per impostazione predefinita.|

**Opzioni:** Non sono disponibili opzioni per questa impostazione.

#### <a name="allow-signed-updates-from-an-intranet-microsoft-update-service-location"></a>Consenti aggiornamenti firmati da un percorso del servizio Microsoft update intranet
Specifica se aggiornamenti automatici accetta gli aggiornamenti che sono firmati da entità diverse da Microsoft durante l'aggiornamento è disponibile in un percorso del servizio intranet Microsoft update.

|Supportato in:|Esclusione:|
|---------|-------|
|Sistemi operativi Windows che si trovano all'interno vengono loro [prodotti di Microsoft Support Lifecycle](https://support.microsoft.com/gp/lifeselect).|Windows RT|

> [!NOTE]
> Gli aggiornamenti da un servizio diverso da un servizio di aggiornamento Microsoft intranet devono sempre essere firmati da Microsoft e non vengono influenzati da questa impostazione di criteri.

> [!NOTE]
> Questo criterio non è supportato in Windows RT. Abilita questo criterio non avrà alcun effetto nei computer che eseguono Windows RT.

**Opzioni:** Non sono disponibili opzioni per questa impostazione.

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Specifica che gli aggiornamenti da un percorso del servizio Microsoft update intranet devono essere firmati da Microsoft.|
|**Attivata**|Specifica che gli aggiornamenti automatici accetta aggiornamenti ricevuti tramite una rete intranet percorso del servizio Microsoft update se sono firmati da un certificato nell'archivio certificati "Autori attendibili" del computer locale.|
|**Disattivata**|Specifica che gli aggiornamenti da un percorso del servizio Microsoft update intranet devono essere firmati da Microsoft.|

**Opzioni:** Non sono disponibili opzioni per questa impostazione.

#### <a name="always-automatically-restart-at-the-scheduled-time"></a>Esegui sempre riavvio automatico nel momento pianificato
Specifica se un timer di riavvio inizia sempre immediatamente dopo che Windows Update installa gli aggiornamenti importanti, anziché prima inviare una notifica agli utenti nella schermata di accesso per almeno due giorni.

|Supportato in:|Esclusione:|
|---------|-------|
|Sistemi operativi Windows che si trovano all'interno vengono loro [prodotti di Microsoft Support Lifecycle](https://support.microsoft.com/gp/lifeselect).|null|

> [!NOTE]
> Se è abilitata l'impostazione dei criteri "nessun riavvio automatico con utenti connessi per le installazioni pianificate di aggiornamenti automatici", questo criterio non ha alcun effetto.

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Specifica che Windows Update non modificherà il comportamento di riavvio del computer.|
|**Attivata**|Specifica che un timer di riavvio verrà sempre avviato immediatamente dopo che Windows Update installa gli aggiornamenti importanti, anziché prima notificare gli utenti nella schermata di accesso per almeno due giorni.<br /><br />Il timer di riavvio può essere configurato per avviarsi con qualsiasi valore da 15 a 180 minuti. Quando il timer scade, il riavvio viene continuato anche se il computer disponga di accesso di utenti.|
|**Disattivata**|Specifica che Windows Update non modificherà il comportamento di riavvio del computer.|

**Opzioni:** se questa impostazione è abilitata, è possibile specificare la quantità di tempo che deve trascorrere dopo l'installazione degli aggiornamenti prima che si verifichi un riavvio forzato del computer.

#### <a name="automatic-updates-detection-frequency"></a>Frequenza rilevamento aggiornamenti automatici
Specifica le ore di Windows viene utilizzato per determinare il tempo di attesa prima di verificare la disponibilità di aggiornamenti. Il tempo di attesa esatto è determinato dall'utilizzo di ore specificato qui meno zero e il 20% delle ore specificato. Ad esempio, se questo criterio viene utilizzato per specificare una frequenza di rilevamento di 20 ore, tutti i client a cui viene applicato il criterio verranno controllati gli aggiornamenti in un punto qualsiasi tra 16 e 20 ore.

|Supportato in:|Esclusione:|
|---------|-------|
|Sistemi operativi Windows che si trovano all'interno vengono loro [prodotti di Microsoft Support Lifecycle](https://support.microsoft.com/gp/lifeselect).|Windows RT|

> [!NOTE]
> L'impostazione "Specificare percorso servizio di aggiornamento Microsoft nella rete intranet" deve essere abilitata per questo criterio abbia effetto.
>
> Se l'impostazione dei criteri "Configura Aggiornamenti automatici" è disabilitata, questo criterio non ha alcun effetto.

> [!NOTE]
> Questo criterio non è supportato in Windows RT. Abilita questo criterio non avrà alcun effetto nei computer che eseguono Windows RT.

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Specifica che Windows verrà verificata la disponibilità di aggiornamenti all'intervallo predefinito di 22 ore.|
|**Attivata**|Specifica che Windows verrà verificata la disponibilità di aggiornamenti all'intervallo specificato.|
|**Disattivata**|Specifica che Windows verrà verificata la disponibilità di aggiornamenti all'intervallo predefinito di 22 ore.|

**Opzioni:** se questa impostazione è abilitata, è possibile specificare l'intervallo di tempo (in ore) che Windows Update attende prima di verificare la disponibilità di aggiornamenti.

#### <a name="configure-automatic-updates"></a>Configurare gli aggiornamenti automatici
Specifica specificare se gli aggiornamenti automatici sono abilitati nel computer.

|Supportato in:|Esclusione:|
|---------|-------|
|Sistemi operativi Windows che si trovano all'interno vengono loro [prodotti di Microsoft Support Lifecycle](https://support.microsoft.com/gp/lifeselect).|Windows RT|

Se abilitata, è necessario selezionare una delle quattro opzioni disponibili in questa impostazione Criteri di gruppo.

Per utilizzare questa impostazione, selezionare **Enabled**, quindi nella **Opzioni** in **configurare l'aggiornamento automatico**, selezionare una delle opzioni (2, 3, 4 o 5).

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Specifica che l'utilizzo di aggiornamenti automatici non è specificata a livello di criteri di gruppo. Tuttavia, un amministratore del computer può comunque configurare Aggiornamenti automatici nel Pannello di controllo.|
|**Attivata**|Specifica che Windows riconosce quando il computer è online e utilizza la connessione Internet per cercare eventuali aggiornamenti di Windows Update.<br /><br />Quando abilitata, gli amministratori locali saranno possibile utilizzare il pannello di controllo di Windows Update per selezionare un'opzione di configurazione di propria scelta. Tuttavia, gli amministratori locali non potrà essere per disabilitare la configurazione per gli aggiornamenti automatici.<br /><br />-   **2-Invia una notifica per il download e invia una notifica per l'installazione**<br />    Quando Windows Update rileva gli aggiornamenti applicabili al computer, gli utenti verranno informati che gli aggiornamenti sono pronti per il download. Gli utenti possono quindi eseguire Windows Update per scaricare e installare eventuali aggiornamenti disponibili.<br />-   **3-download automatico e notifica per l'installazione** (impostazione predefinita)<br />    Windows Update rileva che gli aggiornamenti e li scarica in background. l'utente non è una notifica o interrotta durante il processo. Dopo aver completato il download, gli utenti vengono informati pronto per l'installazione di aggiornamenti. Gli utenti possono quindi eseguire Windows Update per installare gli aggiornamenti scaricati.<br />-   **4-download automatico e pianificazione dell'installazione**<br />    È possibile specificare la pianificazione utilizzando le opzioni in questa impostazione di criteri di gruppo. Se viene specificata alcuna pianificazione, la pianificazione predefinita per tutte le installazioni sarà ogni giorno alle 3:00. Se tutti gli aggiornamenti richiedono il riavvio per completare l'installazione, Windows verrà riavviato automaticamente il computer. Se un utente ha eseguito l'accesso al computer quando Windows è pronto per il riavvio, l'utente riceve una notifica e viene fornita la possibilità di ritardare il riavvio. **Nota:** a partire da Windows 8, è possibile impostare gli aggiornamenti da installare durante la manutenzione automatica anziché usare una pianificazione specifica associata a Windows Update. Manutenzione automatica verrà installare gli aggiornamenti quando il computer non è in uso ed evitare l'installazione degli aggiornamenti quando il computer è alimentato a batteria. Se non è in grado di installare gli aggiornamenti entro manutenzione automatica, Windows Update installerà gli aggiornamenti immediatamente. Gli utenti verranno quindi informati un riavvio in sospeso. Un riavvio in sospeso verrà eseguita solo se è presente alcun potenziale di perdita accidentale dei dati.    È possibile specificare le opzioni di pianificazione nelle impostazioni dell'utilità di pianificazione della manutenzione Editor gestione criteri, che si trovano nel percorso *policyname* > **computer Configuration** > **policies** > **modelli amministrativi** >  **Componenti di Windows** > **utilità di pianificazione della manutenzione**1 limite di attivazione della**manutenzione automatica**. Vedere la sezione di questo riferimento intitolata: [Impostazioni dell'utilità di pianificazione di manutenzione](#computer-configuration--maintenance-scheduler-policy-settings), per i dettagli dell'impostazione.    **5-Consenti all'amministratore locale di scegliere l'impostazione**<br />-Specifica se gli amministratori locali possono utilizzare il pannello di controllo degli aggiornamenti automatici per selezionare un'opzione di configurazione di propria scelta, ad esempio, se gli amministratori locali possono scegliere ora di installazione pianificata.<br />    Gli amministratori locali non saranno possibile disabilitare la configurazione per gli aggiornamenti automatici.|
|**Disattivata**|Specifica che gli aggiornamenti client che sono disponibili dal servizio Windows Update pubblico devono essere scaricati da Internet e installati manualmente.|

#### <a name="delay-restart-for-scheduled-installations"></a>Ritarda riavvio per installazioni pianificate
Specifica la quantità di tempo di che attesa prima di procedere con il riavvio pianificato aggiornamenti automatici.

|Supportato in:|Esclusione:|
|---------|-------|
|Sistemi operativi Windows che si trovano all'interno vengono loro [prodotti di Microsoft Support Lifecycle](https://support.microsoft.com/gp/lifeselect).|null|

> [!NOTE]
> Questo criterio si applica solo quando aggiornamenti automatici è configurato per eseguire installazioni pianificate degli aggiornamenti. Se l'impostazione dei criteri "Configura Aggiornamenti automatici" è disabilitato, questo criterio non ha alcun effetto.

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Specifica che una volta installati gli aggiornamenti, il tempo di attesa predefinito di 15 minuti devono trascorrere prima che si verifichi un riavvio pianificato.|
|**Attivata**|Specifica che, al termine dell'installazione, un riavvio pianificato verrà eseguito una volta scaduto il numero di minuti specificato.|
|**Disattivata**|Specifica che una volta installati gli aggiornamenti, il tempo di attesa predefinito di 15 minuti devono trascorrere prima che si verifichi un riavvio pianificato.|

**Opzioni:** se questa impostazione è abilitata, è possibile usare questa opzione per specificare la quantità di tempo (in minuti) di attesa aggiornamenti automatici prima di procedere con il riavvio pianificato.

#### <a name="do-not-adjust-default-option-to-install-updates-and-shut-down-in-shut-down-windows-dialog"></a>Non modificare l'opzione predefinita per installare gli aggiornamenti e arrestare la finestra di dialogo arresta Windows
Questa impostazione di criteri consente di specificare se il **Installa aggiornamenti e spegni** opzione è consentita come scelta predefinita nel **Spegni** la finestra di dialogo.

|Supportato in:|Esclusione:|
|---------|-------|
|Sistemi operativi Windows che si trovano all'interno vengono loro [prodotti di Microsoft Support Lifecycle](https://support.microsoft.com/gp/lifeselect).|null|

> [!NOTE]
> Questa impostazione dei criteri non ha alcun effetto se la**configurazione del computer** *PolicyName* >   > **criteri** > **modelli amministrativi** > **componenti Windows** > **Windows Update**@no_ _T-11**non visualizzare l'opzione "installa gli aggiornamenti e spegni" nella finestra di dialogo Arresta** l'impostazione dei criteri di Windows.

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Specifica che **Installa aggiornamenti e spegni** sarà l'opzione predefinita nel **Spegni** la finestra di dialogo se gli aggiornamenti disponibili per l'installazione al momento l'utente seleziona l'opzione Arresta per arrestare il computer.|
|**Attivata**|Se si abilita questa impostazione di criteri, l'ultima scelta dell'utente (ad esempio, ibernazione o riavvio) è l'opzione predefinita nella finestra di dialogo **arresta Windows** , indipendentemente dal fatto che l'opzione **Installa aggiornamenti e Spegni** sia disponibile nel **Cosa si vuole fare per il computer?** menu.|
|**Disattivata**|Specifica che **Installa aggiornamenti e spegni** sarà l'opzione predefinita nel **Spegni** la finestra di dialogo se gli aggiornamenti disponibili per l'installazione al momento l'utente seleziona l'opzione Arresta per arrestare il computer.|

**Opzioni:** Non sono disponibili opzioni per questa impostazione.

#### <a name="do-not-connect-to-any-windows-update-internet-locations"></a>Non si connettono a qualsiasi percorso Internet di Windows Update
Anche quando Windows Update è configurato per la ricezione di aggiornamenti da un servizio di aggiornamento Intranet, recupererà periodicamente le informazioni dal servizio public Windows Update per consentire connessioni future a Windows Update e ad altri servizi, ad esempio Microsoft Update o Microsoft Store.

L'abilitazione di questo criterio consente di disabilitare la funzionalità per recuperare periodicamente le informazioni dal servizio pubblico di Windows Server Update e potrebbe causare la connessione a servizi pubblici, ad esempio Microsoft Store per smettere di funzionare.

|Supportato in:|Esclusione:|
|---------|-------|
|a partire da Windows Server 2012 R2, Windows 8.1 o Windows RT 8,1, sistemi operativi Windows che si trovano ancora all'interno del ciclo di vita del [supporto dei prodotti Microsoft](https://support.microsoft.com/gp/lifeselect).|null|

> [!NOTE]
> Questo criterio si applica solo quando il computer è configurato per connettersi a un servizio di aggiornamento di intranet utilizzando l'impostazione dei criteri "Specificare intranet aggiornamento percorso del servizio Microsoft".

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Il comportamento predefinito per recuperare informazioni dal servizio pubblico di Windows Server Update persiste.|
|**Attivata**|Specifica che i computer non recupererà le informazioni dal servizio pubblico di Windows Server Update.|
|**Disattivata**|Il comportamento predefinito per recuperare informazioni dal servizio pubblico di Windows Server Update persiste.|

**Opzioni:** Non sono disponibili opzioni per questa impostazione.

#### <a name="do-not-display-install-updates-and-shut-down-option-in-shut-down-windows-dialog"></a>Non visualizzare l'opzione Installa aggiornamenti e Spegni nella finestra di dialogo arresta Windows
Specifica se il **Installa aggiornamenti e spegni** opzione viene visualizzata nel **Spegni** la finestra di dialogo.

|Supportato in:|Esclusione:|
|---------|-------|
|Sistemi operativi Windows che si trovano all'interno vengono loro [prodotti di Microsoft Support Lifecycle](https://support.microsoft.com/gp/lifeselect).|null|

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Specifica che il **Installa aggiornamenti e spegni** opzione è disponibile nel **Spegni** la finestra di dialogo se sono disponibili aggiornamenti quando l'utente seleziona l'opzione Arresta per arrestare il computer. Un amministratore locale è possibile modificare questa impostazione tramite criteri locali.|
|**Attivata**|Specifica che **Installa aggiornamenti e spegni** non verranno visualizzati come una scelta nel **Spegni** la finestra di dialogo, anche se gli aggiornamenti sono disponibili per l'installazione quando l'utente seleziona l'opzione Arresta per arrestare il computer.|
|**Disattivata**|Specifica che il **Installa aggiornamenti e spegni** opzione sarà l'opzione predefinita nel **Spegni** la finestra di dialogo se gli aggiornamenti disponibili per l'installazione al momento l'utente seleziona l'opzione Arresta per arrestare il computer.|

**Opzioni:** Non sono disponibili opzioni per questa impostazione.

#### <a name="enable-client-side-targeting"></a>Abilitare la destinazione lato client
Specifica il nome del gruppo di destinazione o i nomi configurati nella console di WSUS che devono ricevere gli aggiornamenti da WSUS.

|Supportato in:|Esclusione:|
|---------|-------|
|Sistemi operativi Windows che si trovano all'interno vengono loro [prodotti di Microsoft Support Lifecycle](https://support.microsoft.com/gp/lifeselect).|Windows RT|

> [!NOTE]
> Questo criterio si applica solo quando il computer è configurato per supportare i nomi dei gruppi di destinazione specificata in WSUS. Se il nome del gruppo di destinazione non esiste in WSUS, verrà ignorata fino a quando non viene creato. Se l'impostazione dei criteri "Specificare percorso servizio di aggiornamento Microsoft nella rete intranet" è disabilitato o non configurato, questo criterio non ha alcun effetto.

> [!NOTE]
> Questo criterio non è supportato in Windows RT. Abilita questo criterio non avrà alcun effetto nei computer che eseguono Windows RT.

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Specifica che viene inviata alcuna informazione di gruppo di destinazione a WSUS. Un amministratore locale è possibile modificare questa impostazione utilizzando un criterio locale.|
|**Attivata**|Specifica che le informazioni sul gruppo di destinazione specificato viene inviati a WSUS, che lo utilizza per determinare quali aggiornamenti devono essere distribuiti a questo computer. Se WSUS supporta più gruppi di destinazione, è possibile utilizzare questo criterio per specificare più nomi di gruppi, separati da punti e virgola, se i nomi dei gruppi di destinazione sono stati aggiunti nell'elenco gruppo di computer in WSUS. In caso contrario, è necessario specificare un singolo gruppo.|
|**Disattivata**|Specifica che viene inviata alcuna informazione di gruppo di destinazione a WSUS.|

**Opzioni:** Utilizzare questo spazio per specificare uno o più nomi di gruppi di destinazione.

#### <a name="enabling-windows-update-power-management-to-automatically-wake-up-the-computer-to-install-scheduled-updates"></a>Abilitazione di risparmio energia di Windows Update riattivare automaticamente il computer per installare aggiornamenti pianificati
Specifica se Windows Update verranno utilizzate le funzionalità di risparmio energia di Windows o opzioni risparmio energia per riattivare automaticamente il computer dalla modalità di sospensione, se sono presenti aggiornamenti pianificati per l'installazione.

Il computer verrà riattiva automaticamente solo se è configurato Windows Update per installare automaticamente gli aggiornamenti. Se il computer è in modalità sospensione quando si verifica il tempo di installazione pianificata e sono disponibili aggiornamenti da applicare, Windows Update utilizzerà le funzionalità di risparmio energia di Windows o opzioni risparmio energia per riattivare automaticamente il computer per installare gli aggiornamenti. Windows Update verrà inoltre riattivare il computer e installare un aggiornamento se si verifica una scadenza di installazione.

Il computer non attivano a meno che non sono disponibili aggiornamenti da installare. Se il computer è alimentato a batteria, una volta attivato, Windows Update, non è stato possibile installare aggiornamenti e il computer tornerà allo stato di sospensione entro due minuti.

|Supportato in:|Esclusione:|
|---------|-------|
|a partire da Windows Vista e Windows Server 2008 (Windows 7), i sistemi operativi Windows che rientrano nel ciclo di vita del [supporto dei prodotti Microsoft](https://support.microsoft.com/gp/lifeselect).|null|

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Windows Update non si riattiva il computer dalla modalità di sospensione per installare gli aggiornamenti. Un amministratore locale è possibile modificare questa impostazione utilizzando un criterio locale.|
|**Attivata**|Windows Update riattiva il computer dalla modalità di sospensione per installare gli aggiornamenti in presenza delle condizioni elencate in precedenza.|
|**Disattivata**|Windows Update non si riattiva il computer dalla modalità di sospensione per installare gli aggiornamenti.|

**Opzioni:** Non sono disponibili opzioni per questa impostazione.

#### <a name="no-auto-restart-with-logged-on-users-for-scheduled-automatic-updates-installations"></a>Escludi riavvio automatico per installazioni pianificate di Aggiornamenti automatici con gli utenti non connessi
Specifica che per completare un'installazione pianificata, aggiornamenti automatici attenderà che il computer venga riavviato da qualsiasi utente che ha effettuato l'accesso, anziché il computer venga riavviato automaticamente.

|Supportato in:|Esclusione:|
|---------|-------|
|Sistemi operativi Windows che si trovano all'interno vengono loro [prodotti di Microsoft Support Lifecycle](https://support.microsoft.com/gp/lifeselect).|null|

> [!NOTE]
> Questo criterio si applica solo quando aggiornamenti automatici è configurato per eseguire installazioni pianificate degli aggiornamenti. Se l'impostazione dei criteri "Configura Aggiornamenti automatici" è disabilitato, questo criterio non ha alcun effetto.

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Specifica che gli aggiornamenti automatici informerà l'utente che il computer verrà riavviato automaticamente tra cinque minuti per completare l'installazione.|
|**Attivata**|Alcuni aggiornamenti richiedono il riavvio rendere effettivi gli aggiornamenti del computer. Se lo stato è impostato su abilitato, gli aggiornamenti automatici non riavvia un computer automaticamente durante un'installazione pianificata se un utente ha effettuato l'accesso al computer. Al contrario, aggiornamenti automatici notifica all'utente di riavviare il computer.|
|**Disattivata**|Specifica che gli aggiornamenti automatici informerà l'utente che il computer verrà riavviato automaticamente tra cinque minuti per completare l'installazione.|

**Opzioni:** Non sono disponibili opzioni per questa impostazione.

#### <a name="re-prompt-for-restart-with-scheduled-installations"></a>Richiedi nuovamente riavvio per installazioni pianificate
Specifica la quantità di tempo per gli aggiornamenti automatici di attesa prima di richiedere nuovamente un riavvio pianificato.

|Supportato in:|Esclusione:|
|---------|-------|
|Sistemi operativi Windows che si trovano all'interno vengono loro [prodotti di Microsoft Support Lifecycle](https://support.microsoft.com/gp/lifeselect).|Windows RT|

> [!IMPORTANT]
> Questo criterio si applica solo quando aggiornamenti automatici è configurato per eseguire installazioni pianificate degli aggiornamenti. Se l'impostazione dei criteri "Configura Aggiornamenti automatici" è disabilitato, questo criterio non ha alcun effetto.

> [!NOTE]
> Questo criterio non ha alcun effetto nei computer che eseguono Windows RT.

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Un riavvio pianificato si verifica dieci minuti dopo il riavvio la richiesta di messaggio viene ignorato. Un amministratore locale è possibile modificare questa impostazione utilizzando un criterio locale.|
|**Attivata**|Specifica che dopo la precedente richiesta di riavvio posticipata, verrà eseguito un riavvio pianificato dopo il numero specificato di specificato di minuti.|
|**Disattivata**|Un riavvio pianificato si verifica dieci minuti dopo il riavvio la richiesta di messaggio viene ignorato.|

**Opzioni:** Se abilitata, è possibile usare questa opzione per specificare (in minuti) la durata del tempo che deve trascorrere prima che venga richiesto di nuovo agli utenti il riavvio pianificato.

#### <a name="reschedule-automatic-updates-scheduled-installations"></a>Nuova pianificazione installazioni pianificate Aggiornamenti automatici
Specifica la quantità di tempo di attesa dopo un avvio del computer, prima di procedere con l'installazione non è stato precedentemente eseguita tramite aggiornamenti automatici.

Se lo stato è impostato su **non configurato**, un'installazione pianificata non completata verrà eseguita un minuto dopo l'avvio successivo del computer.

|Supportato in:|Esclusione:|
|---------|-------|
|Sistemi operativi Windows che si trovano all'interno vengono loro [prodotti di Microsoft Support Lifecycle](https://support.microsoft.com/gp/lifeselect).|null|

> [!NOTE]
> Questo criterio si applica solo quando aggiornamenti automatici è configurato per eseguire installazioni pianificate degli aggiornamenti. Se l'impostazione dei criteri "Configura Aggiornamenti automatici" è disabilitato, questo criterio non ha alcun effetto.

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Specifica che un'installazione pianificata verrà avviato un minuto dopo che il computer è successivo.|
|**Attivata**|Specifica che l'installazione non ha luogo in precedenza si verificherà il numero specificato di minuti dopo che il computer viene avviato successivamente.|
|**Disattivata**|Specifica che un'installazione pianificata verrà eseguita con l'installazione pianificata successiva.|

**Opzioni:** Quando questa impostazione dei criteri è abilitata, è possibile utilizzarla per specificare un numero di minuti dopo il successivo avvio del computer, in cui si verificherà un'installazione pianificata che non è stata eseguita in precedenza.

#### <a name="specify-intranet-microsoft-update-service-location"></a>Specificare la posizione del servizio di aggiornamento Microsoft intranet
Specifica un server intranet che ospiterà gli aggiornamenti da Microsoft Update. È quindi possibile utilizzare WSUS per aggiornare automaticamente i computer sulla rete.

|Supportato in:|Esclusione:|
|---------|-------|
|Sistemi operativi Windows che si trovano all'interno vengono loro [prodotti di Microsoft Support Lifecycle](https://support.microsoft.com/gp/lifeselect).|Windows RT.|

Questa impostazione consente di specificare un server WSUS nella rete che verrà utilizzato come un servizio di aggiornamento interno. Invece di utilizzare Microsoft Updates su Internet, i client WSUS cercherà questo servizio per gli aggiornamenti applicabili.

Per utilizzare questa impostazione, è necessario impostare due valori di nome server: il server da cui il client rileva e scarica gli aggiornamenti e il server in cui le workstation aggiornate caricheranno le statistiche. I valori non devono essere diversi se entrambi i servizi sono configurati nello stesso server.

> [!NOTE]
> Se l'impostazione dei criteri "Configura Aggiornamenti automatici" è disabilitata, questo criterio non ha alcun effetto.

> [!NOTE]
> Questo criterio non è supportato in Windows RT. Abilita questo criterio non avrà alcun effetto nei computer che eseguono Windows RT.

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Se Aggiornamenti automatici non è disabilitato per criterio o preferenza utente, questo criterio specifica che i client si connettono direttamente al sito Windows Update su Internet.|
|**Attivata**|Specifica che il client si connette al server WSUS specificato, anziché Windows Update, per cercare e scaricare gli aggiornamenti. Se si abilita questa impostazione significa che gli utenti finali all'interno dell'organizzazione non è necessario passare attraverso un firewall per ottenere gli aggiornamenti, e offre la possibilità di verificare gli aggiornamenti prima di distribuirli.|
|**Disattivata**|Se Aggiornamenti automatici non è disabilitato per criterio o preferenza utente, questo criterio specifica che i client si connettono direttamente al sito Windows Update su Internet.|

**Opzioni:** Quando questa impostazione dei criteri è abilitata, è necessario specificare il servizio di aggiornamento Intranet che verrà utilizzato dai client WSUS per il rilevamento degli aggiornamenti e il server delle statistiche Internet a cui i client WSUS aggiornati caricherà le statistiche. Valori di esempio


|                    Opzione di impostazione:                    |    Valore di esempio    |
|-------------------------------------------------------|----------------------|
| Impostare il servizio di aggiornamento intranet per il rilevamento degli aggiornamenti |  http://wsus01:8530  |
|          Impostare il server delle statistiche intranet           | http://IntranetUpd01 |

#### <a name="turn-on-recommended-updates-via-automatic-updates"></a>Attiva aggiornamenti consigliati tramite aggiornamenti automatici
Specifica se Aggiornamenti automatici fornirà aggiornamenti importanti e consigliati da WSUS.

|Supportato in:|Esclusione:|
|---------|-------|
|a partire da Windows Vista, i sistemi operativi Windows che si trovano ancora nel ciclo di vita del [supporto dei prodotti Microsoft](https://support.microsoft.com/gp/lifeselect).|null|

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Specifica che Aggiornamenti automatici continuerà a fornire aggiornamenti importanti se è già configurato per eseguire questa operazione.|
|**Attivata**|Specifica che Aggiornamenti automatici installerà gli aggiornamenti consigliati e gli aggiornamenti importanti da WSUS.|
|**Disattivata**|Specifica che Aggiornamenti automatici continuerà a fornire aggiornamenti importanti se è già configurato per eseguire questa operazione.|

**Opzioni:** Non sono disponibili opzioni per questa impostazione.

#### <a name="turn-on-software-notifications"></a>Abilitazione delle notifiche del Software
Questa impostazione di criteri consente di controllare se gli utenti visualizzano i messaggi di notifica avanzata dettagliate sul software disponibile dal servizio Microsoft Update. I messaggi di notifica avanzata comunicare il valore e promuovono l'installazione e utilizzo di software opzionale. Questa impostazione deve essere utilizzato in ambienti gestititi in cui consentire l'accesso dell'utente finale per il servizio Microsoft Update.

Se non si utilizza il servizio Microsoft Update, l'impostazione dei criteri "notifiche software" non ha alcun effetto.

Se l'impostazione dei criteri "Configura Aggiornamenti automatici" è disabilitata o non è configurata, l'impostazione dei criteri "notifiche software" non ha alcun effetto.

|Supportato in:|Esclusione:|
|---------|-------|
|a partire da Windows Server 2008 (Windows Vista) e Windows 7, i sistemi operativi Windows che rientrano nel ciclo di vita del [supporto dei prodotti Microsoft](https://support.microsoft.com/gp/lifeselect).|null|

> [!NOTE]
> Per impostazione predefinita, questa impostazione è disabilitata.

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Gli utenti dei computer che eseguono Windows 7 non sono disponibili messaggi per le applicazioni facoltative. Gli utenti dei computer che eseguono Windows Vista non sono disponibili messaggi per le applicazioni facoltative o aggiornamenti. Un amministratore locale è possibile modificare questa impostazione tramite Pannello di controllo o un criterio locale.|
|**Attivata**|Se si abilita questa impostazione di criteri, nel computer dell'utente verrà visualizzato un messaggio di notifica quando è disponibile un software in primo piano. L'utente può fare clic sulla notifica per aprire Windows Update e ottenere ulteriori informazioni sul software o installarlo. L'utente può inoltre fare clic su **chiudere il messaggio** o **Mostra successivamente** per rinviare la notifica come appropriato.<br /><br />In Windows 7, questa impostazione di criteri consente di controllare solo notifiche dettagliate per le applicazioni facoltative. In Windows Vista, questa impostazione controlla le notifiche dettagliate per gli aggiornamenti e applicazioni facoltative.|
|**Disattivata**|Specifica che gli utenti che eseguono Windows 7 non verrà proposto messaggi di notifica dettagliate per le applicazioni facoltative e gli utenti che eseguono Windows Vista non verrà proposto i messaggi di notifica dettagliate per le applicazioni facoltative o aggiornamenti facoltativi.|

**Opzioni:** Non sono disponibili opzioni per questa impostazione.

### <a name="computer-configuration--maintenance-scheduler-policy-settings"></a>Configurazione computer > impostazioni dei criteri dell'utilità di pianificazione di manutenzione
Nell'impostazione Configura Aggiornamenti automatici, è stata selezionata l'opzione **4 - download automatico e pianificazione dell'installazione**, è possibile pianificare le impostazioni dell'utilità di pianificazione di manutenzione nella console GPMC per computer che eseguono Windows 8 e Windows RT. Se non è stata selezionata l'opzione 4 nell'impostazione "Configura Aggiornamenti automatici", non è necessario configurare queste impostazioni per gli aggiornamenti automatici. Le impostazioni dell'utilità di pianificazione di manutenzione si trovano nel percorso: *Policyname* > **Configurazione computer** > **criteri** > **modelli amministrativi** > **componenti Windows** > **utilità di pianificazione della manutenzione**. L'estensione dell'utilità di pianificazione di manutenzione dei criteri di gruppo contiene le seguenti impostazioni:

-   [Limite di attivazione manutenzione automatica](#automatic-maintenance-activation-boundary)

-   [Ritardo casuale manutenzione automatica](#automatic-maintenance-random-delay)

-   [Criteri di attivazione automatica](#automatic-wakeup-policy)

#### <a name="automatic-maintenance-activation-boundary"></a>Limite di attivazione di manutenzione automatica
Questo criterio consente di configurare l'impostazione "Limite di attivazione manutenzione automatica".

Il limite di attivazione di manutenzione è l'orario pianificato giornaliero in cui inizia la manutenzione automatica.

|Supportato in:|Esclusione:|
|---------|-------|
|Sistemi operativi Windows che si trovano all'interno vengono loro [prodotti di Microsoft Support Lifecycle](https://support.microsoft.com/gp/lifeselect).|null|

> [!NOTE]
> Questa impostazione è correlata all'opzione 4 **Configura Aggiornamenti automatici**. Se non è stata selezionata l'opzione 4 in **Configura Aggiornamenti automatici**, non è necessario configurare questa impostazione.

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Se questa impostazione di criteri non è configurata, verrà applicata l'ora pianificata giornaliera specificata nei computer client nel **centro operativo** >  pannello di controllo**manutenzione automatica** .|
|**Attivata**|Attivando questa impostazione esegue l'override di qualsiasi impostazione predefinita o modificare le impostazioni configurate nei computer client **Pannello di controllo** > **Centro operativo** > **manutenzione automatica** (o in alcune versioni di client, **manutenzione**).|
|**Disattivata**|Se si imposta questa impostazione di criteri su **disattivato**, l'ora pianificata giornaliera come specificato nel **centro operativo** > **manutenzione automatica**, nel pannello di controllo verrà applicato.|

#### <a name="automatic-maintenance-random-delay"></a>Ritardo casuale manutenzione automatica
Questa impostazione di criteri consente di configurare il ritardo casuale manutenzione automatica attivazione.

Il ritardo casuale manutenzione è la quantità di tempo fino a cui manutenzione automatica verrà ritardare l'avvio al limite di attivazione. Questa impostazione è utile per le macchine virtuali in cui casuale manutenzione può essere un requisito di prestazioni.

|Supportato in:|Esclusione:|
|---------|-------|
|Sistemi operativi Windows che si trovano all'interno vengono loro [prodotti di Microsoft Support Lifecycle](https://support.microsoft.com/gp/lifeselect).|null|

> [!NOTE]
> Questa impostazione è correlata all'opzione 4 **Configura Aggiornamenti automatici**. Se non è stata selezionata l'opzione 4 in **Configura Aggiornamenti automatici**, non è necessario configurare questa impostazione.

Per impostazione predefinita, quando abilitato, il ritardo casuale manutenzione regolare è **PT4H**.

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Un ritardo casuale di quattro ore viene applicato a **automatica**.|
|**Attivata**|Manutenzione automatica verrà ritardare l'avvio dal relativo limite di attivazione tramite fino alla quantità di tempo specificato.|
|**Disattivata**|Non viene applicato alcun ritardo casuale manutenzione automatica.|

#### <a name="automatic-wakeup-policy"></a>Criteri di attivazione automatica
Questa impostazione di criteri consente di configurare i criteri di riattivazione manutenzione automatica.

Il manutenzione dei criteri di attivazione consente di specificare se manutenzione automatica deve effettuare una richiesta di riattivazione per il computer operativo per la manutenzione pianificata giornaliera.

|Supportato in:|Esclusione:|
|---------|-------|
|Sistemi operativi Windows che si trovano all'interno vengono loro [prodotti di Microsoft Support Lifecycle](https://support.microsoft.com/gp/lifeselect).|null|

> [!NOTE]
> Se il criterio di riattivazione del computer operativo è disabilitato in modo esplicito, questa impostazione non ha alcun effetto.

> [!NOTE]
> Questa impostazione è correlata all'opzione 4 **Configura Aggiornamenti automatici**. Se non è stata selezionata l'opzione 4 in **Configura Aggiornamenti automatici**, non è necessario configurare questa impostazione.

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Se non si configura questa impostazione di criteri, verrà applicata l'impostazione di riattivazione come specificato nel **centro operativo** > **manutenzione automatica** pannello di controllo.|
|**Attivata**|Se si abilita questa impostazione di criteri, la manutenzione automatica tenterà di impostare un criterio di riattivazione del sistema operativo ed effettuerà una richiesta di riattivazione per l'ora pianificata giornaliera, se necessario.|
|**Disattivata**|Se si disabilita questa impostazione di criteri, verrà applicata l'impostazione di riattivazione come specificato nel **centro operativo** > **manutenzione automatica** pannello di controllo.|

### <a name="user-configuration--windows-update-policy-settings"></a>Configurazione utente > Impostazioni di criteri di Windows Update
In questa sezione vengono forniti dettagli sulle impostazioni di criteri basati sull'utente seguenti:

-   [Non visualizzare l'opzione "installa gli aggiornamenti e spegni" nella finestra di dialogo arresta Windows](#do-not-display-install-updates-and-shut-down-option-in-shut-down-windows-dialog)

-   [Non modificare l'opzione predefinita per "installa gli aggiornamenti e spegni" nella finestra di dialogo arresta Windows](#do-not-adjust-default-option-to-install-updates-and-shut-down-in-shut-down-windows-dialog)

-   [rimuovere l'accesso per usare tutte le funzionalità di Windows Update](#remove-access-to-use-all-windows-update-features)

Nella console Gestione criteri di ricerca le impostazioni utente per aggiornamenti automatici dei computer si trovano nel percorso: *Policyname* > **Configurazione utente** > **criteri** > **modelli amministrativi** > **componenti Windows** > **Windows Update**. Le impostazioni sono elencate nello stesso ordine in cui vengono visualizzate nelle estensioni configurazione computer e configurazione utente in Criteri di gruppo, quando si seleziona la scheda **Impostazioni** del criterio Windows Update per ordinare le impostazioni in ordine alfabetico.

> [!NOTE]
> Per impostazione predefinita, se non specificato diversamente, queste impostazioni non sono configurate.

> [!TIP]
> per ognuna di queste impostazioni, è possibile utilizzare la procedura seguente per abilitare, disabilitare o spostarsi tra le impostazioni:

#### <a name="do-not-display-install-updates-and-shut-down-option-in-shut-down-windows-dialog-box"></a>Non visualizzare l'opzione Installa aggiornamenti e spegni nella finestra di dialogo arresto di Windows
Specifica se il **Installa aggiornamenti e spegni** opzione viene visualizzata nel **Spegni** la finestra di dialogo.

|Supportato in:|Esclusione:|
|---------|-------|
|Sistemi operativi Windows che si trovano all'interno vengono loro [prodotti di Microsoft Support Lifecycle](https://support.microsoft.com/gp/lifeselect).|null|

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Specifica che il **Installa aggiornamenti e spegni** opzione verrà visualizzata nel **Spegni** la finestra di dialogo se sono disponibili aggiornamenti quando l'utente seleziona l'opzione Arresta per arrestare il computer.|
|**Attivata**|Se si abilita questa impostazione di criteri, l'opzione **Installa aggiornamenti e arresta** non verrà visualizzata come scelta nella finestra di dialogo **arresta Windows** , anche se gli aggiornamenti sono disponibili per l'installazione quando l'utente seleziona l'opzione arresta per arrestare il computer.|
|**Disattivata**|Specifica che il **Installa aggiornamenti e spegni** opzione verrà visualizzata nel **Spegni** la finestra di dialogo se sono disponibili aggiornamenti quando l'utente seleziona l'opzione Arresta per arrestare il computer.|

**Opzioni:** Non sono disponibili opzioni per questa impostazione.

#### <a name="do-not-adjust-default-option-to-install-updates-and-shut-down-in-shut-down-windows-dialog-box"></a>Non impostare l'opzione predefinita per "Installa gli aggiornamenti e spegni" nella finestra di dialogo arresto di Windows
Specifica se il **Installa aggiornamenti e spegni** l'opzione è consentita come scelta predefinita nel **Spegni** la finestra di dialogo.

|Supportato in:|Esclusione:|
|---------|-------|
|Sistemi operativi Windows che si trovano all'interno vengono loro [prodotti di Microsoft Support Lifecycle](https://support.microsoft.com/gp/lifeselect).|null|

> [!NOTE]
> Questa impostazione dei criteri non ha alcun effetto se la**Configurazione utente** *PolicyName* >   > **criteri** > **modelli amministrativi** > **componenti Windows** > **Windows Update**@no__ t-11**non Visualizza l'opzione "installa gli aggiornamenti e spegni" nella finestra di dialogo arresta Windows** è abilitata.

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Specifica se il **Installa aggiornamenti e spegni** opzione sarà l'opzione predefinita nel **Spegni** la finestra di dialogo se gli aggiornamenti disponibili per l'installazione al momento l'utente seleziona l'opzione Arresta per arrestare il computer.|
|**Attivata**|Specifica se ultimo arresto l'utente scelta (ad esempio, sospensione o riavvio) è l'opzione predefinita nel **arresto di Windows** la finestra di dialogo, indipendentemente dal fatto che il **opzione Installa aggiornamenti e spegni** è disponibile nel **scegliere seguenti?** menu.|
|**Disattivata**|Specifica se il **Installa aggiornamenti e spegni** opzione sarà l'opzione predefinita nel **Spegni** la finestra di dialogo se gli aggiornamenti disponibili per l'installazione al momento l'utente seleziona l'opzione Arresta per arrestare il computer.|

**Opzioni:** Non sono disponibili opzioni per questa impostazione.

#### <a name="remove-access-to-use-all-windows-update-features"></a>Rimuovere l'accesso per l'utilizzo di tutte le funzionalità di Windows Update
Questa impostazione consente di rimuovere l'accesso client di Windows Server Update SERVICES a Windows Update.

|Supportato in:|Esclusione:|
|---------|-------|
|Sistemi operativi Windows che si trovano all'interno vengono loro [prodotti di Microsoft Support Lifecycle](https://support.microsoft.com/gp/lifeselect).|null|

|||
|-|-|
|**Stato impostazione criterio**|**Comportamento**|
|**Non configurato**|Gli utenti sono in grado di connettersi al sito Web Windows Update.|
|**Attivata**|**Importante:** se abilitate, tutte le funzionalità di Windows Update vengono rimosse. Questo include il blocco dell'accesso al sito Web Windows Update all'https://windowsupdate.microsoft.com, dal collegamento ipertestuale Windows Update nel menu Start o nella schermata Start e anche dal menu **strumenti** in Internet Explorer. Aggiornamenti automatici di Windows è anche disabilitato. l'utente verrà alcuna notifica né ricevere gli aggiornamenti critici da Windows Update. Questa impostazione impedisce inoltre Device Manager installa automaticamente gli aggiornamenti dei driver dal sito Web Windows Update.<br /><br />Quando abilitato, è possibile configurare una delle seguenti opzioni di notifica:<br /><br />-   **0-non visualizza alcuna notifica**<br />    Questa impostazione verrà rimossi tutti gli accessi alle funzionalità di Windows Update e nessuna notifica verrà visualizzata.<br />-   **1-Mostra le notifiche di riavvio richieste**<br />    Questa impostazione verrà Mostra notifiche sui riavvii necessari per completare un'installazione. **Nota:** Nei computer che eseguono Windows 8 e Windows RT, se questo criterio è abilitato, verranno visualizzate solo le notifiche relative ai riavvii e l'impossibilità di rilevare gli aggiornamenti. Le opzioni di notifica non sono supportate. Le notifiche nella schermata di accesso vengono sempre visualizzate.|
|**Disattivata**|Gli utenti sono in grado di connettersi al sito Web Windows Update.|

**Opzioni:** Vedere **Enabled** nella tabella per questa impostazione.

## <a name="supplemental-information"></a>Informazioni aggiuntive
Questa sezione vengono fornite ulteriori informazioni sull'utilizzo di apertura e salvataggio delle impostazioni di WSUS in Criteri di gruppo e le definizioni dei termini utilizzati in questa Guida. Per gli amministratori familiari con le versioni precedenti di Windows Server Update SERVICES (WSUS 3.2 e versioni precedenti), è disponibile una tabella che riepiloga brevemente le differenze tra le versioni WSUS.

### <a name="accessing-the-windows-update-settings-in-group-policy"></a>Accesso alle impostazioni di Windows Update in Criteri di gruppo
La procedura descritta di seguito viene descritto come aprire la console GPMC sul controller di dominio. Quindi, la procedura descrive come aprire un oggetto gruppo di criteri di a livello di dominio esistente (GPO) per la modifica, o creare un nuovo GPO a livello di dominio e aprirlo e modificarlo.

> [!NOTE]
> È necessario essere un membro del **Domain Admins** gruppo o equivalente, per eseguire questa procedura.

##### <a name="to-open-or-add-and-open-a-group-policy-object"></a>Per aprire o aggiungere e aprire un oggetto Criteri di gruppo

1.  Nel controller di dominio, andare a **Server Manager**, > **strumenti**, > **Gestione criteri di gruppo**. Verrà visualizzata la Console Gestione Criteri di gruppo.

2.  Nel riquadro sinistro, espandere l'insieme di strutture. Ad esempio, fare doppio clic su **foresta: example.com**.

3.  Nel riquadro a sinistra, fare doppio clic su **domini**, quindi fare doppio clic sul dominio per il quale si desidera gestire un oggetto Criteri di gruppo. Ad esempio, fare doppio clic su **example.com**.

4.  Effettua una delle seguenti operazioni:

    -  **Per aprire un oggetto Criteri di gruppo esistente a livello di dominio per la modifica**, fare doppio clic sul dominio che contiene l'oggetto Criteri di gruppo che si desidera gestire, fare clic con il pulsante destro del mouse sui criteri del dominio che si desidera gestire, quindi fare clic su **modifica**. Si apre Criteri di gruppo Management Editor (Editor gestione criteri).

    -  **Per creare un nuovo oggetto Criteri di gruppo e aprire per la modifica**:
        1.  Fare clic con il pulsante destro del mouse sul dominio per il quale si desidera creare un nuovo oggetto Criteri di gruppo, quindi fare clic su **Crea un oggetto Criteri di gruppo in questo dominio e collegarlo qui**.

        2.  In **nuovo GPO**, in **nome**, digitare un nome per il nuovo oggetto Criteri di gruppo e quindi fare clic su **OK**.

        3.  Fare clic con il pulsante destro del mouse sul nuovo oggetto Criteri di gruppo, quindi scegliere **modifica**. Verrà visualizzata la finestra di EDITOR.

##### <a name="to-open-the-windows-update-or-maintenance-scheduler-extensions-of-group-policy"></a>Per aprire le estensioni di Windows Update o utilità di pianificazione di manutenzione dei criteri di gruppo

1.  In Criteri di gruppo editor di gestione eseguire una delle operazioni seguenti:

    -   **Aprire il > configurazione computer Windows Update estensione di criteri di gruppo**. Passare a: *Policyname* > **Configurazione computer** > **criteri** / **modelli amministrativi** > **componenti Windows** > **Windows Update**.

    -   **Aprire la configurazione utente > estensione di Windows Update di criteri di gruppo**. Passare a: *Policyname* > **Configurazione utente** > **criteri** > **modelli amministrativi** > **componenti Windows** > **Windows Update**.

    -   **Aprire la configurazione del computer > estensione dell'utilità di pianificazione di manutenzione di criteri di gruppo**. In GPOE passare a *policyname* > **computer Configuration** > **policies** > **Modelli amministrativi** > **Windows Components** > **Maintenance Scheduler**.

Per ulteriori informazioni sui criteri di gruppo, vedere [Cenni preliminari sui criteri di gruppo](https://technet.microsoft.com/library/hh831791.aspx(v=ws.12)).

> [!TIP]
> Dopo avere aperto l'estensione di criteri di gruppo che si desidera, è possibile utilizzare la procedura seguente per abilitare, disabilitare o spostarsi tra le impostazioni:

##### <a name="to-configure-group-policy-settings"></a>Per configurare le impostazioni di criteri di gruppo

1.  In *ExtensionOfGroupPolicy*, fare doppio clic su quella che si desidera visualizzare o modificare.

2.  Per configurare le impostazioni, effettuare una delle operazioni seguenti:

    -   Per mantenere lo stato predefinito non specificato dell'impostazione, selezionare **non configurato**.

    -   Per abilitare l'impostazione, selezionare **abilitato**.

    -   Per disabilitare l'impostazione, selezionare **disabilitato**.

3.  In **Opzioni**, se sono elencate le opzioni, mantenere i valori predefiniti o modificarli in base alle esigenze.

4.  Effettua una delle seguenti operazioni:

    -   Per salvare le modifiche e continuare a quella successiva, fare clic su **Applica**, quindi fare clic su **impostazione successiva**.

    -   Per salvare le modifiche e chiudere la finestra di dialogo, fare clic su **OK**.

    -   Per annullare tutte le modifiche non salvate e chiudere la finestra di dialogo, fare clic su **Annulla**.

### <a name="changes-to-wsus-relevant-to-this-guide"></a>Modifiche apportate a WSUS pertinente per questa Guida
Nella tabella seguente sono riepilogate le differenze principali tra le versioni correnti e precedenti di Windows Server Update SERVICES che sono rilevanti per questa Guida.

|Versioni di Windows Server e Windows Server Update SERVICES|Descrizione|
|------------------|--------|
| Windows Server 2012 R2 con Windows Server Update SERVICES 6.0 e versioni successive|a partire da Windows Server 2012, il ruolo server WSUS è integrato con il sistema operativo e le impostazioni Criteri di gruppo associate per i client WSUS sono, per impostazione predefinita, incluse nel Criteri di gruppo.|
| Windows Server 2008 (e versioni precedenti di Windows Server) con WSUS 3.2 e versioni precedenti|In Windows Server 2008 e versioni precedenti di Windows Server tramite WSUS 3.2 (e versioni precedenti), le impostazioni di criteri di gruppo che controllano i client WSUS non sono inclusi in questi sistemi operativi Windows Server. Le impostazioni dei criteri sono nel modello di amministrazione di WSUS, **Wuau. adm**. In queste versioni di server, il modello amministrativo di WSUS deve essere prima aggiunto nella Console di gestione di criteri di gruppo (GPMC) prima che possano essere configurate le impostazioni del client WSUS.|

### <a name="terms-and-definitions"></a>Termini e definizioni
Seguito è riportato un elenco dei termini utilizzati in questa Guida.

|Nome|Definizione|
|----|-------|
|Aggiornamenti automatici|**Un servizio in esecuzione in computer Windows** (aggiornamenti automatici): Si riferisce al componente computer client integrato nei sistemi operativi Microsoft Windows Vista, Windows Server 2003, Windows XP e Windows 2000 con SP3 per ottenere gli aggiornamenti da Microsoft Update o Windows Update.<br /><br />**Riferimento occasionale** (aggiornamenti automatici): Termine utilizzato per descrivere quando l'agente di Windows Update pianifica e Scarica automaticamente gli aggiornamenti.|
|server autonomi|Utilizzare per fare riferimento a un server downstream di Windows Server Update Services (WSUS) in cui gli amministratori possono gestire i componenti di Windows Server Update SERVICES.|
|server downstream|Utilizzare per fare riferimento a un server Windows Server Update Services (WSUS) che ottiene gli aggiornamenti da un altro server WSUS piuttosto che da Microsoft Update o Windows Update.|
|Estensione criteri di gruppo (e: estensione di criteri di gruppo|Una raccolta di impostazioni in Criteri di gruppo che vengono utilizzati per controllare come utenti e computer (a cui i criteri vengono applicati) possono configurare e utilizzare i vari servizi di Windows e funzionalità. Gli amministratori possono utilizzare WSUS con criteri di gruppo per la configurazione lato client del client di aggiornamenti automatici, al fine di garantire che gli utenti finali non possono disattivare o aggirare i criteri di aggiornamento aziendale.<br /><br />WSUS non richiede l'utilizzo di Active Directory o Criteri di gruppo. Configurazione del client può essere applicata anche tramite criteri di gruppo locali o modificando il Registro di sistema di Windows.|
|servizio di aggiornamento interno|Riferimento casuale a un'infrastruttura di rete che utilizza uno o più server WSUS per distribuire gli aggiornamenti.|
|server di replica|Utilizzare per fare riferimento a un server Windows Server Update Services (WSUS) a valle che rispecchia le approvazioni e le impostazioni del server padre a cui è connesso. È possibile gestire WSUS in un server di replica.|
|Microsoft Update|**Un sito di download Microsoft basato su Internet:** Sito Internet Microsoft che archivia e distribuisce gli aggiornamenti per i computer Windows (driver di dispositivo), i sistemi operativi Windows e altri prodotti software Microsoft.|
|Software Update Services (SUS)|SUS è il prodotto precedente per Windows Server Update Services (WSUS).|
|aggiornamenti|Qualsiasi valore di una raccolta di revisioni del software, aggiornamenti rapidi, service pack, feature pack e i driver di dispositivo che possono essere installati in un computer per estendere le funzionalità o migliorare le prestazioni e sicurezza.|
|file di aggiornamento|I file necessari per installare un aggiornamento in un computer.|
|informazioni sugli aggiornamenti (noto anche come i metadati dell'aggiornamento)|Informazioni su un aggiornamento, anziché i file binari di aggiornamento in un pacchetto di aggiornamento. Ad esempio, i metadati forniscono informazioni per le proprietà di un aggiornamento, consentendo di individuare per quali l'aggiornamento è utile. Inoltre, i metadati includono condizioni di licenza Software Microsoft. Il pacchetto di metadati scaricato per un aggiornamento è in genere molto inferiore rispetto al pacchetto di file di aggiornamento effettivo.|
|aggiornare l'origine|Il percorso in cui un server Windows Server Update Services (WSUS) viene sincronizzato per ottenere i file di aggiornamento. Questo percorso può essere Microsoft Update o un server WSUS upstream.|
|server upstream|Un server Windows Server Update Services (WSUS) che fornisce i file di aggiornamento a un altro server WSUS, che a sua volta viene considerato come un server downstream.|
|Windows Server Update Services (WSUS)|Un programma di ruolo del Server che viene eseguito in uno o più computer Windows Server in una rete aziendale. Un'infrastruttura WSUS consente di gestire gli aggiornamenti per computer sulla rete per l'installazione.<br /><br />È possibile utilizzare WSUS per approvare o rifiutare gli aggiornamenti prima del rilascio, per forzare gli aggiornamenti per l'installazione da una determinata data, e per ottenere report estesi su quali aggiornamenti ogni computer della rete richiede. È possibile configurare WSUS per approvare automaticamente determinate classi di aggiornamenti (gli aggiornamenti critici, aggiornamenti della protezione, service pack, driver e così via). WSUS consente inoltre di approvare gli aggiornamenti per "rilevamento" solo, in modo che è possibile visualizzare i computer che richiederanno un aggiornamento specificato senza dover installare gli aggiornamenti.<br /><br />In un'implementazione di WSUS, almeno un server WSUS nella rete deve essere in grado di connettersi a Microsoft Update per ottenere gli aggiornamenti disponibili. In base alla configurazione e sicurezza di rete, l'amministratore può stabilire quanti altri server possono connettersi direttamente a Microsoft Update.<br /><br />È possibile configurare un server WSUS per ottenere gli aggiornamenti su Internet da tali posizioni come:<br /><br />-il pubblico di Microsoft Update<br />-il pubblico di Windows Update<br />-Microsoft Store|
|Windows Update|**Un sito di download Microsoft basato su Internet:** Sito Internet Microsoft che archivia e distribuisce gli aggiornamenti per i computer Windows (driver di dispositivo) e i sistemi operativi Windows.<br /><br />**servizio computer:** Nome del servizio Windows Update eseguito nei computer. Windows Update rileva, scarica e installa gli aggiornamenti nei computer Windows.<br /><br />A seconda del computer e configurazioni di criteri, l'agente Windows Update possono scaricare gli aggiornamenti da:<br /><br />-Microsoft Update<br />-Windows Update<br />-Microsoft Store<br />-Un servizio di aggiornamento di Internet (rete) (WSUS)<br /><br />i computer che non sono gestiti in un ambiente basato su WSUS utilizzeranno in genere Windows Update per connettersi direttamente tramite Internet a Windows Update, Microsoft Update o Microsoft Store per ottenere gli aggiornamenti.|
|Client WSUS|Un computer che riceve gli aggiornamenti da un servizio di aggiornamento WSUS intranet.<br /><br />Nel caso di impostazioni di criteri di gruppo che controllano l'interazione dell'utente finale con aggiornamenti automatici: un utente di un computer in un ambiente Windows Server Update SERVICES.|
