---
title: Migrazione del database WSUS da (database interno di Windows) WID a SQL
description: "Argomento Windows Server Update Service (WSUS): come eseguire la migrazione del database WSUS (SUSDB) da un'istanza di database interno di Windows a un'istanza locale o remota di SQL Server."
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: get-started article
ms.assetid: 90e3464c-49d8-4861-96db-ee6f8a09g7dr
author: coreyp-at-msft
ms.author: coreyp
manager: dougkim
ms.date: 07/25/2018
ms.openlocfilehash: 0977aa1fd9a6848bd7b85bb592b6a82556277e72
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361583"
---
>Si applica a: Windows Server 2012, Windows Server 2012 R2, Windows Server 2016

# <a name="migrating-the-wsus-database-from-wid-to-sql"></a>Migrazione del database WSUS da WID a SQL

Utilizzare la procedura seguente per eseguire la migrazione del database WSUS (SUSDB) da un'istanza di database interno di Windows a un'istanza locale o remota di SQL Server.

## <a name="prerequisites"></a>Prerequisiti

- Istanza di SQL. Può trattarsi del valore predefinito **MSSQLSERVER** o di un'istanza personalizzata.
- SQL Server Management Studio
- WSUS con ruolo WID installato
- IIS (questo è in genere incluso quando si installa WSUS tramite Server Manager). Poiché non è già installato, sarà necessario.

## <a name="migrating-the-wsus-database"></a>Migrazione del database WSUS

### <a name="stop-the-iis-and-wsus-services-on-the-wsus-server"></a>Arrestare i servizi IIS e WSUS sul server WSUS

Da PowerShell (con privilegi elevati) eseguire:

```powershell
    Stop-Service IISADMIN
    Stop-Service WsusService
```

### <a name="detach-susdb-from-the-windows-internal-database"></a>Scollegare SUSDB dal database interno di Windows

#### <a name="using-sql-management-studio"></a>Uso di SQL Management Studio

1. Fare clic con il pulsante destro del mouse su **SUSDB** - @ no__t-2 **attività** - @ no__t-5 fare clic su **Disconnetti**: ![image1 @ no__t-8
2. Selezionare **Elimina connessioni esistenti** e fare clic su **OK** (facoltativo, se esistono connessioni attive).
    ![image2 @ no__t-1

#### <a name="using-command-prompt"></a>Dal prompt dei comandi

> [!IMPORTANT]
> In questa procedura viene illustrato come scollegare il database WSUS (SUSDB) dall'istanza di database interno di Windows tramite l'utilità **SQLCMD** . Per ulteriori informazioni sull'utilità **SQLCMD** , vedere [utilità sqlcmd](https://go.microsoft.com/fwlink/?LinkId=81183).
> 1. Aprire un prompt dei comandi con privilegi elevati
> 2. Eseguire il comando SQL seguente per scollegare il database WSUS (SUSDB) dall'istanza di database interno di Windows tramite l'utilità **SQLCMD** :

```batchfile
        sqlcmd -S \\.\pipe\Microsoft##WID\tsql\query
        use master
        GO
        alter database SUSDB set single_user with rollback immediate
        GO
        sp_detach_db SUSDB
        GO
```

### <a name="copy-the-susdb-files-to-the-sql-server"></a>Copiare i file SUSDB nel SQL Server

1. Copiare **SUSDB. MDF** e **SUSDB@NO__T-2LOG.LDF** dalla cartella wid data ( **% SystemDrive%** \* * Windows\WID\Data * *) alla cartella dati dell'istanza di SQL.

> [!TIP]
> Se ad esempio la cartella dell'istanza di SQL è **C:\Programmi\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL**e la cartella wid data sono **C:\Windows\WID\Data,** copiare i file SUSDB da **C:\Windows\WID\Data** in **c:\Programmi\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\Data**

### <a name="attach-susdb-to-the-sql-instance"></a>Alleghi SUSDB all'istanza di SQL

1. In **SQL Server Management Studio**, nel nodo **istanza** , fare clic con il pulsante destro del mouse su **database**, quindi scegliere **Connetti**.
    ![image3](images/image3.png)
2. Nella casella **Connetti database** , in **database da alleghi**, fare clic sul pulsante **Aggiungi** e individuare il file **SUSDB. MDF** copiato dalla cartella wid, quindi fare clic su **OK**.
    ![image4 @ no__t-1 ![image5 @ no__t-3

> [!TIP]
> Questa operazione può essere eseguita anche tramite Transact-SQL.  Per le istruzioni, vedere la [documentazione di SQL per il fissaggio di un database](https://docs.microsoft.com/sql/relational-databases/databases/attach-a-database) .
>
> Esempio (uso dei percorsi dell'esempio precedente):
> ```sql
>    USE master;
>    GO
>    CREATE DATABASE SUSDB
>    ON
>        (FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data\SUSDB.mdf'),
>        (FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Log\SUSDB_Log.ldf')
>        FOR ATTACH;
>    GO
>```

### <a name="verify-sql-server-and-database-logins-and-permissions"></a>Verificare gli account di accesso e le autorizzazioni di SQL Server e database

#### <a name="sql-server-login-permissions"></a>Autorizzazioni di accesso SQL Server

Dopo aver collegato il SUSDB, verificare che il **servizio NT AUTHORITY\NETWORK** disponga delle autorizzazioni di accesso all'istanza di SQL Server eseguendo le operazioni seguenti:

1. Passa a SQL Server Management Studio
2. Apertura dell'istanza
3. Fare clic su **sicurezza**
4. Fare clic su **accessi**

L'account **NT Authority\Network Service** deve essere elencato. In caso contrario, è necessario aggiungerlo aggiungendo un nuovo nome di account di accesso.

> [!IMPORTANT]
> Se l'istanza SQL si trova in un computer diverso da WSUS, l'account computer del server WSUS deve essere elencato nel formato **[FQDN] \\ [WSUSComputerName] $** .  In caso contrario, è possibile utilizzare la procedura seguente per aggiungerla, sostituendo **NT Authority\Network Service** con l'account computer del server WSUS ( **[FQDN] \\ [WSUSComputerName] $** ), questo sarebbe ***in aggiunta alla*** concessione dei diritti a **NT Authority \ SERVIZIO di rete**

##### <a name="adding-nt-authoritynetwork-service-and-granting-it-rights"></a>Aggiunta di NT AUTHORITY\NETWORK SERVICE e concessione dei diritti it

1. Fare clic con il pulsante destro del mouse su **accessi** e scegliere **nuovo account di accesso.**
    ![image6 @ no__t-1
2. Nella pagina **generale** compilare il **nome dell'account di accesso** (**NT Authority\Network Service**) e impostare il **database predefinito** su SUSDB.
    ![image7 @ no__t-1
3. Nella pagina **ruoli server** verificare che sia selezionata l'opzione **pubblica** e **sysadmin** .
    ![image8 @ no__t-1
4. Nella pagina **mapping utenti** :
    - In **utenti con mapping a questo account di accesso**: selezionare **SUSDB**
    - In appartenenza a un ruolo **Database per: SUSDB @ no__t-0, verificare che siano controllati gli elementi seguenti:
        - **pubblico**
        - **webService** ![image9 @ no__t-2
5. Fare clic su **OK**

A questo punto verrà visualizzato **NT Authority\Network Service** in account di accesso.
![image10 @ no__t-1

#### <a name="database-permissions"></a>Autorizzazioni database

1. Fare clic con il pulsante destro del mouse su SUSDB
2. Selezione **Proprietà**
3. Fare clic su **autorizzazioni**

L'account **NT Authority\Network Service** deve essere elencato.

1. In caso contrario, aggiungere l'account.
2. Nella casella di testo nome account di accesso immettere il computer WSUS nel formato seguente:
    > [**FQDN] \\ [WSUSComputerName] $**
3. Verificare che il **database predefinito** sia impostato su **SUSDB**.

    > [!TIP]
    > Nell'esempio seguente, il nome di dominio completo è **contosto.com** e il nome del computer WSUS è **WsusMachine**:
    >
    > ![image11](images/image11.png)

4. Nella pagina **mapping** utenti selezionare il database **SUSDB** in **"utenti con mapping a questo account di accesso"**
5. Controllare **WebService** con l'appartenenza al ruolo del database  **per: SUSDB "** : ![image12 @ no__t-2
6. Fare clic su **OK** per salvare le impostazioni.
    > [!NOTE]
    > Per rendere effettive le modifiche, potrebbe essere necessario riavviare il servizio SQL.

### <a name="edit-the-registry-to-point-wsus-to-the-sql-server-instance"></a>Modificare il registro di sistema per puntare WSUS all'istanza di SQL Server

> [!IMPORTANT]
> Segui con attenzione la procedura descritta in questa sezione. Se le modifiche al Registro di sistema vengono apportate in modo non corretto, possono verificarsi problemi gravi. Prima di modificarlo, [esegui il backup del Registro di sistema per il ripristino](https://support.microsoft.com/en-us/help/322756) nel caso in cui si verifichino problemi.

1. Fare clic su **Start**, **Esegui**, digitare **regedit** e fare clic su **OK**.
2. Individuare la chiave seguente: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\UpdateServices\Server\Setup\SqlServerName**
3. Nella casella di testo **valore** Digitare **[nomeserver] \\ [nomeistanza]** , quindi fare clic su **OK**. Se il nome dell'istanza è l'istanza predefinita, digitare **[servername]** .
4. Individuare la chiave seguente: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Update Services\Server\Setup\Installed Role Services\UpdateServices-WidDatabase** ![image13 @ no__t-2
5. Rinominare la chiave in **UpdateServices-Database** ![image41 @ no__t-2

    > [!NOTE]
    > Se non si aggiorna questa chiave, **WsusUtil** tenterà di eseguire il servizio a wid anziché all'istanza di SQL in cui è stata eseguita la migrazione.

### <a name="start-the-iis-and-wsus-services-on-the-wsus-server"></a>Avviare i servizi IIS e WSUS sul server WSUS

Da PowerShell (con privilegi elevati) eseguire:

```powershell
    Start-Service IISADMIN
    Start-Service WsusService
```

> [!NOTE]
> Se si utilizza la console di WSUS, chiuderla e riavviarla.

## <a name="uninstalling-the-wid-role-not-recommended"></a>Disinstallazione del ruolo WID (scelta non consigliata)

> [!WARNING]
> La rimozione del ruolo WID consente inoltre di rimuovere una cartella di database ( **%SystemDrive%\Program Programmi\update Services\Database**) che contiene gli script richiesti da WSUSutil. exe per le attività successive all'installazione. Se si sceglie di disinstallare il ruolo WID, assicurarsi di eseguire prima di tutto il backup della cartella **%SystemDrive%\Program Programmi\update Services\Database** .

Usando PowerShell:

```powershell
Uninstall-WindowsFeature -Name 'Windows-Internal-Database'
```

Dopo la rimozione del ruolo WID, verificare che sia presente la seguente chiave del registro di sistema: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Update Services\Server\Setup\Installed Role Services\UpdateServices-Database**