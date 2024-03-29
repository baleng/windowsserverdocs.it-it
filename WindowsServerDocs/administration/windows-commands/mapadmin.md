---
title: mapadmin
description: 'Argomento dei comandi di Windows per * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b17332c7-8622-4223-9c43-2fb9cf4d992d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fc4b76c1989298ea83c480b9c838ce0fc18fef5f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373765"
---
# <a name="mapadmin"></a>mapadmin



È possibile usare **mapadmin** per gestire il mapping dei nomi utente per i servizi Microsoft per il file System di rete.

## <a name="syntax"></a>Sintassi
```
mapadmin [<computer>] [-u <user> [-p <password>]]
mapadmin [<computer>] [-u <user> [-p <password>]] {start | stop}
mapadmin [<computer>] [-u <user> [-p <password>]] config <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] add -wu <WindowsUser> -uu <UNIXUser> [-setprimary]
mapadmin [<computer>] [-u <user> [-p <password>]] add -wg <WindowsGroup> -ug <UNIXGroup> [-setprimary]
mapadmin [<computer>] [-u <user> [-p <password>]] setprimary -wu <WindowsUser> [-uu <UNIXUser>]
mapadmin [<computer>] [-u <user> [-p <password>]] setprimary -wg <WindowsGroup> [-ug <UNIXGroup>]
mapadmin [<computer>] [-u <user> [-p <password>]] delete <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] list <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] backup <filename> 
mapadmin [<computer>] [-u <user> [-p <password>]] restore <filename>
mapadmin [<computer>] [-u <user> [-p <password>]] adddomainmap -d <WindowsDomain> {-y <<NISdomain>> | -f <path>}
mapadmin [<computer>] [-u <user> [-p <password>]] removedomainmap -d <WindowsDomain> -y <<NISdomain>>
mapadmin [<computer>] [-u <user> [-p <password>]] removedomainmap -all
mapadmin [<computer>] [-u <user> [-p <password>]] listdomainmaps
```

## <a name="description"></a>Descrizione
L'utilità da riga di comando **mapadmin** gestisce il mapping dei nomi utente nel computer locale o remoto che esegue i servizi Microsoft per il file System di rete. Se si è connessi con un account che non dispone di credenziali amministrative, è possibile specificare un nome utente e una password di un account che lo esegue.

Oltre agli argomenti di comando specifici, **mapadmin** accetta gli argomenti e le opzioni seguenti:

&lt;computer @ no__t-1 specifica il computer remoto che esegue il servizio di mapping dei nomi utente che si desidera amministrare. È possibile specificare il computer utilizzando un nome WINS (Windows Internet Name Service) o un nome di Domain Name System (DNS) o un indirizzo IP (Internet Protocol).

-u &lt;user @ no__t-1 specifica il nome utente dell'utente di cui si desidera utilizzare le credenziali. Potrebbe essere necessario aggiungere il nome di dominio al nome utente nel formato <em>dominio</em> **\\** <em>nome utente</em>.

-p &lt;password @ no__t-1 specifica la password dell'utente. Se si specifica l'opzione **-u** omettendo l'opzione **-p** , verrà richiesta la password dell'utente.
L'azione specifica eseguita da **mapadmin** dipende dall'argomento del comando specificato:

## <a name="parameters"></a>Parametri
### <a name="start"></a>start
avvia il servizio di mapping dei nomi utente.

### <a name="stop"></a>stop
Arresta il servizio di mapping dei nomi utente.

### <a name="config"></a>configurazione
Specifica le impostazioni generali per il mapping dei nomi utente. Con questo argomento di comando sono disponibili le opzioni seguenti: **-r &lt;dddd @ no__t-2: &lt;HH @ no__t-4: &lt;mm @ no__t-6** -specifica l'intervallo di aggiornamento per l'aggiornamento dai database Windows e NIS in giorni, ore e minuti. L'intervallo minimo è di 5 minuti.
**-i {Yes | No}** -attiva il mapping semplice (**Sì**) o disattivato (**No**). Per impostazione predefinita, il mapping semplice è on.
**Aggiungi** : crea un nuovo mapping per un utente o un gruppo. Con questo argomento di comando sono disponibili le opzioni seguenti:

|Opzione|Definizione|
|-----|-------|
|-Wu &lt;name @ no__t-1|Specifica il nome dell'utente di Windows per il quale viene creato un nuovo mapping.|
|-UU &lt;name @ no__t-1|Specifica il nome dell'utente UNIX per il quale viene creato un nuovo mapping.|
|-WG &lt;group @ no__t-1|Specifica il nome del gruppo di Windows per il quale viene creato un nuovo mapping.|
|-UG &lt;group @ no__t-1|Specifica il nome del gruppo UNIX per il quale viene creato un nuovo mapping.|
|-seprimary|Specifica che il nuovo mapping è il mapping primario.|

**seprimary** : specifica il mapping primario per un utente o un gruppo UNIX con più mapping. Con questo argomento di comando sono disponibili le opzioni seguenti:

|Opzione|Definizione|
|-----|-------|
|-Wu &lt;name @ no__t-1|Specifica l'utente di Windows del mapping primario. Se esiste più di un mapping per l'utente, utilizzare l'opzione **-UU** per specificare il mapping primario.|
|-UU &lt;name @ no__t-1|Specifica l'utente UNIX del mapping primario.|
|-WG &lt;group @ no__t-1|Specifica il gruppo di Windows del mapping primario. Se esiste più di un mapping per il gruppo, utilizzare l'opzione **-UG** per specificare il mapping primario.|
|-UG &lt;group @ no__t-1|Specifica il gruppo UNIX del mapping primario.|

**Elimina** : consente di rimuovere il mapping per un utente o un gruppo. Per questo argomento di comando sono disponibili le opzioni seguenti:

|Opzione|Definizione|
|-----|-------|
|-Wu &lt;user @ no__t-1|Utente di Windows per il quale verrà eliminato il mapping, specificato come &lt;*WindowsDomain @ no__t-2 @ no__t-3 @ no__t-4User Name @ no__t-5*. È necessario specificare l'opzione **-Wu** o **-UU** oppure entrambe. Se si specificano entrambe le opzioni, il mapping specifico identificato dalle due opzioni verrà eliminato. Se si specifica solo l'opzione **-Wu** , verranno eliminati tutti i mapping per l'utente specificato.|
|-WG &lt;group @ no__t-1|Gruppo di Windows per il quale verrà eliminato il mapping, specificato come &lt;WindowsDomain @ no__t-1 @ no__t-2 @ no__t-3groupname @ no__t-4. È necessario specificare l'opzione **-WG** o **-UG** oppure entrambe. Se si specificano entrambe le opzioni, il mapping specifico identificato dalle due opzioni verrà eliminato. Se si specifica solo l'opzione **-WG** , verranno eliminati tutti i mapping per il gruppo specificato.|
|-UU &lt;user @ no__t-1|Utente UNIX per il quale verrà eliminato il mapping, specificato come &lt;User nome @ no__t-1. È necessario specificare l'opzione **-Wu** o **-UU** oppure entrambe. Se si specificano entrambe le opzioni, il mapping specifico identificato dalle due opzioni verrà eliminato. Se si specifica solo l'opzione **-UU** , verranno eliminati tutti i mapping per l'utente specificato.|
|-UG &lt;group @ no__t-1|Gruppo UNIX per il quale verrà eliminato il mapping, specificato come &lt;groupname @ no__t-1. È necessario specificare l'opzione **-WG** o **-UG** oppure entrambe. Se si specificano entrambe le opzioni, il mapping specifico identificato dalle due opzioni verrà eliminato. Se si specifica solo l'opzione **-UG** , verranno eliminati tutti i mapping per il gruppo specificato.|

**elenco** : Visualizza informazioni sui mapping di utenti e gruppi. Con questo argomento di comando sono disponibili le opzioni seguenti:

|Opzione|Definizione|
|-----|-------|
|-tutto|elenca i mapping semplici e avanzati per utenti e gruppi.|
|-semplice|Elenca tutti gli utenti e i gruppi con mapping semplice.|
|-avanzate|Elenca tutti gli utenti e i gruppi con mapping avanzati. Le mappe sono elencate nell'ordine in cui vengono valutate. Le mappe primarie, contrassegnate con un asterisco (*), vengono elencate per prime, seguite dalle mappe secondarie, contrassegnate da un carato (^).|
|-Wu &lt;name @ no__t-1|Elenca il mapping per un utente di Windows specificato.|
|-WG &lt;group @ no__t-1|Elenca il mapping per un gruppo di Windows.|
|-UU &lt;name @ no__t-1|Elenca il mapping per un utente UNIX.|
|-UG &lt;group @ no__t-1|Elenca il mapping per un gruppo UNIX.|

**backup** : Salva la configurazione del mapping dei nomi utente e i dati di mapping nel file specificato da &lt;filename @ no__t-2.
**Restore** : sostituisce i dati di configurazione e di mapping con i dati del file (specificato da &lt;filename @ no__t-2) creati usando l'argomento del comando di **backup** .
**adddomainmap** : consente di aggiungere una mappa semplice tra un dominio Windows e un dominio NIS oppure file di gruppo e di password. Per questo argomento di comando sono disponibili le opzioni seguenti:

|Opzione|Definizione|
|-----|-------|
|-d &lt;WindowsDomain @ no__t-1|Specifica il dominio di Windows di cui eseguire il mapping.|
|-y &lt;NISdomain @ no__t-1|Specifica il dominio NIS da mappare. &lt;BR/&gt; @ no__t-2BR/&gt; **-n** &lt;nisServer @ no__t-6 specifica il server NIS per il dominio NIS specificato con l'opzione **-y** .|
|-f &lt;path @ no__t-1|Specifica il percorso completo della directory contenente i file di gruppo e di password da mappare. I file devono trovarsi nel computer gestito e non è possibile usare **mapadmin** per gestire un computer remoto per configurare le mappe in base ai file di password e di gruppo.|

**removedomainmap** : consente di rimuovere una mappa semplice tra un dominio Windows e un dominio NIS. Per questo argomento di comando sono disponibili le opzioni e gli argomenti seguenti:

|Opzione|Definizione|
|-----|-------|
|-d &lt;WindowsDomain @ no__t-1|Specifica il dominio di Windows della mappa da rimuovere.|
|-y &lt;NISdomain @ no__t-1|Specifica il dominio NIS della mappa da rimuovere.|
|-tutto|Specifica che devono essere rimosse tutte le mappe semplici tra i domini Windows e NIS. Verrà inoltre rimossa qualsiasi mappa semplice tra un dominio Windows e i file di gruppo e di password.|

**listdomainmaps** -elenca i domini di Windows di cui è stato eseguito il mapping a domini NIS o a file di gruppi e password.

## <a name="notes"></a>Note
-   Se non si specifica un argomento di comando, **mapadmin** Visualizza le impostazioni correnti per il mapping dei nomi utente.
-   per tutte le opzioni che specificano il nome di un utente o di un gruppo, è possibile usare i formati seguenti:
-   per gli utenti di Windows, usare il formato &lt;domain @ no__t-1 @ no__t-2 @ no__t-3User Name @ no__t-4, \\ @ no__t-6 @ no__t-7computer @ no__t-8 @ no__t-9 @ no__t-10user Name @ no__t-11, &gt;2 @ no__t-13computer @ no__t-14 @ no__t-15 @ no__t-16user Name @ no__ t-17 o 8computer @ no__t-19 @ no__t-20 @ no__t-21user Name @ no__t-22
-   per i gruppi di Windows, usare il formato &lt;domain @ no__t-1 @ no__t-2 @ no__t-3 @ no__t-4groupname @ no__t-5 @ no__t-6, \\ @ no__t-8 @ no__t-9computer @ no__t-10 @ no__t-11 @ no__t-12 @ no__t-13groupname @ no__t-14 @ no__t-15, &gt;6 @ no__t-17computer @ No_ _T-18 @ no__t-19 @ no__t-20 @ no__t-21groupname @ no__t-22 @ no__t-23 o \\4computer @ no__t-25 @ no__t-26 @ no__t-27 @ no__t-28groupname @ no__t-29 @ no__t-30
-   per gli utenti UNIX, utilizzare il formato &lt;NISdomain @ no__t-1 @ no__t-2 @ no__t-3User nome @ no__t-4, &lt;user nome @ no__t-6 @ no__t-7 @ no__t-8NISdomain @ no__t-9, User &gt;0name @ no__t-11 @ no__t-12 o PCNFS @ no__t-13 @ no__t-14user @ no__t-15
-   per i gruppi UNIX, usare il formato &lt;NISdomain @ no__t-1 @ no__t-2 @ no__t-3groupname @ no__t-4, &lt;groupname @ no__t-6 @ no__t-7 @ no__t-8NISdomain @ no__t-9, &gt;0groupname @ no__t-11 @ no__t-12 o PCNFS @ no__t-13 @ no__t-14groupname @ no__t-15

## <a name="additional-references"></a>Riferimenti aggiuntivi
[Indicazioni generali sulla sintassi della riga di comando](command-line-syntax-key.md)
