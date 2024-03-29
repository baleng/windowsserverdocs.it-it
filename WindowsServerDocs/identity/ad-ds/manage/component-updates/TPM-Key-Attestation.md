---
ms.assetid: 16a344a9-f9a6-4ae2-9bea-c79a0075fd04
title: Attestazione chiave TPM
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: d7104daaa10cf7093370cb309e0366e1ab2b9b51
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389857"
---
# <a name="tpm-key-attestation"></a>Attestazione chiave TPM

>Si applica a: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**Autore**: Justin Turner, Senior Support Escalation Engineer con il gruppo di Windows  
  
> [!NOTE]  
> Questo contenuto è stato redatto da un ingegnere del Supporto tecnico Microsoft ed è destinato ad amministratori esperti e architetti di sistemi che desiderano una spiegazione tecnica delle funzionalità e delle soluzioni relative a Windows Server 2012 R2 più approfondita rispetto agli argomenti solitamente disponibili su TechNet. Non è stato tuttavia sottoposto agli stessi passaggi redazionali e, di conseguenza, per alcune lingue potrebbe essere meno accurato della documentazione che si trova in genere su TechNet.  
  
## <a name="overview"></a>Panoramica  
Mentre il supporto per le chiavi protette da TPM esistente dal Windows 8, non vi sono alcun meccanismo per le CA a livello di crittografia attestare che la chiave privata del certificato richiedente è effettivamente protetto da un modulo TPM (Trusted Platform). Questo aggiornamento consente a un'autorità di certificazione per eseguire tale attestazione e per riflettere tale attestazione nel certificato emesso.  
  
> [!NOTE]  
> Questo articolo si presuppone che il lettore abbia familiarità con il concetto di modello certificato (per riferimento, vedere [modelli di certificato](https://technet.microsoft.com/library/cc730705.aspx)). Si presuppone inoltre che il lettore abbia familiarità con la configurazione delle CA globali (Enterprise) per emettere certificati basati sui modelli di certificato. per informazioni di riferimento, vedere [Checklist: Configurare CA per rilasciare e gestire i certificati @ no__t-0).  
  
### <a name="terminology"></a>Terminologia  
  
|Nome|Definizione|  
|--------|--------------|  
|VERIFICA DELL'AUTENTICITÀ|Chiave di verifica dell'autenticità. Si tratta di una chiave asimmetrica contenuta all'interno del TPM (introdotto in fase di produzione). La verifica dell'AUTENTICITÀ è univoco per ogni TPM e possibile identificarlo. La verifica dell'AUTENTICITÀ non può essere modificata o rimossa.|  
|EKpub|Fa riferimento alla chiave pubblica della verifica dell'AUTENTICITÀ.|  
|EKPriv|Fa riferimento alla chiave privata della verifica dell'AUTENTICITÀ.|  
|EKCert|Certificato di verifica dell'AUTENTICITÀ. Un certificato emesso dal produttore del TPM per EKPub. TPM non tutti sono EKCert.|  
|TPM|Trusted Platform Module. Un TPM è progettato per fornire funzioni correlate alla sicurezza basate su hardware. Un chip TPM è un cryptoprocessor sicuro progettato per eseguire operazioni di crittografia. Il chip include più meccanismi di sicurezza fisica in grado di proteggerlo da manomissioni; il software dannoso non sarà pertanto in grado di manomettere le funzioni di sicurezza del TPM.|  
  
### <a name="background"></a>Sfondo  
A partire da Windows 8, un modulo TPM (Trusted Platform) può essere utilizzato per proteggere la chiave privata del certificato. Il Microsoft Platform Crypto Provider di archiviazione Provider chiavi (KSP) abilita questa funzionalità. Sono presenti due problemi con l'implementazione:  

-   Non c'era alcuna garanzia che una chiave sia effettivamente protetta da un TPM (un utente può facilmente effettuare lo spoofing di un provider di archiviazione chiavi software come KSP del TPM con credenziali di amministratore locale).

-   Non è stato possibile limitare l'elenco dei moduli TPM che sono autorizzati a proteggere l'azienda ha rilasciato i certificati (nel caso in cui l'amministratore dell'infrastruttura PKI desidera controllare i tipi di dispositivi che possono essere utilizzati per ottenere i certificati nell'ambiente).  

### <a name="tpm-key-attestation"></a>Attestazione chiave TPM  
Attestazione chiave TPM è la capacità dell'entità che richiede un certificato per la verifica crittografica di una CA che la chiave RSA nella richiesta di certificato è protetta da "a" o "il" TPM considerato attendibile dalla CA. Il modello di attendibilità TPM è illustrato più avanti nella sezione [Panoramica della distribuzione](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_DeploymentOverview) più avanti in questo argomento.  
  
### <a name="why-is-tpm-key-attestation-important"></a>Perché è importante attestazione chiave TPM?  
Un certificato utente con una chiave con attestazione TPM offre una garanzia di sicurezza più elevata, sottoposta a backup da non esportabilità, anti-martellamento e isolamento delle chiavi fornite dal TPM.  
  
Con l'attestazione chiave TPM, è ora possibile usare un nuovo paradigma di gestione: Un amministratore può definire il set di dispositivi che gli utenti possono usare per accedere alle risorse aziendali (ad esempio, VPN o punto di accesso wireless) e avere garanzie **sicure** che nessun altro dispositivo possa essere usato per accedervi. Questo nuovo paradigma di controllo di accesso è **forte** perché è associato a un'identità utente *associata a hardware* , che è più potente rispetto a una credenziale basata su software.
  
### <a name="how-does-tpm-key-attestation-work"></a>Come funziona l'attestazione chiave TPM?  
In generale, l'attestazione chiave TPM si basa sui pilastri seguenti:  
  
1.  Ogni TPM viene fornito con una chiave asimmetrica univoca, denominata *chiave* di verifica dell'autenticità, bruciata dal produttore. Si fa riferimento alla parte pubblica della chiave come *EKPub* e alla chiave privata associata come *EKPriv*. Alcuni chip TPM dispone anche di un certificato di verifica dell'AUTENTICITÀ rilasciato dal produttore per il EKPub. Questo certificato viene fatto riferimento a *EKCert*.  
  
2.  Una CA stabilisce una relazione di trust nel TPM tramite EKPub o EKCert.  
  
3.  Un utente tenta l'autorità di certificazione che la chiave RSA per cui viene richiesto il certificato di crittografia è correlata al EKPub e che l'utente proprietario di EKpriv.  
  
4.  L'autorità di certificazione emette un certificato con un criterio di rilascio speciale OID per indicare che la chiave viene attestata ora possono essere protette da un TPM.  
  
## <a name="BKMK_DeploymentOverview"></a>Panoramica della distribuzione  
In questa distribuzione, si presuppone che sia configurata una CA dell'organizzazione di Windows Server 2012 R2. Inoltre, i client (Windows 8.1) sono configurati per la registrazione a tale CA globale (Enterprise) usando modelli di certificato. 

Esistono tre passaggi per la distribuzione di attestazione chiave TPM:  
  
1.  **Pianificare il modello di trust TPM:** Il primo passaggio consiste nel decidere quale modello di attendibilità TPM utilizzare. Sono disponibili 3 modi per eseguire questa operazione:  
  
    -   **Attendibilità in base alle credenziali dell'utente:** La CA globale (Enterprise) considera attendibile il EKPub fornito dall'utente come parte della richiesta di certificato e non viene eseguita alcuna convalida oltre alle credenziali di dominio dell'utente.  
  
    -   **Trust basato su EKCert:** La CA globale (Enterprise) convalida la catena EKCert fornita come parte della richiesta di certificato rispetto a un elenco gestito dall'amministratore di *catene di certificati EK accettabili*. Le catene accettabili sono definite per produttore e sono espresse tramite due archivi certificati personalizzati nella CA emittente (un archivio per il livello intermedio e uno per i certificati CA radice). Questa modalità di attendibilità significa che **tutti** TPM di un determinato produttore sono attendibili. Si noti che in questa modalità, TPM in uso nell'ambiente deve contenere EKCerts.
  
    -   **Trust basato su EKPub:** La CA globale (Enterprise) verifica che il EKPub fornito come parte della richiesta di certificato venga visualizzato in un elenco gestito da amministratore di EKPubs consentiti. Questo elenco viene espresso come una directory di file in cui il nome di ogni file in questa directory è l'hash SHA-2 EKPub consentiti. Questa opzione offre il massimo livello di garanzia, ma richiede un maggiore impegno amministrativo, perché ogni dispositivo viene identificato singolarmente. In questo modello di trust solo i dispositivi per i quali è stato aggiunto il EKPub del TPM all'elenco di EKPubs consentito possono registrarsi per un certificato con attestazione TPM.  
  
    A seconda del metodo usato, la CA applicherà un OID del criterio di rilascio diverso al certificato emesso. Per ulteriori informazioni sui criteri di rilascio OID, vedere la tabella OID dei criteri di rilascio nel [configurare un modello di certificato](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_ConfigCertTemplate) in questo argomento.  
  
    Si noti che è possibile scegliere una combinazione di modelli di protezione TPM. In questo caso, l'autorità di certificazione accetterà uno dei metodi di attestazione e i criteri di rilascio OID rifletteranno tutti i metodi di attestazione che hanno esito positivo.  
  
2.  **Configurare il modello di certificato:** La configurazione del modello di certificato è descritta nella sezione [Dettagli distribuzione](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_DeploymentDetails) in questo argomento. In questo articolo riguardano la modalità di assegnazione di questo modello di certificato per la CA dell'organizzazione o procedura per la registrazione non ha accesso a un gruppo di utenti. Per ulteriori informazioni, vedere [Elenco di controllo: Configurare CA per rilasciare e gestire i certificati @ no__t-0.  
  
3.  **Configurare la CA per il modello di attendibilità TPM**  
  
    1.  **Attendibilità in base alle credenziali dell'utente:** Non è necessaria alcuna configurazione specifica.  
  
    2.  **Trust basato su EKCert:** L'amministratore deve ottenere i certificati della catena EKCert dai produttori del TPM e importarli in due nuovi archivi certificati, creati dall'amministratore, sulla CA che eseguono l'attestazione chiave TPM. Per ulteriori informazioni, vedere il [configurazione CA](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) in questo argomento.  
  
    3.  **Trust basato su EKPub:** L'amministratore deve ottenere il EKPub per ogni dispositivo che necessita di certificati con attestazione TPM e aggiungerli all'elenco di EKPubs consentiti. Per ulteriori informazioni, vedere il [configurazione CA](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) in questo argomento.  
  
    > [!NOTE]  
    > -   Questa funzionalità richiede Windows 8.1/Windows Server 2012 R2.  
    > -   Attestazione chiave TPM per provider di archiviazione di terze parti smart card non è supportata. È necessario utilizzare Microsoft piattaforma Crypto Provider KSP.  
    > -   Attestazione chiave TPM funziona solo per le chiavi RSA.  
    > -   Attestazione chiave TPM non è supportata per una CA autonoma.  
    > -   Attestazione chiave TPM non supporta [l'elaborazione di certificati non permanenti](https://technet.microsoft.com/library/ff934598).  
  
## <a name="BKMK_DeploymentDetails"></a>Dettagli della distribuzione  
  
### <a name="BKMK_ConfigCertTemplate"></a>Configurare un modello di certificato  
Per configurare il modello di certificato per l'attestazione chiave TPM, eseguire i passaggi di configurazione seguenti:  
  
1.  **Compatibilità** scheda  
  
    Nel **le impostazioni di compatibilità** sezione:  
  
    -   Verificare **Windows Server 2012 R2** è selezionata per il **autorità di certificazione**.  
  
    -   Verificare **Windows 8.1 / Windows Server 2012 R2** è selezionata per il **destinatario certificato**.  
  
    ![Attestazione chiave TPM](media/TPM-Key-Attestation/GTR_ADDS_CompatibilityTab.gif)  
  
2.  **Crittografia** scheda  
  
    Verificare **Provider di archiviazione chiavi** è selezionata per il **categoria Provider** e **RSA** è selezionata per il **nome dell'algoritmo**. Verificare che le **richieste debbano usare uno dei seguenti provider** è selezionata e l'opzione **provider di crittografia piattaforma Microsoft** è selezionata in **provider**.  
  
    ![Attestazione chiave TPM](media/TPM-Key-Attestation/GTR_ADDS_CryptoTab.gif)  
  
3.  **Attestazione chiave** scheda  
  
    Si tratta di una nuova scheda per Windows Server 2012 R2:  
  
    ![Attestazione chiave TPM](media/TPM-Key-Attestation/GTR_ADDS_ConfigCertTemplate.gif)  
  
    Scegliere una modalità di attestazione tra le tre opzioni possibili.  
  
    ![Attestazione chiave TPM](media/TPM-Key-Attestation/GTR_ADDS_KeyModes.gif)  
  
    -   **Nessuno** Indica che non è necessario usare l'attestazione chiave  
  
    -   **Obbligatorio, se il client è in grado di:** Consente agli utenti di un dispositivo che non supporta l'attestazione della chiave TPM di continuare la registrazione per tale certificato. Gli utenti possono eseguire un'attestazione verranno distinto con un criterio di rilascio speciale OID. Alcuni dispositivi potrebbero non essere in grado di eseguire l'attestazione a causa di un TPM precedente che non supporta l'attestazione chiave oppure il dispositivo non dispone di un TPM.
  
    -   **Obbligatorio:** Il client *deve* eseguire l'attestazione chiave TPM, in caso contrario la richiesta di certificato avrà esito negativo.  
  
    Scegliere il modello di protezione TPM. Sono disponibili tre opzioni:  
  
    ![Attestazione chiave TPM](media/TPM-Key-Attestation/GTR_ADDS_KeyTypeToEnforce.gif)  
  
    -   **Credenziali utente:** Consentire a un utente che esegue l'autenticazione di garantire un TPM valido specificando le proprie credenziali di dominio.  
  
    -   **Certificato di verifica dell'autenticità:** Il EKCert del dispositivo deve essere convalidato tramite certificati CA intermedi TPM gestiti dall'amministratore a un certificato CA radice gestito dall'amministratore. Se si sceglie questa opzione, è necessario impostare EKCA ed EKRoot archivi nella CA di emissione di certificati come descritto nel  [configurazione CA](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) in questo argomento.  
  
    -   **Chiave di verifica dell'autenticità:** Il EKPub del dispositivo deve essere visualizzato nell'elenco PKI gestito dall'amministratore. Questa opzione offre il massimo livello di garanzia, ma richiede uno sforzo amministrativo. Se si sceglie questa opzione, è necessario impostare un elenco di EKPub nella CA emittente come descritto nel [configurazione CA](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md#BKMK_CAConfig) in questo argomento.  
  
    Infine, decidere quali criteri di rilascio per visualizzare il certificato emesso. Per impostazione predefinita, ogni tipo di applicazione ha un identificatore di oggetto (OID) associato che verrà inserito nel certificato se passa tale tipo di imposizione, come descritto nella tabella seguente. Si noti che è possibile scegliere una combinazione di metodi di imposizione. In questo caso, l'autorità di certificazione accetterà uno dei metodi di attestazione e l'OID del criterio di rilascio rifletterà tutti i metodi di attestazione che hanno avuto esito positivo.  
  
    **Criteri di rilascio OID**  
  
    |OID|Tipo di attestazione chiave|Descrizione|Livello di garanzia|  
    |-------|------------------------|---------------|-------------------|  
    |1.3.6.1.4.1.311.21.30|VERIFICA DELL'AUTENTICITÀ|"EK verificato":   Per l'elenco gestito dall'amministratore di EK|Alto|  
    |1.3.6.1.4.1.311.21.31|Certificato di verifica dell'autenticità|"Certificato EK verificato": Quando viene convalidata la catena di certificati EK|Medio|  
    |1.3.6.1.4.1.311.21.32|Credenziali dell'utente|"EK Trusted on Use": Per la EK attestata dall'utente|Bassa|  
  
    L'OID verrà inserito nel certificato emesso se **includere criteri di rilascio** è selezionata (configurazione predefinita).  
  
    ![Attestazione chiave TPM](media/TPM-Key-Attestation/GTR_ADDS_IssuancePolicies.gif)  
  
    > [!TIP]  
    > Un potenziale utilizzo dell'OID presente nel certificato consiste nel limitare l'accesso alla rete VPN o wireless a determinati dispositivi. Ad esempio, i criteri di accesso potrebbero consentire la connessione (o l'accesso a una VLAN diversa) se OID 1.3.6.1.4.1.311.21.30 è presente nel certificato. Ciò consente di limitare l'accesso ai dispositivi cui EK TPM è presente nell'elenco EKPUB.  
  
### <a name="BKMK_CAConfig"></a>Configurazione CA  
  
1.  **Configurare gli archivi certificati EKCA e EKROOT in una CA emittente**  
  
    Se si sceglie **certificato di verifica dell'autenticità** per le impostazioni del modello, effettuare i passaggi di configurazione seguenti:  
  
    1.  Utilizzare Windows PowerShell per creare due nuovi archivi certificati nel server di autorità di (certificazione CA) di certificazione che eseguirà l'attestazione chiave TPM.  
  
    2.  Ottenere i certificati dell'autorità di certificazione intermedia e radice dai produttori che si desidera consentire nell'ambiente aziendale. Questi certificati devono essere importati negli archivi certificati creati in precedenza (EKCA e EKROOT) in base alle esigenze.  
  
    Il seguente script Windows PowerShell esegue entrambe queste operazioni. Nell'esempio seguente, il produttore del TPM Fabrikam ha fornito un certificato radice *FabrikamRoot.cer* e un certificato della CA emittente *Fabrikamca.cer*.  
  
    ```powershell  
    PS C:>\cd cert:  
    PS Cert:\>cd .\\LocalMachine  
    PS Cert:\LocalMachine> new-item EKROOT  
    PS Cert:\ LocalMachine> new-item EKCA  
    PS Cert:\EKCA\copy FabrikamCa.cer .\EKCA  
    PS Cert:\EKROOT\copy FabrikamRoot.cer .\EKROOT  
    ```  
  
2.  **Configurare l'elenco EKPUB se si usa il tipo di attestazione EK**  
  
    Se si sceglie **chiave** di verifica dell'autenticità nelle impostazioni del modello, i passaggi di configurazione successivi sono la creazione e la configurazione di una cartella nella CA emittente, contenente i file da 0 byte, ognuno dei quali denominato per l'hash SHA-2 di un valore EK consentito. Questa cartella funge da "elenco di accesso consentito" dei dispositivi autorizzati a ottenere certificati con attestazioni chiave TPM. Poiché è necessario aggiungere manualmente il EKPUB per ogni dispositivo che richiede un certificato attested, fornisce dell'azienda con una garanzia dei dispositivi autorizzati per ottenere i certificati di attestata chiave TPM. La configurazione di un'autorità di certificazione per questa modalità richiede due passaggi:  
  
    1.  **Creare la voce del registro di sistema EndorsementKeyListDirectories:** Utilizzare lo strumento da riga di comando certutil per configurare i percorsi della cartella in cui sono definiti EKpubs attendibili, come descritto nella tabella seguente.  
  
        |Operazione|Sintassi del comando|  
        |-------------|------------------|  
        |Aggiungere percorsi di cartelle|certutil.exe - setreg CA\EndorsementKeyListDirectories + "<folder>"|  
        |Rimuovere i percorsi delle cartelle|certutil.exe - setreg CA\EndorsementKeyListDirectories-"<folder>"|  
  
        Il EndorsementKeyListDirectories nel comando certutil è un'impostazione del registro di sistema, come descritto nella tabella seguente.  
  
        |Nome del valore|Type|Data|  
        |--------------|--------|--------|  
        |EndorsementKeyListDirectories|REG_MULTI_SZ|< percorso LOCALE o UNC EKPUB consentire elenchi ><br /><br />Esempio:<br /><br />*\\ \ blueCA. contoso. com\ekpub*<br /><br />*\\ \ bluecluster1. contoso. com\ekpub*<br /><br />D:\ekpub|  
  
        HKLM\SYSTEM\CurrentControlSet\Services\CertSvc\Configuration @ no__t-0 @ no__t-1  
  
        *EndorsementKeyListDirectories* conterrà un elenco di percorsi UNC o file system locali, ognuno dei quali fa riferimento a una cartella a cui l'autorità di certificazione ha accesso in lettura. Ogni cartella può contenere zero o più voci di elenco Consenti, in cui ogni voce è un file con un nome che corrisponde all'hash SHA-2 di un EKpub attendibile, senza estensione di file. 
        La creazione o la modifica della configurazione della chiave del registro di sistema richiede il riavvio della CA, esattamente come le impostazioni di configurazione del registro di sistema della CA esistente Tuttavia, le modifiche alle impostazioni della configurazione avranno effetto immediato e non richiederà la CA è necessario riavviare.  
  
        > [!IMPORTANT]  
        > Proteggere le cartelle nell'elenco da eventuali manomissioni e accessi non autorizzati tramite la configurazione delle autorizzazioni in modo che solo gli amministratori autorizzati lettura e l'accesso in scrittura. L'account computer della CA richiede solo l'accesso in lettura.  
  
    2.  **Popolare l'elenco EKPUB:** Usare il cmdlet di Windows PowerShell seguente per ottenere l'hash della chiave pubblica del TPM EK usando Windows PowerShell in ogni dispositivo, quindi inviare questo hash della chiave pubblica all'autorità di certificazione e archiviarlo nella cartella EKPubList.  
  
        ```powershell  
        PS C:>\$a=Get-TpmEndorsementKeyInfo -hashalgorithm sha256  
        PS C:>$b=new-item $a.PublicKeyHash -ItemType file  
        ```  
  
## <a name="troubleshooting"></a>Risoluzione dei problemi  
  
### <a name="key-attestation-fields-are-unavailable-on-a-certificate-template"></a>Attestazione chiave campi non sono disponibili in un modello di certificato  
I campi chiave attestazione non sono disponibili se le impostazioni del modello non soddisfano i requisiti per l'attestazione. Cause comuni sono:  
  
1.  Le impostazioni di compatibilità non sono configurate correttamente. Assicurarsi che siano configurate come indicato di seguito:  
  
    1.  **Autorità di certificazione**: **Windows Server 2012 R2**  
  
    2.  **Destinatario certificato**: **Windows 8.1/Windows Server 2012 R2**  
  
2.  Le impostazioni di crittografia non sono configurate correttamente. Assicurarsi che siano configurate come indicato di seguito:  
  
    1.  **Categoria provider**: **Provider di archiviazione chiavi**  
  
    2.  **Nome algoritmo**: **RSA**  
  
    3.  **Provider**: **Provider di crittografia della piattaforma Microsoft**  
  
3.  Le impostazioni di gestione delle richieste non sono configurate correttamente. Assicurarsi che siano configurate come indicato di seguito:  
  
    1.  Il **Rendi la chiave privata esportabile** opzione non deve essere selezionato.  
  
    2.  Il **Archivia chiave privata di crittografia del soggetto** opzione non deve essere selezionato.  
  
### <a name="verification-of-tpm-device-for-attestation"></a>Verifica del dispositivo TPM per l'attestazione  
Utilizzare il cmdlet Windows PowerShell, **Conferma CAEndorsementKeyInfo**, per verificare che un determinato dispositivo TPM sia attendibile per l'attestazione dalle autorità di certificazione. Sono disponibili due opzioni: uno per la verifica di EKCert e l'altro per la verifica di un EKPub. Il cmdlet sia eseguito localmente su una CA o in remoto CAs usando la comunicazione remota di Windows PowerShell.  
  
1.  Per la verifica dell'attendibilità in un EKPub, eseguire i due passaggi seguenti:  
  
    1.  **Estrarre il EKPub dal computer client:** EKPub può essere Estratto da un computer client tramite **Get-TpmEndorsementKeyInfo**. Da un prompt dei comandi con privilegi elevati, eseguire le operazioni seguenti:  
  
        ```  
        PS C:>\$a=Get-TpmEndorsementKeyInfo -hashalgorithm sha256  
        ```  
  
    2.  **Verificare l'attendibilità in un EKCert in un computer della CA:** Copiare la stringa estratta (hash SHA-2 del EKPub) nel server (ad esempio tramite posta elettronica) e passarla al cmdlet Confirm-CAEndorsementKeyInfo. Si noti che questo parametro deve essere di 64 caratteri.  
  
        ```  
        Confirm-CAEndorsementKeyInfo [-PublicKeyHash] <string>  
        ```  
  
2.  Per la verifica dell'attendibilità in un EKCert, eseguire i due passaggi seguenti:  
  
    1.  **Estrarre il EKCert dal computer client:** EKCert può essere Estratto da un computer client tramite **Get-TpmEndorsementKeyInfo**. Da un prompt dei comandi con privilegi elevati, eseguire le operazioni seguenti:  
  
        ```  
        PS C:>\$a=Get-TpmEndorsementKeyInfo
        PS C:>\$a.manufacturerCertificates|Export-Certificate -filepath c:\myEkcert.cer
        ```  
  
    2.  **Verificare l'attendibilità in un EKCert in un computer della CA:** Copiare il EKCert Estratto (EkCert. cer) nell'autorità di certificazione (ad esempio tramite posta elettronica o Xcopy). Ad esempio, se si copia il file del certificato nella cartella "c:\diagnose" nel server CA, eseguire il comando seguente per completare la verifica:  
  
        ```  
        PS C:>new-object System.Security.Cryptography.X509Certificates.X509Certificate2 "c:\diagnose\myEKcert.cer" | Confirm-CAEndorsementKeyInfo  
        ```  
  
## <a name="see-also"></a>Vedere anche  
[Panoramica della tecnologia Trusted Platform Module](https://technet.microsoft.com/library/jj131725.aspx)  
Risorsa [External: Trusted Platform Module @ no__t-0  
