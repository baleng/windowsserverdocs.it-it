---
title: Client Desktop remoto domande frequenti
description: Domande frequenti su client di Desktop remoto
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 785a18cf-a5d0-4bc2-95e4-9ef53ee8f65a
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 07/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: e6f91aa02cd0f19d480c24309be5797c273b0f2e
ms.sourcegitcommit: d888e35f71801c1935620f38699dda11db7f7aad
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66804954"
---
# <a name="frequently-asked-questions-about-the-remote-desktop-clients"></a>Domande frequenti su client di Desktop remoto

>Si applica a: Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

Ora che è stato configurato il client Desktop remoto nel dispositivo (Android, Mac, iOS o Windows), è possibile domande. Di seguito sono fornite le risposte alle domande più frequenti sul client Desktop remoto. 

- [Configurazione di](#setting-up)
- [Le connessioni, gateway e reti](#connection-gateway-and-networks)
- [client Web](#web-client)
- [Audio, monitor e mouse](#monitors-audio-and-mouse)
- [Hardware Mac](#mac-client---hardware-questions)
- [Specifici messaggi di errore](#specific-errors)

La maggior parte di queste domande si applicano a tutti i client, ma esistono alcuni elementi specifici di client.

Se hai altre domande che si desidera contattarci per rispondere, lasciarle come commenti e suggerimenti in questo articolo.

## <a name="setting-up"></a>Impostazione di

### <a name="which-pcs-can-i-connect-to"></a>Dei PC che è possibile connettersi a

Estrarre il [configurazione supportata](remote-desktop-supported-config.md) per informazioni su quali computer è possibile connettersi.

### <a name="how-do-i-set-up-a-pc-for-remote-desktop"></a>Come configurare un PC per Desktop remoto?

Ho configurato il dispositivo, ma non credo pronto del PC. aiuto?

Innanzitutto, hai visto l'installazione guidata di Remote Desktop? Ne descrive le operazioni preliminari per l'accesso remoto al computer. Download ed eseguire strumento nel PC per ottenere tutti gli elementi impostato. 

In caso contrario, se si preferisce eseguire manualmente operazioni, continuare a leggere.

Per Windows 10, eseguire le operazioni seguenti:

1. Sul dispositivo si desidera connettersi, aprire **impostazioni**.
2. Selezionare **System** e quindi **Desktop remoto**.
3. Usare il dispositivo di scorrimento per abilitare Desktop remoto.
4. In generale, è consigliabile mantenere i PC attivi e individuabile per facilitare le connessioni. Fare clic su **Mostra le impostazioni** per passare alle impostazioni di risparmio energia del PC, in cui è possibile modificare questa impostazione.
   > [!NOTE]
   > Non è possibile connettersi a un computer che è in modalità sospensione o ibernazione, quindi verificare che le impostazioni di sospensione e ibernazione nel computer remoto è impostate su **Never**. (La sospensione non è disponibile in tutti i PC.)


Prendere nota del nome di questo PC sotto **come connettersi a questo PC**. È necessario per configurare i client.

È possibile concedere l'autorizzazione per determinati utenti per accedere a questo PC - per eseguire questa operazione, fare clic su **selezionare gli utenti che possono accedere in remoto il PC**.
I membri del gruppo Administrators hanno automaticamente accesso.

Per Windows 8.1, seguire le istruzioni per consentire le connessioni remote in [connettersi a un altro desktop mediante connessioni Desktop remoto](https://support.microsoft.com/en-us/help/17463/windows-7-connect-to-another-computer-remote-desktop-connection#1TC=windows-8).



## <a name="connection-gateway-and-networks"></a>Connessione gateway e reti

### <a name="why-cant-i-connect-using-remote-desktop"></a>Il motivo per cui non è possibile connettersi tramite Desktop remoto?

Ecco alcune possibili soluzioni a problemi comuni che possono verificarsi quando si tenta di connettersi a un computer remoto. Se queste soluzioni non funzionano, è possibile trovare ulteriori informazioni sul [sito Web Community Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=242079).

- **Impossibile trovare il computer remoto.** Assicurarsi di avere il nome PC a destra e quindi verificare se tale nome è stato immesso correttamente. Non è ancora possibile connettersi, provare a usare l'indirizzo IP del computer remoto anziché il nome del computer.
- **Si è verificato un problema con la rete.** Assicurarsi di avere accesso a Internet. 
- **La porta di Desktop remoto potrebbe essere bloccata da un firewall.** Se si utilizza Windows Firewall, seguire questi passaggi:

  1. Aprire Windows Firewall. 
  2. Fare clic su **Consenti app o funzionalità attraverso Windows Firewall**. 
  3. Fare clic su **modificare le impostazioni**. È possibile che venga richiesto per una password di amministratore o di confermare la scelta.
  4. In **applicazioni e funzionalità consentiti**, selezionare **Desktop remoto**, e quindi toccare o fare clic su **OK**.

     Se si utilizza un firewall diverso, assicurarsi che la porta per Desktop remoto (in genere la 3389) sia aperta.
- **Le connessioni remote potrebbero non essere configurate nel computer remoto.** Per risolvere questo problema, scorrere tornando alla [come configuro un PC per Desktop remoto?](#how-do-i-set-up-a-pc-for-remote-desktop) domanda in questo argomento.
- **Sul computer remoto potrebbe consentire solo PC per la connessione con autenticazione a livello di rete impostato.** 
- **Sul computer remoto potrebbe essere spento.** Non è possibile connettersi a un computer è spento, nello stato di sospensione o ibernazione, quindi verificare che le impostazioni di sospensione e ibernazione nel computer remoto è impostate su **mai** (modalità di sospensione non è disponibile in tutti i PC.).

### <a name="why-cant-i-find-or-connect-to-my-pc"></a>Impossibile trovare o connettersi al computer.

Verificare quanto segue:

- È il PC in e attivi?
- È stato immesso il nome corretto o l'indirizzo IP?

   > [!IMPORTANT]
   > Usando il nome PC richiede la rete per risolvere il nome corretto tramite DNS. In molte reti domestiche, è necessario utilizzare l'indirizzo IP anziché il nome host per la connessione.
- È il PC in una rete diversa? È stato configurato il PC per consentire all'esterno di connessioni tramite?  Consulta [consentire l'accesso al PC dall'esterno della rete](remote-desktop-allow-outside-access.md) per assistenza.
- Ci si sta connettendo a una versione supportata di Windows? 

   > [!NOTE]
   > Windows XP Home Edition, Windows Media Center Edition, Windows Vista e Windows 7 Home o Starter non sono supportate senza 3 software di terze parti.

### <a name="why-cant-i-sign-in-to-a-remote-pc"></a>Perché non posso accedere a un computer remoto?

Se è possibile visualizzare la schermata di accesso del PC remoto, ma non è possibile accedere, è possibile che non sono state aggiunte al gruppo utenti Desktop remoto o a qualsiasi gruppo con diritti di amministratore nel computer remoto. Chiedere all'amministratore di sistema per eseguire questa operazione.

### <a name="which-connection-methods-are-supported-for-company-networks"></a>Sono supportati i metodi di connessione per reti aziendali?

Se si desidera accedere al desktop di office dall'esterno della rete aziendale, la società deve fornire un mezzo di accesso remoto. Il Client desktop remoto supporta attualmente le operazioni seguenti:

- Gateway di Terminal Server o Gateway Desktop remoto
- Accesso Web Desktop remoto
- VPN (tramite opzioni VPN incorporate iOS)

### <a name="vpn-doesnt-work"></a>VPN non funziona

Problemi VPN possono avere cause diverse. Il primo passaggio consiste nel verificare che la connessione VPN funziona nella stessa rete del computer Mac o PC. Se non è possibile testare con un PC o Mac, è possibile accedere a una pagina web intranet aziendale con il browser del dispositivo.

Controllare gli altri elementi:
- **Rete 3G blocca o danneggia VPN.** Esistono diversi provider 3G nel mondo che sembrano danneggiati traffico 3G o blocco. Verificare la connettività VPN funziona correttamente per più di un minuto.
- **L2TP o PPTP VPN.** Se si utilizza nella VPN L2TP o PPTP, impostare inviare tutto il traffico su ON nella configurazione VPN.
- **VPN è configurato correttamente.** Una configurazione errata del server VPN può essere il motivo le connessioni VPN mai lavorano o ha smesso di funzionare dopo un certo tempo. Assicurarsi che il test con iOS, web browser del dispositivo o un PC o Mac nella stessa rete in questo caso.

### <a name="how-can-i-test-if-vpn-is-working-properly"></a>Come posso verificare se funziona correttamente VPN?

Verificare che sia abilitata la VPN nel dispositivo. Passare a una pagina Web nella rete interna o utilizzando un servizio web disponibile solo tramite la connessione VPN, è possibile testare la connessione VPN.

### <a name="how-do-i-configure-l2tp-or-pptp-vpn-connections"></a>Configurazione delle connessioni VPN PPTP o L2TP

Se si utilizza L2TP o PPTP nella VPN, assicurarsi di impostare **Invia tutto il traffico** a **via** nella configurazione VPN.

## <a name="web-client"></a>client Web

### <a name="which-browsers-can-i-use"></a>Quali browser è possibile usare?

Il client web supporta Microsoft Edge, Internet Explorer 11, Mozilla Firefox (v55.0 e versioni successive), Safari e Google Chrome.

### <a name="what-pcs-can-i-use-to-access-the-web-client"></a>Quali computer è possibile usare per accedere al client web?

Il client web supporta Windows, macOS, Linux e ChromeOS. I dispositivi mobili non sono supportati in questo momento.

### <a name="can-i-use-the-web-client-in-a-remote-desktop-deployment-without-a-gateway"></a>È possibile usare il client web in una distribuzione di Desktop remoto senza un gateway?

No. Il client richiede un Gateway Desktop remoto per la connessione. Non sapere che cosa significa? Chiedere all'amministratore su di esso.

### <a name="does-the-remote-desktop-web-client-replace-the-remote-desktop-web-access-page"></a>Il client di web Desktop remoto sostituisce la pagina di accesso Web Desktop remoto?

No. Il client di web Desktop remoto è ospitato in un URL diverso rispetto alla pagina di accesso Web Desktop remoto. È possibile usare il client web o pagina di accesso Web per visualizzare le risorse remote in un browser.

### <a name="can-i-embed-the-web-client-in-another-web-page"></a>È possibile si incorporano il client web in un'altra pagina web?

Questa funzionalità non è supportata al momento.

## <a name="monitors-audio-and-mouse"></a>Audio, monitor e mouse

### <a name="how-do-i-use-all-of-my-monitors"></a>Come è possibile utilizzare tutti i monitor?
Per utilizzare due o più schermate, eseguire le operazioni seguenti:

1. Fare doppio clic su desktop remoto che si desidera abilitare più schermate per e quindi fare clic su **modifica**.
2. Abilitare **utilizzare tutti i monitoraggi** e **schermo**.

### <a name="is-bi-directional-sound-supported"></a>Audio bidirezionale è supportata?
Audio a monte (dal client al server, per microfoni) non è supportata dal Client Desktop remoto.

### <a name="what-can-i-do-if-the-sound-wont-play"></a>Cosa può fare se non riproduce il suono?
Disconnette la sessione (non solo disconnettere, disconnettersi completamente) e quindi accedere di nuovo.

## <a name="mac-client---hardware-questions"></a>Client Mac - domande hardware
### <a name="is-retina-resolution-supported"></a>Risoluzione retina è supportata?
Sì, il client desktop remoto supporta la risoluzione retina.

### <a name="how-do-i-enable-secondary-right-click"></a>Come è possibile abilitare rapida secondario?
Per utilizzare il pulsante destro del mouse all'interno di una sessione aperta sono disponibili tre opzioni:

- Mouse USB a standard PC due pulsanti
- Apple Magic Mouse: Per abilitare il pulsante destro del mouse, fare clic su **preferenze di sistema** in ancoraggio, fare clic su **Mouse**, quindi abilitare **secondario fare clic su**.
- Apple Magic Trackpad o MacBook Trackpad: Per abilitare il pulsante destro del mouse, fare clic su **preferenze di sistema** in ancoraggio, fare clic su **Mouse**, quindi abilitare **secondario fare clic su**.

### <a name="is-airprint-supported"></a>AirPrint è supportato?
No, il client Desktop remoto non supporta AirPrint. (Questo è true per i client Mac e iOS).

### <a name="why-do-incorrect-characters-appear-in-the-session"></a>Perché inclusi caratteri non validi vengono visualizzati nella sessione?
Se si utilizza una tastiera internazionale, è possibile visualizzare un problema in cui i caratteri visualizzati nella sessione corrisponde ai caratteri digitato sulla tastiera Mac.

Ciò può verificarsi nei seguenti scenari:

- Si sta utilizzando una tastiera che non riconosce la sessione remota. Se Desktop remoto non riconosce la tastiera, per impostazione predefinita la lingua utilizzata l'ultima volta con il computer remoto.
- Ci si connette a una sessione disconnessa in precedenza in un computer remoto e che PC remoto utilizza una lingua di tastiera diversa da quella di attualmente si sta tentando di utilizzare.

È possibile risolvere questo problema impostando manualmente la lingua della tastiera per la sessione remota. Vedere i passaggi nella sezione successiva.

### <a name="how-do-language-settings-affect-keyboards-in-a-remote-session"></a>Come vengono applicate impostazioni relative alle lingue tastiere in una sessione remota?
Esistono molti tipi di layout di tastiera Mac. Alcune di queste sono layout specifici Mac o layout personalizzati per il quale una corrispondenza esatta potrebbe non essere disponibile nella versione di Windows si è .NET remoting in. La sessione remota viene eseguito il mapping della tastiera sulla migliore corrispondenti alla lingua della tastiera disponibile nel computer remoto. 

Se il layout di tastiera Mac è impostato su dovrebbe funzionare solo alla versione PC di tutte le chiavi devono essere mappate correttamente la tastiera nella lingua (ad esempio, francese-PC) e la tastiera.

Se è impostato il layout di tastiera Mac alla versione Mac di una tastiera (ad esempio, francese) la sessione remota verrà eseguito il mapping è alla versione PC di lingua francese. Alcune delle scelte rapide da tastiera Mac che è utilizzato per l'utilizzo in OSX non funzionerà nella sessione remota di Windows.

Se il layout di tastiera è impostato su una variante di una lingua (ad esempio, francese (Canada)) e la sessione remota non può associare tale variazione esatta, la sessione remota verrà eseguito il mapping è il linguaggio più vicino (ad esempio, francese). Alcune delle scelte rapide da tastiera Mac che è utilizzato per l'utilizzo in OSX non funzionerà nella sessione remota di Windows.

Se il layout di tastiera è impostato su un layout che della sessione remota non può corrispondere a tutti, verrà automaticamente la sessione remota per fornire la lingua che è utilizzata l'ultima volta con il PC. In questo caso, o nei casi in cui è necessario modificare la lingua della sessione remota in modo che corrisponda tastiera Mac, è possibile impostare manualmente la lingua della tastiera nella sessione remota per la lingua che è la corrispondenza più vicina a quella che si desidera utilizzare come indicato di seguito.

Utilizzare le istruzioni seguenti per modificare il layout di tastiera all'interno della sessione di desktop remoto:

**In Windows 10 o Windows 8:**

1. All'interno della sessione remota, aprire paese e lingua. Fare clic su **Start > Impostazioni > ora e la lingua**. Aprire **paese e lingua**.
2. Aggiungere la lingua che si desidera utilizzare. Quindi chiudere la finestra di paese e lingua.
3. A questo punto, nella sessione remota, si noterà la possibilità di passare tra i linguaggi. (Nella parte destra della sessione remota, accanto all'orologio.) Selezionare la lingua che si desidera passare (ad esempio **Eng**).

Potrebbe essere necessario chiudere e riavviare l'applicazione in uso per la tastiera modifica diventino effettive.


## <a name="specific-errors"></a>Errori specifici

### <a name="why-do-i-get-an-insufficient-privileges-error"></a>Perché viene visualizzato un errore "Privilegi insufficienti"?
Non è consentito accedere alla sessione in cui che si desidera connettersi. La causa più probabile è che si sta tentando di connettersi a una sessione di amministrazione. Solo gli amministratori sono autorizzati a connettersi alla console. Verificare che la console è disattiva nelle impostazioni avanzate di desktop remoto. Se non è l'origine del problema, contattare l'amministratore di sistema per ulteriore assistenza.

### <a name="why-does-the-client-say-that-there-is-no-cal"></a>Perché il client si supponga che non vi sia alcuna licenza CAL
Quando un client di desktop remoto si connette a un server di Desktop remoto, il server rilascia un Remote Desktop Services licenza di accesso Client (CAL Servizi Desktop REMOTO) archiviato dal client. Ogni volta che il client si connette nuovamente verranno utilizzate le CAL RDS e il server non creerà un'altra licenza. Se le Licenze CAL sul dispositivo è mancante o danneggiato, il server rilascerà un'altra licenza. Quando viene raggiunto il numero massimo di dispositivi con licenza server non creerà nuove licenze CAL Servizi Desktop REMOTO. Per assistenza, contattare l'amministratore di rete.

### <a name="why-did-i-get-an-access-denied-error"></a>Perché viene visualizzato un errore "Accesso negato"?
L'errore "Accesso negato" è un oggetto generato dal Gateway Desktop remoto e il risultato di credenziali non corrette durante il tentativo di connessione. Verificare il nome utente e password. Se la connessione ha lavorato prima e l'errore si è verificato di recente, possibilmente modificato la password dell'account utente Windows e non ancora aggiornate nelle impostazioni di desktop remote.

### <a name="what-does-rpc-error-23014-or-error-0x59e6-mean"></a>Che cosa significa "Errore RPC 23014" o Media "Errore 0x59e6"?
In caso di un **errore RPC 23014** o **errore 0x59E6 riprovare dopo alcuni minuti**, il server Gateway Desktop remoto ha raggiunto il numero massimo di connessioni attive. A seconda della versione di Windows in esecuzione su Gateway Desktop remoto il numero massimo di connessioni è diversa: L'implementazione di Windows Server 2008 R2 Standard limita il numero di connessioni a 250. L'implementazione di Windows Server 2008 R2 Foundation limita il numero di connessioni a 50. Tutte le altre implementazioni di Windows consentono un numero illimitato di connessioni.

### <a name="what-does-the-failed-to-parse-ntlm-challenge-error-mean"></a>Che cosa significa l'errore "Impossibile analizzare sfida NTLM"?
Questo errore è causato da un'errata configurazione nel computer remoto. Verificare che l'impostazione del livello di protezione RDP nel computer remoto è impostato su "Compatibile con Client". (Rivolgersi all'amministratore di sistema se ti serve assistenza in questo modo.)

### <a name="what-does-tsrap-you-are-not-allowed-to-connect-to-the-given-host-mean"></a>Funzionamento di "TS_RAP non è consentito connettersi all'host specificato" significa?
Questo errore si verifica quando un criterio di autorizzazione risorse nel server gateway si arresta il proprio nome utente di connettersi al computer remoto. Questa situazione può verificarsi nei casi seguenti:

- Il nome del computer remoto è identico al nome del gateway. Quindi, quando si prova a connettersi al computer remoto, l'interruzione della connessione al gateway, invece, che probabilmente non si dispone dell'autorizzazione per accedere. Se è necessario connettersi al gateway, non utilizzare il nome del gateway esterno come nome del computer. Usare invece "localhost" o l'indirizzo IP (127.0.0.1) o il nome del server interno.
- L'account utente non è un membro del gruppo di utenti per l'accesso remoto.