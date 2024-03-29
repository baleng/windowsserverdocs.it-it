---
title: Creazione del file Cfg.ini
description: Viene descritto come utilizzare Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 93a73556-22ef-402d-b8d4-582b74c22bcf
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 967db5f36ea27fb04eab9a6682a106ba0072d45d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820122"
---
# <a name="create-the-cfgini-file"></a>Creazione del file Cfg.ini

>Si applica a: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Il file cfg.ini consente di automatizzare un'installazione del sistema operativo nel seguente scenario:  
  
-   Durante l'analisi dell'uso di un'immagine preinstallata sul computer di destinazione, la sezione di configurazione iniziale viene utilizzata per procedere all'installazione in modalità manuale o automatica. A tale scopo, vedere [Create the Initial Configuration section](Create-the-Cfg.ini-File.md#BKMK_CreateInit2).  
  
##  <a name="BKMK_CreateInit2"></a> Creare la sezione di configurazione iniziale  
 Utilizzare la sezione di configurazione iniziale del file cfg.ini per eseguire l'installazione in modalità manuale o automatica.  
  
#### <a name="to-define-the-initial-configuration-section"></a>Definizione della sezione di configurazione iniziale  
  
1.  Se presente, aprire il file cfg.ini con il Blocco note; in caso contrario, creare un nuovo file.  
  
2.  Aggiungere il seguente testo per creare una sezione InitialConfiguration.  
  
    ```  
  
    [InitialConfiguration]  
    ;Optional, display language can only be one of the installed language  
    Language=en-us  
    ;Optional, The name of a script that runs after setupComplete.cmd but before the initial configuration begins.  
    ;Optional  
    Locale=en-us  
    ;Optional  
    Country=US  
    ;Optional  
    Keyboard=0409:00000409  
    AcceptEula=true  
    ;This is only required on a server where an OEM EULA has been specified   
    ;by using the OOBE.xml file  
    AcceptOEMEula=true  
    ;Optional. Example: My Company Name  
    CompanyName=EnterCompanyName  
    ServerName=EnterServerName  
    ; Example: CONTOSO  
    NetbiosName=EnterNetbiosDomainName  
    ; Example: contoso.local  
    DNSName=EnterDNSDomain   
    ; Used to set the user name for the domain admin  
    UserName=EnterDomainAdminUserName  
    ;The password has to be strong and at least 8 characters  
    PlainTextPassword=EnterAdminPassword  
    ;. Used to set the user name for the domain standard user account. Ignored in migration mode.  
    StdUserName=EnterDomainStandardUserName  
    ;. The password for the domain standard user account has to be strong and at least 8 characters  
    StdUserPlainTextPassword=EnterStandardUserPassword  
    ;Controls the Watson and automatic update settings  
    Settings=All or Updates or None  
    WebDomainName=www.abc.com  
    TrustedCertFileName=c:\cert\a.pfx  
    TrustedCertPassword=Enteryourpassword  
    EnableVPN=true  
    EnableRWA=true  
    IPv4DNSForwarder=<IPV4Address,IPV4Address,¦>  
    IPv6DNSForwarder=<IPV6Address,IPV6Address,¦>  
    VpnIPv4StartAddress=<IPV4Address>  
    VpnIPv4EndAddress=<IPV4Address>  
    VpnBaseIPv6Address=<IPV6Address>  
    VpnIPv6PrefixLength=<number>  
    ;All these section are optional.  
     [PostOSInstall]  
    ;Optional, The name of a script that runs after setupComplete.cmd but before the initial configuration begins.  
  
    IsHosted=true  
    StaticIPv4Address=<IPV4Address>  
    StaticIPv4Gateway=<IPV4Address>  
    StaticIPv4SubnetMask=<IPV4SubnetMask>   
    StaticIPv6Address=<IPV6Address>  
    StaticIPv6SubnetPrefixLength=<number>  
    StaticIPv6Gateway=<IPV6Address>  
    ClientBackupOn=true  
    FileHistoryOn=true  
    LaunchPadHiddenTasks=<Microsoft.LaunchPad.AdminDashboard,Microsoft.LaunchPad.Backup>  
  
    ```  
  
    > [!NOTE]
    >  Non è possibile selezionare una diversa lingua nel corso della configurazione iniziale. Se il sistema viene ripristinato, la lingua del sistema operativo sarà quella installata originariamente.  
  
    |Nome parametro|Descrizione parametro|  
    |--------------------|---------------------------|  
    |*AcceptEula*|Indica che l'utente accetta le Condizioni di licenza software Microsoft. Il valore può essere True o False, tuttavia l'installazione continua solo se viene impostato su True.|  
    |*AcceptOEMEula*|(Facoltativo) Indica che l'utente accetta il contratto di licenza partner. Il valore può essere True o False. Questo campo è obbligatorio soltanto se il server è stato acquistato presso un partner che ha fornito un accordo di licenza distinto.|  
    |*CompanyName*|(Facoltativo) Ragione sociale della società. La ragione sociale viene utilizzata per associare il server alla società e per personalizzare i rapporti aziendali. Può essere composto da un massimo di 254 caratteri.|  
    |*Country*|(Facoltativo) Stringa che indica il paese/regione desiderato. Esempio: US per Stati Uniti.|  
    |*ServerName*|Il nome server identifica in maniera univoca il server sulla rete. Il nome server deve soddisfare i criteri riportati di seguito.<br /><br /> -Può essere fino a 15 caratteri.<br /><br /> -Può contenere lettere, numeri e trattini (-).<br /><br /> -Non deve iniziare con un trattino.<br /><br /> -Non può contenere spazi.<br /><br /> -Non può contenere solo numeri.<br /><br /> Esempio: ContosoServer.|  
    |*DNSName*|In un dominio interno vengono raggruppati i computer server e client per consentire la condivisione di un database comune di nomi utente, password e altre informazioni comuni. Questo nome viene visualizzato al momento dell'accesso ai computer da parte degli utenti, ma viene utilizzato solo internamente e non corrisponde al nome di dominio Internet. Il nome di dominio interno deve soddisfare i criteri specifici per il *ServerName*.<br /><br /> Ad esempio: contoso.local.|  
    |*NetbiosName*|Un nome NetBIOS viene utilizzato per individuare le risorse in esecuzione sul server. Può essere composto da un massimo di 15 caratteri. Esempio: Contoso.|  
    |*Lingua*|(Facoltativo) Specifica la lingua visualizzata. Deve essere una delle lingue installate. Ad esempio: en-us indica l'inglese utilizzato negli Stati Uniti d'America.|  
    |*Impostazioni locali*|(Facoltativo) Specifica il formato ora e valuta usando un formato *LocaleID* . Ad esempio: en-us per la valuta e l'ora visualizzate in inglese e con un formato che rispetta gli standard utilizzati negli Stati Uniti d'America.|  
    |*Tastiera*|La tastiera può utilizzare i seguenti due formati:<br /><br /> - **layout input: tastiera nella lingua.** Ad esempio: 0409:00000409, dove 0409 prima di **:** è la lingua di input e **00000409** è il layout di tastiera. L'elenco dei layout di tastiera si trova nella chiave del Registro di sistema **HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Keyboard Layouts**.<br /><br /> - **lingua di input: identificatore IME.** Di seguito è fornito un elenco completo degli identificatori IME.<br /><br /> -Metodo di Input Amharico {E429B25A-E5D3-4D1F-9BE3-0C608477E3A1}{8F96574E-C86C-4bd6-9666-3F7327D4CBE8}<br /><br /> -{81d4e9c9-1d3b-41bc-9e6c-4b40bf79e35e}{FA550B04-5AD7-411F-A5AC-CA038EC515D7} Microsoft Pinyin - Simple Fast (cinese semplificato)<br /><br /> -{531FDEBF-9B4C-4A43-A2AA-960E8FCDC732}{B2F9C502-1742-11D4-9790-0080C882687E} cinese (tradizionale) - nuovo fonetico<br /><br /> -Cinese (tradizionale) {531FDEBF-9B4C-4A43-A2AA-960E8FCDC732}{4BDF9F03-C7D3-11D4-B2AB-0080C882687E} - ChangJie<br /><br /> Quick - {531FDEBF-9B4C-4A43-A2AA-960E8FCDC732}{6024B45F-5C54-11D4-B921-0080C882687E} cinese (tradizionale)-<br /><br /> -Matrice tradizionale cinese {E429B25A-E5D3-4D1F-9BE3-0C608477E3A1}{D38EFF65-AA46-4FD5-91A7-67845FB02F5B}<br /><br /> -DaYi tradizionale cinese {E429B25A-E5D3-4D1F-9BE3-0C608477E3A1}{037B2C25-480C-4D7F-B027-D6CA6B69788A}<br /><br /> -{03B5835F-F03C-411B-9CE2-AA23E1171E36}{A76C93D9-5523-4E90-AAFA-4DB112F9AC76} Microsoft IME (giapponese)<br /><br /> - {A028AE76-01B1-46C2-99C4-ACD9858AE02F}{B5FE1F02-D5F2-4445-9C03-C568F23C99A1}             Microsoft IME (Korean)<br /><br /> - {A1E2B86B-924A-4D43-80F6-8A820DF7190F}{B60AF051-257A-46BC-B9D3-84DAD819BAFB}         Old Hangul IME (Korean)<br /><br /> -Metodo di Input Yi {E429B25A-E5D3-4D1F-9BE3-0C608477E3A1}{409C8376-007B-4357-AE8E-26316EE3FB0D}<br /><br /> -Metodo di Input Tigrino {E429B25A-E5D3-4D1F-9BE3-0C608477E3A1}{3CAB88B7-CC3E-46A6-9765-B772AD7761FF}|  
    |*Impostazioni*|Imposta la selezione dell'utente per gli aggiornamenti. Utilizzare uno dei valori seguenti:<br /><br /> **-Tutte** equals Usa impostazioni consigliata.<br /><br /> **-Aggiorna** uguale a installare gli aggiornamenti importanti. Solo<br /><br /> **-None** equals verifica la presenza di aggiornamenti.|  
    |*Nome utente*|-Il nome del nuovo account amministratore creato durante l'installazione. I nomi account amministratore e utente standard devono soddisfare i criteri riportati di seguito.<br /><br /> -Può essere fino a 19 caratteri.<br /><br /> -Non possono contenere / \ [] &#124; < > + =; , ? *<br /><br /> -Non devono iniziare o terminare con un punto.<br /><br /> -Non può contenere due punti consecutivi.<br /><br /> -Deve essere lo stesso come il nome del server o un nome di dominio interno.<br /><br /> -Deve essere lo stesso nome utente predefinito, ad esempio amministratore o Guest.|  
    |*PlainTextPassword*|Si tratta della password per il nuovo account amministratore creato durante la configurazione.<br /><br /> -Deve essere composta da almeno otto caratteri.<br /><br /> -Deve contenere almeno tre delle quattro categorie seguenti:<br /><br /> -Lettere maiuscole caratteri.<br /><br /> -Lettere minuscole.<br /><br /> -Numeri.<br /><br /> -I simboli.|  
    |*StdUserName*|Nome del nuovo account utente standard creato durante l'installazione. Per i requisiti, vedere il parametro *UserName*.|  
    |*StdUserPlainTextPassword*|Password per l'account utente standard creato durante l'installazione.|  
    |WebDomainName|(Facoltativo) Configurare il nome del dominio Internet del server. Questo file consente di configurare il nome del dominio in modo simile al metodo utilizzato per la configurazione manuale guidata del nome di dominio.|  
    |TrustedCertFileName|(Facoltativo) Configurare il certificato attendibile per il nome del dominio. Questo consente di inserire un certificato .PFX che contiene la chiave privata.|  
    |TrustedCertPassword|(Facoltativo) La password per importare il certificato .PFX.|  
    |EnableVPN|(Facoltativo) Attivare VPN per impostazione predefinita.|  
    |VpnIPv4StartAddress|(Facoltativo) Impostare l'indirizzo VPN di inizio.|  
    |VpnIPv4EndAddress|(Facoltativo) Impostare l'indirizzo VPN di fine.|  
    |VpnBaseIPv6Address|(Facoltativo) Impostare l'indirizzo IPV6 di base per VPN.|  
    |VpnIPv6PrefixLength|(Facoltativo) Impostare la lunghezza del prefisso dell'indirizzo IPv6 VPN.|  
    |IsHosted|(Facoltativo) Se non specificato, il valore predefinito è false. Impostare questo valore se la configurazione viene eseguita in un ambiente ospitante. Disabiliterà la configurazione del router.|  
    |StaticIPv4Address|(Facoltativo) Specificare l'indirizzo IP se si desidera configurare un indirizzo IP statico piuttosto che dinamico.|  
    |StaticIPv4Gateway|(Facoltativo) Specificare l'indirizzo gateway predefinito se si desidera configurare un indirizzo IP statico piuttosto che dinamico.|  
    |StaticIPv4SubnetMask|(Facoltativo) Specificare la subnet mask se si vuole configurare un indirizzo IP statico invece di un indirizzo dinamico.|  
    |StaticIPv6Address|(Facoltativo) Specificare l'indirizzo IP predefinito se si desidera configurare un indirizzo IP statico piuttosto che dinamico.|  
    |StaticIPv6SubnetPrefixLength|(Facoltativo) Specificare la lunghezza predefinita per il prefisso della subnet IPV6 se si desidera configurare un indirizzo IP statico piuttosto che dinamico.|  
    |StaticIPv6Gateway|(Facoltativo) Specificare l'indirizzo gateway predefinito se si desidera configurare un indirizzo IP statico piuttosto che dinamico.|  
    |ClientBackupOn|(Facoltativo) Disattivare il backup client per impostazione predefinita quando i nuovi client vengono aggiunti al server.|  
    |FileHistoryOn|(Facoltativo) Disattivare il backup di Cronologia file per impostazione predefinita quando i nuovi client con Windows 8 Consumer Preview vengono aggiunti al server.|  
    |EnableRWA|Abiliterà accesso Web remoto quando si installa Windows Server Essentials, ma ignorerà la configurazione del router. Questa soluzione è supportata solo in un'installazione pulita del prodotto. Il valore predefinito è false.|  
    |IPv4DNSForwarder|Impostare il server di inoltro DNS IPv4.|  
    |IPv6DNSForwarder|Impostare il server di inoltro DNS IPv6.|  
    |LaunchPadHiddenTasks|-(Facoltativo) è possibile nascondere la voce di Backup o / e Dashboard di amministrazione voce nella finestra di avvio.<br /><br /> -Per disabilitare il dashboard: LaunchPadHiddenTasks=Microsoft.LaunchPad.AdminDashboard<br /><br /> -Per disabilitare il backup: LaunchPadHiddenTasks=Microsoft.LaunchPad.Backup<br /><br /> -Per disabilitare il backup e il dashboard: LaunchPadHiddenTasks=Microsoft.LaunchPad.Backup,Microsoft.LaunchPad.AdminDashboard|  
  
3.  Salvare il file. Assicurarsi di salvare il file come cfg.ini, non come cfg.ini.txt.  
  
    > [!NOTE]
    >  È possibile salvare il file su un'unità flash USB, da utilizzare per passaggi specifici dell'installazione. Oppure, il file cfg.ini è disponibile nella radice di qualsiasi unità disco rigido del server di destinazione. Accertarsi che per il file venga utilizzata la codifica ANSI o Unicode; la codifica UTF-8 non è supportata.  
  
> [!IMPORTANT]
>  La sezione di configurazione iniziale del file cfg.ini deve essere utilizzata solo dall'utente finale per personalizzare il server oppure da un partner per analizzare l'uso del server da parte dell'utente utilizzando un file di risposte automatico. Questa sezione del file non è destinata alla creazione dell'immagine.  
  
## <a name="see-also"></a>Vedere anche  

 [Guida introduttiva a Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Creazione e personalizzazione dell'immagine](Creating-and-Customizing-the-Image.md)   
 [Personalizzazioni aggiuntive](Additional-Customizations.md)   
 [Preparazione dell'immagine per la distribuzione](Preparing-the-Image-for-Deployment.md)   
 [Testare l'esperienza dei clienti](Testing-the-Customer-Experience.md)

 [Guida introduttiva a Windows Server Essentials ADK](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Creazione e personalizzazione dell'immagine](../install/Creating-and-Customizing-the-Image.md)   
 [Personalizzazioni aggiuntive](../install/Additional-Customizations.md)   
 [Preparazione dell'immagine per la distribuzione](../install/Preparing-the-Image-for-Deployment.md)   
 [Testare l'esperienza dei clienti](../install/Testing-the-Customer-Experience.md)

