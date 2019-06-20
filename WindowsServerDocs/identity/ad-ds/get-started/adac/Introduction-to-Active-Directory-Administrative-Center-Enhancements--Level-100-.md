---
ms.assetid: 074e63e9-976c-49da-8cba-9ae0b3325e34
title: Introduction to Active Directory Administrative Center Enhancements (Level 100)
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d3b5f3eee338128fb424c28e7280bb7f543c9f58
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443006"
---
# <a name="introduction-to-active-directory-administrative-center-enhancements-level-100"></a>Introduction to Active Directory Administrative Center Enhancements (Level 100)

>Si applica a: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Il centro di amministrazione di Active Directory in Windows Server include le funzionalità di gestione per le operazioni seguenti:

- [Il Cestino di Active Directory](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#ad_recycle_bin_mgmt)
- [Criteri granulari per le Password](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#fine_grained_pswd_policy_mgmt)
- [Visualizzatore della cronologia di PowerShell di Windows](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#windows_powershell_history_viewer)

## <a name="ad_recycle_bin_mgmt"></a>Il Cestino di Active Directory

L'eliminazione accidentale di oggetti Active Directory è un problema comune per gli utenti di Servizi di dominio Active Directory e Active Directory Lightweight Directory Services. Nelle versioni precedenti di Windows Server, prima di Windows Server 2008 R2, è possibile ripristinare oggetti eliminati in modo accidentale in Active Directory, tuttavia le soluzioni presentano svantaggi.

In Windows Server 2008 è possibile utilizzare la funzionalità Windows Server Backup e il comando per il ripristino autorevole **ntdsutil** per contrassegnare gli oggetti come autorevoli e garantire la replica dei dati ripristinati nell'intero dominio. La soluzione relativa al ripristino autorevole deve tuttavia essere eseguita nella modalità ripristino servizi directory e ciò costituisce uno svantaggio. In tale modalità, infatti, il controller di dominio da ripristinare deve rimanere offline e non è pertanto in grado di soddisfare le richieste client.

In Windows Server 2003 Active Directory e Servizi di dominio Active Directory di Windows Server 2008 è possibile ripristinare oggetti Active Directory tramite il recupero degli oggetti contrassegnati per la rimozione definitiva. Non è tuttavia possibile recuperare gli attributi con valori di collegamento degli oggetti recuperati, ad esempio l'appartenenza a gruppi degli account utente, che sono stati rimossi fisicamente e gli attributi con valori non di collegamento cancellati. Gli amministratori non possono pertanto avvalersi del recupero degli oggetti contrassegnati per la rimozione definitiva come soluzione ideale in caso di eliminazione accidentale degli oggetti. Per altre informazioni sul recupero degli oggetti contrassegnati per la rimozione definitiva, vedere [Recupero degli oggetti contrassegnati per la rimozione definitiva di Active Directory](https://go.microsoft.com/fwlink/?LinkID=125452).

A partire da Windows Server 2008 R2, il Cestino per Active Directory si basa sull'infrastruttura esistente di recupero degli oggetti contrassegnati per la rimozione definitiva e amplia le possibilità di salvaguardare e recuperare oggetti Active Directory eliminati in modo accidentale.

Quando si attiva il Cestino per Active Directory, vengono mantenuti tutti gli attributi con valori di collegamento e non di collegamento degli oggetti Active Directory eliminati e gli oggetti vengono interamente ripristinati nello stesso stato logico coerente in cui si trovavano immediatamente prima dell'eliminazione. Gli account utente ripristinati, ad esempio, ottengono di nuovo automaticamente tutte le appartenenze ai gruppi e i diritti di accesso corrispondenti di cui disponevano all'interno del dominio e tra domini immediatamente prima dell'eliminazione. Il Cestino per Active Directory supporta gli ambienti Servizi di dominio Active Directory e Active Directory Lightweight Directory Services. Per una descrizione dettagliata del Cestino Active Directory, vedere [What ' s New in Active Directory Domain Services: Cestino per Active Directory](https://technet.microsoft.com/library/dd391916(WS.10).aspx).

**Quali sono le novità?** In Windows Server 2012 e versioni successive, la funzionalità al Cestino per Active Directory è stata migliorata con una nuova interfaccia utente grafica per gli utenti di gestire e ripristinare oggetti eliminati. Gli utenti possono infatti visualizzare un elenco di oggetti eliminati e ripristinarli nei percorsi originali o a scelta.

Se si prevede di abilitare Cestino Active Directory in Windows Server, considerare quanto segue:

- Per impostazione predefinita, il Cestino per Active Directory è disabilitato. Per abilitarla, è prima necessario aumentare il livello di funzionalità foresta dell'ambiente Active Directory Domain Services o AD LDS a Windows Server 2008 R2 o versione successiva. Ciò a sua volta richiede che tutti i controller di dominio nella foresta o tutti i server che ospitano istanze dei set di configurazione di AD LDS in esecuzione Windows Server 2008 R2 o versione successiva.
- Il processo di abilitazione del Cestino per Active Directory è irreversibile. Se si abilita il Cestino per Active Directory nell'ambiente in uso, non sarà più possibile disabilitarlo.
- Per gestire la funzionalità Cestino tramite un'interfaccia utente, è necessario installare la versione di centro di amministrazione di Active Directory in Windows Server 2012.

    > [!NOTE]
    > È possibile usare **Server Manager** installare amministrazione remota del Server strumenti () per usare la versione corretta di centro di amministrazione di Active Directory per gestire il Cestino tramite un'interfaccia utente.
    >
    > Per informazioni sull'installazione di amministrazione remota del server, vedere l'articolo [strumenti di amministrazione remota del Server](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools).

### <a name="active-directory-recycle-bin-step-by-step"></a>Cestino per Active Directory - Procedura dettagliata

Nei passaggi seguenti, si utilizzerà centro di eseguire le attività seguenti al Cestino per Active Directory in Windows Server 2012:

- [Passaggio 1: Aumentare il livello funzionale di foresta](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_raise_ffl)
- [Passaggio 2: Abilitare il Cestino](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_enable_recycle_bin)
- [Passaggio 3: Creare utenti di test, gruppo e unità organizzativa](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_test_env)
- [Passaggio 4: Ripristinare oggetti eliminati](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_restore_del_obj)

> [!NOTE]
> Per eseguire i passaggi seguenti, è necessario essere membri del gruppo Enterprise Admins o disporre di autorizzazioni equivalenti.

### <a name="bkmk_raise_ffl"></a>Passaggio 1: Aumentare il livello di funzionalità della foresta

In questo passaggio si aumenterà il livello di funzionalità della foresta. È prima necessario aumentare il livello funzionale della foresta di destinazione sia Windows Server 2008 R2 come minimo, prima di abilitare al Cestino per Active Directory.

#### <a name="to-raise-the-functional-level-on-the-target-forest"></a>Per aumentare il livello di funzionalità della foresta di destinazione

1. Fare clic con il pulsante destro sull'icona di Windows PowerShell, fare clic su **Esegui come amministratore** e digitare **dsac.exe** per aprire Centro.

2. Fare clic su **Gestisci**e su **Aggiungi nodi di spostamento** . Selezionare il dominio di destinazione appropriato nella finestra di dialogo **Aggiungi nodi di spostamento** e quindi fare clic su **OK**.

3. Fare clic sul dominio di destinazione nel riquadro di spostamento a sinistra e nel riquadro **Attività** fare clic su **Aumenta livello di funzionalità foresta**. Selezionare un livello di foresta funzionale che sia almeno Windows Server 2008 R2 o versione successiva e quindi fare clic su **OK**.

![Introduzione all'interfaccia di amministrazione di Active Directory](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>comandi equivalenti di Windows PowerShell</em>***

Il cmdlet o i cmdlet di Windows PowerShell seguenti eseguono la stessa funzione della procedura precedente. Immettere ogni cmdlet in una singola riga, anche se qui può sembrare che siano divisi su più righe a causa di vincoli di formattazione.

```powershell
Set-ADForestMode -Identity contoso.com -ForestMode Windows2008R2Forest -Confirm:$false
```

Per il **-identità** argomento, specificare il nome di dominio DNS completo.

### <a name="bkmk_enable_recycle_bin"></a>Passaggio 2: Abilitare il Cestino

In questo passaggio si abiliterà il Cestino per ripristinare oggetti eliminati in Servizi di directory Active Directory.

#### <a name="to-enable-active-directory-recycle-bin-in-adac-on-the-target-domain"></a>Per abilitare il Cestino per Active Directory in Centro di amministrazione di Active Directory nel dominio di destinazione

1. Fare clic con il pulsante destro sull'icona di Windows PowerShell, fare clic su **Esegui come amministratore** e digitare **dsac.exe** per aprire Centro.

2. Fare clic su **Gestisci**e su **Aggiungi nodi di spostamento** . Selezionare il dominio di destinazione appropriato nella finestra di dialogo **Aggiungi nodi di spostamento** e quindi fare clic su **OK**.

3. Nel riquadro **Attività** fare clic su **Abilita Cestino ...** nel riquadro **Attività**, fare clic su **OK** nel riquadro del messaggio di avviso e quindi **OK** nel messaggio di aggiornamento di Centro di amministrazione di Active Directory.

4. Premere F5 per aggiornare Centro di amministrazione di Active Directory.

![Introduzione all'interfaccia di amministrazione di Active Directory](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>comandi equivalenti di Windows PowerShell</em>***

Il cmdlet o i cmdlet di Windows PowerShell seguenti eseguono la stessa funzione della procedura precedente. Immettere ogni cmdlet in una singola riga, anche se qui può sembrare che siano divisi su più righe a causa di vincoli di formattazione.

```powershell
Enable-ADOptionalFeature -Identity 'CN=Recycle Bin Feature,CN=Optional Features,CN=Directory Service,CN=Windows NT,CN=Services,CN=Configuration,DC=contoso,DC=com' -Scope ForestOrConfigurationSet -Target 'contoso.com'
```

### <a name="bkmk_create_test_env"></a>Passaggio 3: Creare utenti, gruppo e unità organizzativa di prova

Nelle procedure seguenti si creeranno due utenti di prova. Si creerà quindi un gruppo di prova al quale aggiungere gli utenti di prova. Si creerà infine un'unità organizzativa.

#### <a name="to-create-test-users"></a>Per creare gli utenti di prova

1. Fare clic con il pulsante destro sull'icona di Windows PowerShell, fare clic su **Esegui come amministratore** e digitare **dsac.exe** per aprire Centro.

2. Fare clic su **Gestisci**e su **Aggiungi nodi di spostamento** . Selezionare il dominio di destinazione appropriato nella finestra di dialogo **Aggiungi nodi di spostamento** e quindi fare clic su **OK**.

3. Nel riquadro **Attività** fare clic su **Nuovo** e quindi su **Utente**.

    ![Introduzione all'interfaccia di amministrazione di Active Directory](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/ADDS_ADACNewUser.gif)

4. Immettere le informazioni seguenti in **Account** e fare clic su OK:

   - Nome completo: test1
   - Accesso utente SamAccountName: test1
   - Password: p@ssword1
   - Conferma password: p@ssword1

5. Ripetere i passaggi precedenti per creare un secondo utente test2.

#### <a name="to-create-a-test-group-and-add-users-to-the-group"></a>Per creare un gruppo di prova al quale aggiungere utenti

1. Fare clic con il pulsante destro sull'icona di Windows PowerShell, fare clic su **Esegui come amministratore** e digitare **dsac.exe** per aprire Centro.
2. Fare clic su **Gestisci**e su **Aggiungi nodi di spostamento** . Selezionare il dominio di destinazione appropriato nella finestra di dialogo **Aggiungi nodi di spostamento** e quindi fare clic su **OK**.
3. Nel riquadro **Attività** fare clic su **Nuovo** e quindi su **Gruppo**.
4. Immettere le informazioni seguenti in **Gruppo** e fare clic su **OK**:

    -   **Nome gruppo: group1**

5. Fare clic su **group1**e quindi nel riquadro **Attività** fare clic su **Proprietà**.
6. Fare clic su **Membri**e su **Aggiungi**, digitare **test1;test2**e quindi fare clic su **OK**.

![Introduzione all'interfaccia di amministrazione di Active Directory](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>comandi equivalenti di Windows PowerShell</em>***

Il cmdlet o i cmdlet di Windows PowerShell seguenti eseguono la stessa funzione della procedura precedente. Immettere ogni cmdlet in una singola riga, anche se qui può sembrare che siano divisi su più righe a causa di vincoli di formattazione.

```powershell
Add-ADGroupMember -Identity group1 -Member test1
```

#### <a name="to-create-an-organizational-unit"></a>Per creare un'unità organizzativa

1. Fare clic con il pulsante destro sull'icona di Windows PowerShell, fare clic su **Esegui come amministratore** e digitare **dsac.exe** per aprire Centro.
2. Fare clic su **Manage**, fare clic su **Aggiungi nodi di spostamento** e selezionare il dominio di destinazione appropriato nella **Aggiungi nodi di spostamento** nella finestra di dialogo e quindi fare clic su * * OK
3. Nel riquadro **Attività** fare clic su **Nuovo** e quindi su **Unità organizzativa**.
4. Immettere le informazioni seguenti in **Unità organizzativa** e fare clic su **OK**:

   - **NameOU1**

![Introduzione all'interfaccia di amministrazione di Active Directory](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>comandi equivalenti di Windows PowerShell</em>***

Il cmdlet o i cmdlet di Windows PowerShell seguenti eseguono la stessa funzione della procedura precedente. Immettere ogni cmdlet in una singola riga, anche se qui può sembrare che siano divisi su più righe a causa di vincoli di formattazione.

```powershell
1..2 | ForEach-Object {New-ADUser -SamAccountName test$_ -Name "test$_" -Path "DC=fabrikam,DC=com" -AccountPassword (ConvertTo-SecureString -AsPlainText "p@ssword1" -Force) -Enabled $true}
New-ADGroup -Name "group1" -SamAccountName group1 -GroupCategory Security -GroupScope Global -DisplayName "group1"
New-ADOrganizationalUnit -Name OU1 -Path "DC=fabrikam,DC=com"
```

### <a name="bkmk_restore_del_obj"></a>Passaggio 4: Ripristinare gli oggetti eliminati

Nelle procedure seguenti gli oggetti eliminati presenti nel contenitore **Oggetti eliminati** verranno ripristinati nel percorso originale e in un percorso diverso.

#### <a name="to-restore-deleted-objects-to-their-original-location"></a>Per ripristinare oggetti eliminati nel percorso originale

1. Fare clic con il pulsante destro sull'icona di Windows PowerShell, fare clic su **Esegui come amministratore** e digitare **dsac.exe** per aprire Centro.

2. Fare clic su **Gestisci**e su **Aggiungi nodi di spostamento** . Selezionare il dominio di destinazione appropriato nella finestra di dialogo **Aggiungi nodi di spostamento** e quindi fare clic su **OK**.

3. Selezionare gli utenti **test1** e **test2**, fare clic su **Elimina** nel riquadro **Attività** e quindi fare clic su **Sì** per confermare l'eliminazione.

    ![Introduzione all'interfaccia di amministrazione di Active Directory](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>comandi equivalenti di Windows PowerShell</em>***

    Il cmdlet o i cmdlet di Windows PowerShell seguenti eseguono la stessa funzione della procedura precedente. Immettere ogni cmdlet in una singola riga, anche se qui può sembrare che siano divisi su più righe a causa di vincoli di formattazione.

    ```powershell
    Get-ADUser -Filter 'Name -Like "*test*"'|Remove-ADUser -Confirm:$false
    ```

4. Passare al contenitore **Oggetti eliminati** , selezionare **test2** e **test1** e quindi fare clic su **Ripristina** nel riquadro **Attività** .

5. Per confermare che gli oggetti sono stati ripristinati nel percorso originale, passare al dominio di destinazione e verificare che gli account utente sono inclusi nell'elenco.

    > [!NOTE]
    > Se si passa a **Proprietà** degli account utente **test1** e **test2** e quindi si fa clic su **Membro di**, si noterà che è stata ripristinata anche l'appartenenza ai gruppi.

Il cmdlet o i cmdlet di Windows PowerShell seguenti eseguono la stessa funzione della procedura precedente. Immettere ogni cmdlet in una singola riga, anche se qui può sembrare che siano divisi su più righe a causa di vincoli di formattazione.

![Introduzione all'interfaccia di amministrazione di Active Directory](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>comandi equivalenti di Windows PowerShell</em>***

```powershell
Get-ADObject -Filter 'Name -Like "*test*"' -IncludeDeletedObjects | Restore-ADObject
```

#### <a name="to-restore-deleted-objects-to-a-different-location"></a>Per ripristinare oggetti eliminati in un percorso diverso

1. Fare clic con il pulsante destro sull'icona di Windows PowerShell, fare clic su **Esegui come amministratore** e digitare **dsac.exe** per aprire Centro.

2. Fare clic su **Gestisci**e su **Aggiungi nodi di spostamento** . Selezionare il dominio di destinazione appropriato nella finestra di dialogo **Aggiungi nodi di spostamento** e quindi fare clic su **OK**.

3. Selezionare gli utenti **test1** e **test2**, fare clic su **Elimina** nel riquadro **Attività** e quindi fare clic su **Sì** per confermare l'eliminazione.

4. Passare al contenitore **Oggetti eliminati** , selezionare **test2** e **test1** e quindi fare clic su **Ripristina in** nel riquadro **Attività** .

5. Selezionare **OU1** e quindi fare clic su **OK**.

6. Per confermare che gli oggetti sono stati ripristinati in **OU1**, passare al dominio di destinazione, fare doppio clic su **OU1** e verificare che gli account utente sono inclusi nell'elenco.

![Introduzione all'interfaccia di amministrazione di Active Directory](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>comandi equivalenti di Windows PowerShell</em>***

Il cmdlet o i cmdlet di Windows PowerShell seguenti eseguono la stessa funzione della procedura precedente. Immettere ogni cmdlet in una singola riga, anche se qui può sembrare che siano divisi su più righe a causa di vincoli di formattazione.

```powershell
Get-ADObject -Filter 'Name -Like "*test*"' -IncludeDeletedObjects | Restore-ADObject -TargetPath "OU=OU1,DC=contoso,DC=com"
```

## <a name="fine_grained_pswd_policy_mgmt"></a>Criteri granulari per le Password

Il sistema operativo Windows Server 2008 consente alle organizzazioni di definire criteri password e di blocco account diversi a seconda del gruppo di utenti di un dominio. Nei domini di Active Directory di versioni precedenti a Windows Server 2008 è possibile applicare un solo criterio password e di blocco account a tutti gli utenti del dominio. Tali criteri vengono specificati nei criteri di dominio predefiniti del dominio. Di conseguenza, per definire impostazioni diverse per le password e il blocco degli account a seconda dei gruppi di utenti, le organizzazioni devono creare un filtro password o distribuire più domini, opzioni entrambe onerose.

È ora possibile utilizzare criteri granulari per le password per specificare più criteri password in un unico dominio e applicare restrizioni diverse per i criteri password e di blocco account a seconda dei gruppi di utenti di un dominio. È ad esempio possibile applicare impostazioni più rigide ad account con privilegi e impostazioni meno rigide per gli account di altri utenti. In altri casi è opportuno applicare criteri password speciali per gli account le cui password vengono sincronizzate con altre origini dati. Per una descrizione dettagliata dei criteri granulari per le Password, vedere [Active Directory Domain Services: Criteri granulari per le Password](https://technet.microsoft.com/library/cc770394(WS.10).aspx)

**Quali sono le novità?**

In Windows Server 2012 e successive, con granularità fine password gestione dei criteri viene eseguita più semplice e più visiva, fornendo un'interfaccia utente per gli amministratori di dominio Active Directory per gestirli in centro. Gli amministratori possono ora visualizzare criteri risultanti di un utente specificato, visualizzare e ordinare tutti i criteri password in un dominio specifico e gestire visivamente singoli criteri password.

Se si prevede di usare i criteri granulari per le password in Windows Server 2012, considerare quanto segue:

- I criteri granulari per le password si applicano solo a oggetti utente e gruppi di sicurezza globali oppure a oggetti inetOrgPerson se vengono utilizzati in sostituzione di oggetti utente. Per impostazione predefinita, solo i membri del gruppo Domain Admins possono impostare criteri granulari per le password. È tuttavia possibile delegare l'impostazione di questi criteri ad altri utenti. Il livello di funzionalità del dominio deve essere impostato su Windows Server 2008 o versione successiva.

- È necessario utilizzare per amministrare i criteri granulari per le password tramite un'interfaccia utente grafica di Windows Server 2012 o versione più recente del centro di amministrazione di Active Directory.

    > [!NOTE]
    > È possibile usare **Server Manager** installare amministrazione remota del Server strumenti () per usare la versione corretta di centro di amministrazione di Active Directory per gestire il Cestino tramite un'interfaccia utente.
    >
    > Per informazioni sull'installazione di amministrazione remota del server, vedere l'articolo [strumenti di amministrazione remota del Server](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools).

### <a name="fine-grained-password-policy-step-by-step"></a>Criteri granulari per le password - Procedura dettagliata

Nei passaggi seguenti si utilizzerà Centro di amministrazione di Active Directory per eseguire le attività seguenti relative ai criteri granulari per le password:

- [Passaggio 1: Aumentare il livello funzionale di dominio](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_raise_dfl)
- [Passaggio 2: Creare utenti di test, gruppo e unità organizzativa](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk2_test_fgpp)
- [Passaggio 3: Creare un nuovo criterio granulare per le password](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)
- [Passaggio 4: Visualizzare un insieme risultante di criteri per un utente](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_view_resultant_fgpp)
- [Passaggio 5: Modificare un criterio granulare per le password](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_edit_fgpp)
- [Passaggio 6: Eliminare criteri granulari per le password](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_delete_fgpp)

> [!NOTE]
> Per eseguire i passaggi seguenti, è necessario essere membri del gruppo Domain Admins o disporre di autorizzazioni equivalenti.

#### <a name="bkmk_raise_dfl"></a>Passaggio 1: Aumentare il livello di funzionalità del dominio

Nella procedura seguente si aumenterà il livello di funzionalità del dominio di destinazione a Windows Server 2008 o versione successiva. Per abilitare i criteri granulari per le password, è necessario un livello funzionale di dominio di Windows Server 2008 o versione successiva.

##### <a name="to-raise-the-domain-functional-level"></a>Per aumentare il livello di funzionalità del dominio

1. Fare clic con il pulsante destro sull'icona di Windows PowerShell, fare clic su **Esegui come amministratore** e digitare **dsac.exe** per aprire Centro.

2. Fare clic su **Gestisci**e su **Aggiungi nodi di spostamento** . Selezionare il dominio di destinazione appropriato nella finestra di dialogo **Aggiungi nodi di spostamento** e quindi fare clic su **OK**.

3. Fare clic sul dominio di destinazione nel riquadro di spostamento a sinistra, quindi nel riquadro **Attività** fare clic su **Aumenta livello di funzionalità dominio**. Selezionare un livello di foresta funzionale che sia almeno Windows Server 2008 o versione successiva e quindi fare clic su **OK**.

![Introduzione all'interfaccia di amministrazione di Active Directory](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>comandi equivalenti di Windows PowerShell</em>***

Il cmdlet o i cmdlet di Windows PowerShell seguenti eseguono la stessa funzione della procedura precedente. Immettere ogni cmdlet in una singola riga, anche se qui può sembrare che siano divisi su più righe a causa di vincoli di formattazione.

```powershell
Set-ADDomainMode -Identity contoso.com -DomainMode 3
```

#### <a name="bkmk2_test_fgpp"></a>Passaggio 2: Creare utenti, gruppo e unità organizzativa di prova

Per creare gli utenti di test e il gruppo per questo passaggio, seguire le procedure descritte in questo caso: [Passaggio 3: Creare utenti di test, gruppo e unità organizzativa](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_test_env) (non è necessario creare l'unità Organizzativa per dimostrare i criteri granulari per le password).

#### <a name="bkmk_create_fgpp"></a>Passaggio 3: Creare un nuovo criterio granulare per le password

Nella procedura seguente si creerà un nuovo criterio granulare per le password utilizzando l'interfaccia utente di Centro di amministrazione di Active Directory.

##### <a name="to-create-a-new-fine-grained-password-policy"></a>Per creare un nuovo criterio granulare per le password

1. Fare clic con il pulsante destro sull'icona di Windows PowerShell, fare clic su **Esegui come amministratore** e digitare **dsac.exe** per aprire Centro.

2. Fare clic su **Gestisci**e su **Aggiungi nodi di spostamento** . Selezionare il dominio di destinazione appropriato nella finestra di dialogo **Aggiungi nodi di spostamento** e quindi fare clic su **OK**.

3. Nel riquadro di spostamento di Centro di amministrazione di Active Directory aprire il contenitore **System** e fare clic sul contenitore **Password Settings Container**.

4. Nel riquadro **Attività** fare clic su **Nuovo** e quindi su **Impostazioni password**.

    Compilare o modificare i campi nella pagina delle proprietà per creare un nuovo oggetto **Impostazioni password**. I campi **Nome** e **Precedenza** sono obbligatori.

    ![Introduzione all'interfaccia di amministrazione di Active Directory](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/ADDS_ADACNewFGPP.gif)

5. In **Si applica direttamente a**e su **Aggiungi**, digitare **group1**e quindi fare clic su **OK**.

    In tal modo l'oggetto Criteri password verrà associato ai membri del gruppo globale creato per l'ambiente di testing.

6. Fare clic su **OK** per completare la creazione.

![Introduzione all'interfaccia di amministrazione di Active Directory](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>comandi equivalenti di Windows PowerShell</em>***

Il cmdlet o i cmdlet di Windows PowerShell seguenti eseguono la stessa funzione della procedura precedente. Immettere ogni cmdlet in una singola riga, anche se qui può sembrare che siano divisi su più righe a causa di vincoli di formattazione.

```powershell
New-ADFineGrainedPasswordPolicy TestPswd -ComplexityEnabled:$true -LockoutDuration:"00:30:00" -LockoutObservationWindow:"00:30:00" -LockoutThreshold:"0" -MaxPasswordAge:"42.00:00:00" -MinPasswordAge:"1.00:00:00" -MinPasswordLength:"7" -PasswordHistoryCount:"24" -Precedence:"1" -ReversibleEncryptionEnabled:$false -ProtectedFromAccidentalDeletion:$true
Add-ADFineGrainedPasswordPolicySubject TestPswd -Subjects group1
```

#### <a name="bkmk_view_resultant_fgpp"></a>Passaggio 4: Visualizzare un insieme risultante di criteri per un utente

Nella procedura seguente si visualizzeranno le impostazioni password risultanti per un utente che è un membro del gruppo a cui è stato assegnato un criteri granulari per le password in [passaggio 3: Creare un nuovo criterio granulare per le password](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp).

##### <a name="to-view-a-resultant-set-of-policies-for-a-user"></a>Per visualizzare un insieme risultante di criteri per un utente

1. Fare clic con il pulsante destro sull'icona di Windows PowerShell, fare clic su **Esegui come amministratore** e digitare **dsac.exe** per aprire Centro.

2. Fare clic su **Gestisci**e su **Aggiungi nodi di spostamento** . Selezionare il dominio di destinazione appropriato nella finestra di dialogo **Aggiungi nodi di spostamento** e quindi fare clic su **OK**.

3. Selezionare un utente **test1** che appartiene al gruppo **group1** che è stato associato un criterio granulare per le password in [passaggio 3: Creare un nuovo criterio granulare per le password](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp).

4. Fare clic su **Visualizza impostazioni password risultanti** nel riquadro **Attività**.

5. Esaminare i criteri di impostazione password e quindi fare clic su **Annulla**.

![Introduzione all'interfaccia di amministrazione di Active Directory](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>comandi equivalenti di Windows PowerShell</em>***

Il cmdlet o i cmdlet di Windows PowerShell seguenti eseguono la stessa funzione della procedura precedente. Immettere ogni cmdlet in una singola riga, anche se qui può sembrare che siano divisi su più righe a causa di vincoli di formattazione.

```powershell
Get-ADUserResultantPasswordPolicy test1
```

#### <a name="bkmk_edit_fgpp"></a>Passaggio 5: Modificare un criterio granulare per le password

Nella procedura seguente si modificherà i criteri granulari per le password creati in [passaggio 3: Creare un nuovo criterio granulare per le password](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)

##### <a name="to-edit-a-fine-grained-password-policy"></a>Per modificare un criterio granulare per le password

1. Fare clic con il pulsante destro sull'icona di Windows PowerShell, fare clic su **Esegui come amministratore** e digitare **dsac.exe** per aprire Centro.

2. Fare clic su **Gestisci**e su **Aggiungi nodi di spostamento** . Selezionare il dominio di destinazione appropriato nella finestra di dialogo **Aggiungi nodi di spostamento** e quindi fare clic su **OK**.

3. Nel **riquadro di spostamento** di Centro di amministrazione di Active Directory espandere **Sistema** e fare clic su **Contenitore Impostazioni password**.

4. Selezionare i criteri granulari per le password creati in [passaggio 3: Creare un nuovo criterio granulare per le password](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp) e fare clic su **delle proprietà** nel **attività** riquadro.

5. In **Imponi cronologia delle password** modificare il valore di **Numero di password memorizzate** in **30**.

6. Fare clic su **OK**.

![Introduzione all'interfaccia di amministrazione di Active Directory](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>comandi equivalenti di Windows PowerShell</em>***

Il cmdlet o i cmdlet di Windows PowerShell seguenti eseguono la stessa funzione della procedura precedente. Immettere ogni cmdlet in una singola riga, anche se qui può sembrare che siano divisi su più righe a causa di vincoli di formattazione.

```powershell
Set-ADFineGrainedPasswordPolicy TestPswd -PasswordHistoryCount:"30"
```

#### <a name="bkmk_delete_fgpp"></a>Passaggio 6: Eliminare criteri granulari per le password

##### <a name="to-delete-a-fine-grained-password-policy"></a>Per eliminare criteri granulari per le password

1. Fare clic con il pulsante destro sull'icona di Windows PowerShell, fare clic su **Esegui come amministratore** e digitare **dsac.exe** per aprire Centro.

2. Fare clic su **Gestisci**e su **Aggiungi nodi di spostamento** . Selezionare il dominio di destinazione appropriato nella finestra di dialogo **Aggiungi nodi di spostamento** e quindi fare clic su **OK**.

3. Nel riquadro di spostamento di Centro di amministrazione di Active Directory espandere **Sistema** e fare clic sul contenitore **Impostazioni password**.

4. Selezionare i criteri granulari per le password creati in [passaggio 3: Creare un nuovo criterio granulare per le password](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp) e il **attività** riquadro fare clic su **proprietà**.

5. Deselezionare la casella di controllo **Proteggi da eliminazioni accidentali** e fare clic su **OK**.

6. Selezionare i criteri granulari per le password e fare clic su **Elimina** nel riquadro **Attività**.

7. Fare clic su **OK** nella finestra di dialogo di conferma.

![Introduzione all'interfaccia di amministrazione di Active Directory](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>comandi equivalenti di Windows PowerShell</em>***

Il cmdlet o i cmdlet di Windows PowerShell seguenti eseguono la stessa funzione della procedura precedente. Immettere ogni cmdlet in una singola riga, anche se qui può sembrare che siano divisi su più righe a causa di vincoli di formattazione.

```powershell
Set-ADFineGrainedPasswordPolicy -Identity TestPswd -ProtectedFromAccidentalDeletion $False
Remove-ADFineGrainedPasswordPolicy TestPswd -Confirm
```

## <a name="windows_powershell_history_viewer"></a>Visualizzatore della cronologia di PowerShell di Windows

Centro di amministrazione di Active Directory è uno strumento di interfaccia utente basato su Windows PowerShell. In Windows Server 2012 e versioni successive, gli amministratori IT possono sfruttare Centro per acquisire familiarità con Windows PowerShell per i cmdlet di Active Directory tramite il Visualizzatore della cronologia di Windows PowerShell. Poiché le azioni vengono eseguite nell'interfaccia utente, il comando di Windows PowerShell equivalente viene visualizzato nel Visualizzatore della cronologia di Windows PowerShell. In tal modo gli amministratori possono creare script automatizzati e ridurre le attività ripetitive, incrementando la produttività. Inoltre, questa funzionalità consente di ridurre il tempo necessario per acquisire familiarità con Windows PowerShell per Active Directory e aumenta la fiducia degli utenti correttezza degli script di automazione creati.

Quando si usa il Visualizzatore della cronologia di Windows PowerShell in Windows Server 2012 o versioni successive, considerare quanto segue:

- Per usare il Visualizzatore di Script di Windows PowerShell, è necessario utilizzare il Windows Server 2012 o versione più recente del centro

    > [!NOTE]
    > È possibile usare **Server Manager** installare amministrazione remota del Server strumenti () per usare la versione corretta di centro di amministrazione di Active Directory per gestire il Cestino tramite un'interfaccia utente.
    >
    > Per informazioni sull'installazione di amministrazione remota del server, vedere l'articolo [strumenti di amministrazione remota del Server](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools).

- Avere una conoscenza di base di Windows PowerShell. ad esempio il funzionamento del piping. Per altre informazioni sul piping in Windows PowerShell, vedere [Piping e pipeline in Windows PowerShell](https://technet.microsoft.com/library/ee176927.aspx).

### <a name="windows-powershell-history-viewer-step-by-step"></a>Visualizzatore della cronologia di Windows PowerShell - Procedura dettagliata

Nella procedura seguente si utilizzerà il Visualizzatore della cronologia di Windows PowerShell di Centro di amministrazione di Active Directory per creare uno script di Windows PowerShell.  Prima di iniziare questa procedura, rimuovere l'utente **test1** dal gruppo **group1**.

#### <a name="to-construct-a-script-using-powershell-history-viewer"></a>Per creare uno script con il Visualizzatore della cronologia di Windows PowerShell

1. Fare clic con il pulsante destro sull'icona di Windows PowerShell, fare clic su **Esegui come amministratore** e digitare **dsac.exe** per aprire Centro.

2. Fare clic su **Gestisci**e su **Aggiungi nodi di spostamento** . Selezionare il dominio di destinazione appropriato nella finestra di dialogo **Aggiungi nodi di spostamento** e quindi fare clic su **OK**.

3. Espandere il riquadro **Visualizzatore della cronologia di Windows PowerShell** nella parte inferiore della schermata di Centro di amministrazione di Active Directory.

4. Selezionare l'utente **test1**.

5. Fare clic su **Aggiungi al gruppo...**  nella **attività** riquadro.

6. Passare a **group1** e fare clic su **OK** nella finestra di dialogo.

7. Passare al riquadro **Cronologia di Windows PowerShell** e individuare il comando appena generato.

8. Copiare il comando e incollarlo nell'editor desiderato per creare lo script.

    È ad esempio possibile modificare il comando per aggiungere un utente diverso a **group1** oppure aggiungere **test1** a un gruppo diverso.

## <a name="see-also"></a>Vedere anche

[Advanced AD DS gestione utilizzando Centro di amministrazione di Active Directory &#40;livello 200&#41;](Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md)