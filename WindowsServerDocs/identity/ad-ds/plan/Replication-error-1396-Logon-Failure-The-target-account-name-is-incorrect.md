---
ms.assetid: 399a8bbe-3375-4bb0-b55b-5f46e7050028
title: Errore di replica 1396 Errore di accesso. Il nome dell'account di destinazione non è corretto
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: a8af10fd54f557e4f4a2127dbd1cc178d53d93a4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402485"
---
# <a name="replication-error-1396-logon-failure-the-target-account-name-is-incorrect"></a>Errore di replica 1396 Errore di accesso. Il nome dell'account di destinazione non è corretto

>Si applica a: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd"> <introduction> @ no__t-2 @ no__t-3<para>Questo articolo descrive i sintomi, le cause e la risoluzione dei problemi Active Directory replica con errore Win32 1396: errore &quot;Logon: Il nome dell'account di destinazione non è corretto. &quot; </para>
    <list class="bullet"> <listItem> @ no__t-2 @ no__t-3<para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Symptoms">Sintomi</link>
 @ no__t-2</para>
      </listItem> <listItem> @ no__t-2 @ no__t-3<para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Causes">Causa</link>
 @ no__t-2</para>
      </listItem> <listItem> @ no__t-2 @ no__t-3<para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Resolutions">Risoluzioni</link>
 @ no__t-2</para>
      </listItem>
    </list>
  </introduction>
  <section address="BKMK_Symptoms">
    <title>Symptoms @ no__t-1 @ no__t-2 @ no__t-3<para />
      <list class="ordered">
<listItem><para>DCDIAG segnala che il test delle repliche Active Directory non è riuscito con l'errore 1396: Errore di accesso: Il nome dell'account di destinazione non è corretto. &quot;</para><code>Testing server: &lt;Site name&gt;&lt;DC Name&gt;
Starting test: Replications
[Replications Check,&lt;DC Name&gt;] A recent replication attempt failed:
From &lt;source DC&gt; to &lt;destination DC&gt;
Naming Context: CN=&lt;DN path of naming context&gt;
<codeFeaturedElement>The replication generated an error (1396):
Logon Failure: The target account name is incorrect.</codeFeaturedElement>
The failure occurred at &lt;date&gt; &lt;time&gt;.
The last success occurred at &lt;date&gt; &lt;time&gt;.
XX failures have occurred since the last success</code></listItem><listItem><para>REPADMIN. EXE indica che l'ultimo tentativo di replica non è riuscito con lo stato 1396.</para><para>I comandi REPADMIN che comunemente citano lo stato 1396 includono ma non sono limitati a:</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><tbody><tr><TD><list class="bullet"><listItem><para>REPADMIN/ADD</para></listItem><listItem><para>REPADMIN/REPLSUM.</para></listItem><listItem><para>REPADMIN/REHOST</para></listItem><listItem><para>REPADMIN/SHOWVECTOR/LATENCY</para></listItem></list></TD><TD><list class="bullet"><listItem><para>REPADMIN/SHOWREPS</para></listItem><listItem><para>REPADMIN/SHOWREPL</para></listItem><listItem><para>REPADMIN /SYNCALL</para></listItem></list></TD></tr></tbody></table><para>Esempio di output di &quot;REPADMIN/SHOWREPS @ no__t-1 che illustra la replica in ingresso da CONTOSO-DC2 a CONTOSO-DC1 con errore &quot;Logon: Il nome dell'account di destinazione non è corretto. di seguito è riportato un errore &quot;:</para><code>Default-First-Site-NameCONTOSO-DC1
DSA Options: IS_GC 
Site Options: (none)
DSA object GUID: b6dc8589-7e00-4a5d-b688-045aef63ec01
DSA invocationID: b6dc8589-7e00-4a5d-b688-045aef63ec01
==== INBOUND NEIGHBORS ======================================
DC=contoso,DC=com
Default-First-Site-NameCONTOSO-DC2 via RPC
DSA object GUID: 74fbe06c-932c-46b5-831b-af9e31f496b2
Last attempt @ &lt;date&gt; &lt;time&gt; failed, <codeFeaturedElement>result 1396 (0x574):
Logon Failure: The target account name is incorrect.</codeFeaturedElement>
&lt;#&gt; consecutive failure(s).
Last success @ &lt;date&gt; &lt;time&gt;.
</code></listItem><listItem><para>Il comando <ui>Replicate Now</ui> in Active Directory Sites and Services restituisce un errore &quot;Logon: Il nome dell'account di destinazione non è corretto. &quot;</para><para>Facendo clic con il pulsante destro del mouse sull'oggetto connessione da un controller di dominio di origine e scegliendo <ui>Replica ora</ui> non riesce con errore &quot;Logon: Il nome dell'account di destinazione non è corretto. &quot; Di seguito è riportato il messaggio di errore su schermo:</para><para>Testo del titolo della finestra di dialogo:</para><para>Esegui replica ora</para><para>Testo del messaggio di dialogo: </para><para>Si è verificato il seguente errore durante il tentativo di sincronizzare il contesto dei nomi @no__t-percorso DNS 0partition @ no__t-1 dal controller di dominio &lt;source DC @ no__t-3 al controller di dominio &lt;destination DC @ no__t-5: Errore di accesso: Il nome dell'account di destinazione non è corretto. Questa operazione non continuerà. </para></listItem><listItem><para>Gli eventi NTDS KCC, NTDS General o Microsoft-Windows-ActiveDirectory DomainService con lo stato 1396 vengono registrati nel registro dei servizi directory Visualizzatore eventi.</para><para>Active Directory eventi che comunemente citano lo stato 1396 includono ma non sono limitati a:</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><thead><tr><TD><para>ID evento</para></TD><TD><para>Origine evento</para></TD><TD><para>Stringa dell'evento</para></TD></tr></thead><tbody><tr><TD><para>1125</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Il Installazione guidata di Active Directory Domain Services (Dcpromo) non è riuscito a stabilire una connessione con il controller di dominio seguente.</para></TD></tr><tr><TD><para>1645</para><para>Questo evento elenca il nome SPN in tre parti.</para></TD><TD><para>Replica NTDS</para></TD><TD><para>Impossibile eseguire una chiamata di procedura remota (RPC) autenticata verso un altro controller di dominio. Il nome principale del servizio (SPN) per il controller di dominio di destinazione non è registrato nel controller di dominio Centro distribuzione chiavi (KDC) che risolve il nome SPN.</para></TD></tr><tr><TD><para>1655</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Active Directory Domain Services ha tentato di comunicare con il catalogo globale seguente e i tentativi non sono riusciti.</para></TD></tr><tr><TD><para>2847</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Il controllo di coerenza informazioni ha individuato una connessione di replica per il servizio directory di sola lettura locale e ha tentato di aggiornarlo in remoto nell'istanza del servizio directory seguente. Operazione non riuscita. Verrà eseguito un nuovo tentativo.</para></TD></tr><tr><TD><para>1925</para></TD><TD><para>NTDS KCC</para></TD><TD><para>Non è riuscito il tentativo di stabilire un collegamento di replica per la partizione di directory scrivibile.</para></TD></tr><tr><TD><para>1926</para></TD><TD><para>NTDS KCC</para></TD><TD><para>Il tentativo di stabilire un collegamento di replica per una partizione di directory di sola lettura con i seguenti parametri non è riusciti.</para></TD></tr><tr><TD><para>5781</para></TD><TD><para>NETLOGON</para></TD><TD><para> Il server non è in grado di registrare il nome in DNS.</para></TD></tr></tbody></table></listItem><listItem><para>DCPROMO ha esito negativo e viene visualizzato un errore sullo schermo</para><para>Testo del titolo della finestra di dialogo:</para><para>Installazione Active Directory non riuscita</para><para>Testo del messaggio di dialogo:</para><para>Operazione non riuscita. Motivo: Il servizio directory non è riuscito a creare l'oggetto server per CN = NTDS Settings, CN = ServerBeingPromoted, CN = Servers, CN = site, CN = Sites, CN = Configuration, DC = contoso, DC = com nel server ReplicationSourceDC.contoso.com. </para><para>Verificare che le credenziali di rete fornite dispongano di diritti di accesso sufficienti per aggiungere una replica. </para><para>
Errore &quot;Logon: Il nome dell'account di destinazione non è corretto. &quot;</para><para>In questo caso, l'ID evento 1645, 1168 e 1125 viene registrato sul server che viene innalzato di più.</para></listItem><listItem><para>Eseguire il mapping di un'unità usando <embeddedLabel>net use</embeddedLabel>:</para><code>C:&gt;net use z: &lt;server_name&gt;c$
System error 1396 has occurred.
Logon Failure: The target account name is incorrect.</code><para>In questo caso, il server può anche registrare l'ID evento 333 nel registro eventi di sistema e usare una quantità elevata di memoria virtuale per un'applicazione, ad esempio SQL Server.</para></listItem><listItem><para>L'ora del controller di dominio non è corretta.</para></listItem><listItem><para>Il KDC non viene avviato in un RODC dopo un ripristino dell'account krbtgt per il RODC, che è stato eliminato. Ad esempio, dopo un ripristino, viene visualizzato l'errore 1396. </para><para>
L'ID evento 1645 è registrato nel controller di sola lettura. </para><para>
Dcdiag genera inoltre un errore che indica che non è possibile aggiornare l'account krbtgt RODC. </para></listItem>
</list>
    </content>
  </section>
  <section address="BKMK_Causes">
    <title>Causes @ no__t-1 @ no__t-2 @ no__t-3<para />
      <list class="ordered">
        <listItem>
          <para>Il nome SPN non esiste nel catalogo globale cercato dal KDC per conto del client che tenta di eseguire l'autenticazione tramite Kerberos.</para>
          <para>Nel contesto della replica Active Directory, il client Kerberos è il controller di dominio di destinazione, il KDC che esegue la ricerca SPN è probabilmente il controller di dominio di destinazione, ma potrebbe essere un controller di dominio remoto.</para>
        </listItem>
        <listItem>
          <para>L'account utente o del servizio che deve contenere il nome dell'entità servizio da cercare non esiste nel catalogo globale cercato dal KDC per conto del controller di dominio di destinazione che tenta di eseguire la replica.</para>
          <para>Nel contesto della replica Active Directory, l'account del computer del controller di dominio di origine non esiste nel catalogo globale cercato dal controller di dominio per conto del controller di dominio di destinazione che esegue la replica in ingresso.</para>
        </listItem>
        <listItem>
          <para>Il controller di dominio di destinazione non dispone di un segreto LSA per il dominio del controller di dominio di origine.</para>
        </listItem>
        <listItem>
          <para>Il nome SPN da cercare esiste in un account computer diverso da quello del controller di dominio di origine.</para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_Resolutions">
    <title>Resolutions @ no__t-1 @ no__t-2 @ no__t-3 @ no__t-4 @ no__t-5<para>Controllare il registro eventi del servizio directory nel controller di dominio di destinazione per l'evento di replica NTDS 1645 e tenere presente quanto segue:</para>
          <para>Nome del controller di dominio di destinazione</para>
          <para>Nome SPN cercato (GUID E3514235-4B06-11D1-AB04-00C04FC2DCD2/&lt;object per i controller di dominio di origine NTDS Settings Object @ no__t-1 @ no__t-2 @ no__t-3target Domain @ no__t-4Amp; gt;. &amp;Amp; lt; TLD @ no__t-6Amp; gt; @ &lt;target dominio @ no__t-8. &lt;tld @ no__t-10</para>
          <para>KDC utilizzato dal controller di dominio di destinazione</para>
        </listItem>
        <listItem>
          <para>Dalla console del KDC identificato nel passaggio 1, digitare: </para>
          <code>nltest /dsgetdc &lt;forest root DNS domain name &gt; /gc</code>
          <para>Eseguire il test di NLTEST Locator immediatamente dopo un tentativo di replica che ha esito negativo con l'errore 1396 sul controller di dominio di destinazione. </para>
          <para>Questo dovrebbe identificare il GC con cui il KDC esegue ricerche SPN. </para>
          <para>Il GC cercato dal KDC può anche essere acquisito in Microsoft-Windows-ActiveDirectory DomainService evento 1655.</para>
        </listItem>
        <listItem>
          <para>Cercare il nome SPN individuato nel passaggio 1 nel catalogo globale individuato nel passaggio 2.</para>
          <code>C:&gt;repadmin /showattr Server_Name DC=corp,DC=contoso,dc=com &lt;GC used by KDC&gt; &lt;DN path of forest root domain&gt; /filter:&quot;(serviceprincipalname=&lt;SPN cited in the NTDS Replication event 1645&gt;)&quot; /gc /subtree /atts:cn,serviceprincipalname</code>
          <para>O</para>
          <code>C:&gt;dsquery * forestroot -scope subtree -filter &quot;(serviceprincipalname=E3514235-4B06-11D1-AB04-00C04FC2DCD2/65cead9f-4949-46a3-a49a-f1fbfe13d2b3*)&quot; -attr * -s Server_Name.europe.corp.contoso.com</code>
          <para>Verificare che l'oggetto host per il nome SPN esista.</para>
          <para>Verificare il percorso DN per l'oggetto host, incluso il fatto che l'oggetto sia stato modificato da CNF/conflitto o che si trovi nel contenitore Lost and found.</para>
          <para>Verificare che il controller di dominio di origine Active Directory nome SPN di replica sia registrato solo nell'account del computer controller di dominio di origine.</para>
          <para>Se il nome SPN della replica è mancante, determinare se il controller di dominio di origine ha registrato il nome SPN e se il nome SPN non è presente nel GC utilizzato dal KDC a causa di una latenza di replica semplice o di un errore di replica.</para>
        </listItem>
        <listItem>
          <para>Verificare lo stato di integrità e di attendibilità del canale sicuro.</para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics> @ no__t-1 @ no__t-2Troubleshooting Active Directory operazioni che hanno esito negativo con errore 1396: Errore di accesso: Il nome dell'account di destinazione non è corretto. </linkText>
      <linkUri><a href="https://support.microsoft.com/kb/2183411/en-gb" data-raw-source="https://support.microsoft.com/kb/2183411/en-gb">https://support.microsoft.com/kb/2183411/en-gb</a></linkUri>
    </externalLink>
  </relatedTopics> @ no__t-6


